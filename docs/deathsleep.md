# DeathSleep:终止当前线程和恢复的回避技术的 PoC 实现

> 原文：<https://kalilinuxtutorials.com/deathsleep/>

[![](img/97162af2c6a0dda86572e5d3d74144fe.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgN6DdOdHII2Cl6jtqQbKAUOj6fb8ui4v1DLSgxL2kFaNKITADXlvrmrbhJjmnACsLmDpRxrdb7Z6L-ffoloz1JMjEZneC8vbhs7k0oe37DZiIsXJqlEFOqrInY9b1I8EXnKEizU26-2ndB5VMSPJ0Iz3JY3pstafmVYUPU5kCNJO0Cu2TE55MMP75G/s728/9h4q698razh91.png)

**DeathSleep** ，一种回避技术的 PoC 实现，用于在恢复执行之前终止当前线程并恢复它，同时在不执行期间实现页面保护改变。

## 简介

Sleep 和 obfuscation 方法在 maldev 社区中是众所周知的，它们有不同的实现，它们的目标是在睡眠时隐藏内存扫描器，通常会更改页面保护，甚至添加一些很酷的功能，如加密外壳代码，但隐藏外壳代码还有另一个要点，即隐藏当前的执行线程。欺骗堆栈很酷，但是在稍微思考之后，我认为没有必要欺骗堆栈…如果没有堆栈的话🙂

这项技术的可用性留给读者来评估，但无论如何，我认为这是一种很酷的方式来复习一些主题，并为像我一样的人学习一些 maldev。

这里展示的主要实现将我们需要从堆栈中取出的所有东西都保存在数据段中，作为全局变量，但是将所有东西都移到堆中的实现将很快发布。它的目的是展示一些关键的修改，需要做的，使这个代码 pic 和注入。

这个库在 GitHub 和 GitLab 之间镜像。

## 发生什么事了？

## 首先

这里陈述的一切都来自我对所涵盖的不同主题的理解，或者来自阅读，或者来自开发过程中的经验。我知道我不是专家，我最不想做的事情就是传播错误的信息，所以如果你认为有些事情是不正确的，我希望你能让我知道，你可以在 twitter 上联系我，或者在这个回购中打开问题。非常感谢您的理解。🙂

## 基础知识

这种技术的主要目的很清楚，在继续执行之前终止当前线程并恢复它，但是这到底意味着什么，以及它设置了哪些新的约束？

为了能够恢复执行，我们需要在终止线程之前保存两件事情，首先是 CPU 状态，其次是堆栈，并在新线程启动后有效地再次设置它们。

我谈到了将在这个技术中出现的新约束，有两个大的约束:首先，我们需要在堆栈外存储从线程终止到堆栈恢复所需的任何东西，正如您将看到的，这带来了一些新的挑战。

第二，我们总是需要至少另一个线程在我们的进程中运行，因为我们正在终止我们的线程，如果没有其他线程，进程将结束。我不认为这是一个大问题，因为大多数代理是在其他进程中注入的，我们可以假设这个进程将保持至少一个线程运行。

## 死亡睡眠组件

我们可以在此查看 poco 4 的核心功能:

*   主程序:这是你写代理程序代码的地方，这部分代码将使用死亡睡眠
*   **Awake 函数:**这是我们所有线程的入口点，它负责保存我们将要恢复的堆栈的起点。此外，它还负责在需要时恢复堆栈和 CPU 上下文，或者只是启动我们的主程序。
*   这是这项技术的主要功能，负责备份线程上下文和堆栈，并为即将发生的奇迹做好准备。
*   重生:一个简单的函数，只负责启动我们的新线程。

## 保存堆栈

当我们要保存堆栈时，一个问题出现了:需要保存多少堆栈？

让我们先回顾一下调用 DeathSleep 函数后堆栈中的内容(这个函数保存上下文、堆栈并为混淆和恢复做好准备)

正如我们所看到的，每个函数都有三个部分:

*   **Shadow space:** 这是一个 32 字节的空间，由调用者分配，但由被调用者使用。据我所知，如果需要的话，它的主要功能是在寄存器中保存传递给被调用函数的参数，但是它可以用于被调用函数决定的任何事情。
*   **返回地址:**这是 CALL 指令推送的调用者函数中要执行的下一条指令的地址，所以被调用者中的 RET 指令只会取这个地址，并在结束时“跳转”到这个地址。
*   **函数堆栈空间:**这是被调用者预留的空间，用来存放需要恢复的寄存器的值及其局部变量的值。

很明显，我们需要保存的堆栈的最小部分是主程序内部的所有内容，这意味着它的影子空间，它的返回地址，以及 DeathSleep 函数之前的所有内容。在此之前的任何事情都不是真正需要的(保存 entry 函数使用的堆栈有其优点，但我们将在后面讨论)，因为这是 windows 例程用于启动我们的新线程的堆栈。除此之外，我还决定存储 DeathSleep 函数的阴影空间(实际上并不需要，但是它使得醒来时 Rsp 的计算更容易)。

所以最后，我们保存了这个:

## 如何找到我们的堆栈地址

标准编译中的每一个功能都应该由三部分组成，序言、功能代码和结语。

Rsp(堆栈指针)只能在函数序言和结语中修改。序言增加了堆栈指针(记住增加堆栈意味着减少地址，因为它们的方向相反)，以保存寄存器，保存所有的局部变量，然后保存阴影空间，而结尾做的正好相反。

这意味着函数代码内部的堆栈指针应该总是指向阴影空间的末端(上图中的紫色)，通过计算 prologue 增加多少堆栈指针就可以得到函数的堆栈大小和阴影空间的总和。使用 unwind 表中保存的信息可以很容易地计算出该值，关于它们的用法的解释我们在这里不做介绍，但是作为总结，这些表用于允许任何其他线程或进程正确地在堆栈中移动以查看其内容、处理异常或分析异常。

## 捕获并准备要恢复的上下文

捕获上下文可能是最容易做的事情之一，因为我们可以在对非易失性寄存器进行任何修改之前，在 DeathSleep 的第一行简单地执行 RtlCaptureContext()。我们仍然需要对将要恢复执行的上下文做两处修改。

第一个将修改它的 Rip，正如你所记得的，这是保存下一个要运行的指令的寄存器，如果我们不修改它，执行将在 DeathSleep 函数中恢复。我们要做的是改变 Rip 来保存 DeathSleep 的返回地址，这是由当前的 Rsp 所指向的，替换了尾声中增加的大小(上图中的绿色+紫色区域)。

第二个修改将在线程恢复时完成，它意味着将 Rsp 设置为指向我们恢复的堆栈的顶部；这将在恢复阶段完成，因为我们不知道我们的新堆栈将放在哪里。该值将只是我们恢复的堆栈的结束地址，因为正如我们稍后讨论的，我们还复制了死亡睡眠的调用者保留的阴影空间，这正是 RSP 在调用死亡睡眠之前的值。

## 恢复我们的堆栈

一旦我们到达唤醒点，就在恢复执行之前，我们需要将保存的堆栈放在适当的位置。我们已经知道，我们保存的堆栈是从 awake 函数捕获的地址开始的，所以新捕获的地址将是我们放置保存的堆栈的起点，但这带来了一个问题，在我们放置旧堆栈后，任何对函数的调用都会修改它并破坏它，在这里进行清理非常方便，特别是释放了用于保存堆栈备份的堆。这意味着我们需要将我们当前的 Rsp 以及我们当前正在使用的部分堆栈移动到我们将放置恢复的堆栈的外部位置。试图让它在这里更清楚是一个问题

## 还原上下文

在我们完成所有艰苦的工作之后，最后要做的事情是使用 NtContinue，这个函数允许我们用之前捕获和修改的上下文来改变当前的上下文，在调用 DeathSleep 之后立即设置 RIP，所有的寄存器应该具有和调用 DeathSleep 时相同的值，RSP 应该指向堆栈的顶部。

## 安排恢复过程:使用线程池 API

好了，我们知道了存储和恢复当前线程需要做的基本工作，但是我们需要在没有线程的情况下也能运行所有这些。在这里，我们遇到了可爱的线程池 API，这是 Windows 提供的一个工具，它允许我们将任务(最多一个参数的函数)排队到一组线程(一个池)中，这些线程将完全由操作系统管理。如果你见过 Ekko，你可以看到它使用了这个 API，所以…我们用同样的方法实现它。

一切都很好，但有一个问题，一个工人甚至在结束执行其排队的任务后仍在工作。这是一个问题，因为我想销毁我们的程序可以生成的所有线程，所以这不是办法。

深入研究之后，我发现 Ekko 中使用的线程池 API 是一个旧版本，有一个新版本具有更多功能，在它们之间有一个函数可以有效地解决我们的问题:CloseThreadPool()。这个新的 API 允许我们创建自己的池，并在使用它们之后销毁它们，终止所有使用的工人。它提供了另外两个优点:设置最大数量的线程和清理组。设置线程的最大数量将允许我们顺序地执行所有的任务，只要它们以任何时间差排队。清洁组有助于在完成所有工作后使清洁工作变得更加容易。

那么…一切都搞定了吗？好了，在这一点上线程被终止，我们正在排队重生函数，它创建一个新的线程，以 awake 作为它的入口点，恢复以前的状态并关闭池，到目前为止一切顺利！

## 更改内存权限，重定向执行

当我结束我们之前讨论的所有内容时，我认为困难的部分已经解决了，因为这部分已经通过以前的技术解决了，但是，哦，我不知道接下来会发生什么。

主要问题是，我们需要在代码之外卸载它，因为我们正在将内存保护更改为 RW(读写)，如果我们调用 VirtualProtect()，当函数返回时，我们的进程将崩溃(我们不能在 RW 页面中执行指令)，因此我们需要找到一种方法从其他地方执行它，并使它也返回到一些 RX(读-执行)页面(当返回时会发生同样的事情)。显然，我们也将为此使用线程池 API，但是有一个问题，我们只能给我们的任务一个参数，而 VirtualProtect()需要 4 个参数。

为此，我们将再次使用 NtContinue()，我第一次看到这个函数的使用是在叶子上，但它也在 Ekko 中使用。正如我们之前看到的，NtContinue()允许我们为调用它的线程设置一些上下文，通过一些巧妙的调整，它可以“调用”一个具有多个参数的函数，只需使用一个参数(对于线程池 API 来说非常方便)。主要思想是将 RIP 设置为函数的起始地址，并且，由于 windows x64 调用约定在寄存器中传递前四个参数(rcx、rdx、r8、r9，按此顺序)，只需将参数放在将传递给 NtContinue 和的上下文结构中，它将有效地模拟对函数的调用。当使用 NtContinue 时，我们必须注意的最后一件事是 Rsp，因为，正如我们之前看到的，当函数被调用时，这个地址应该保存返回地址。

因此，我们需要 NtContinue 工作的第一件事是获得一个上下文，我们可以手动创建它，但我们会发现一个问题，找到 Rsp 的值，当传递给我们的函数时，它将指向 RET 返回的地址。我们的任务将在不同的线程中工作，所以我们不知道它的堆栈将放在哪里。解决方案(小心偷自 Ekko，非常感谢:P)是用 rtlcaptrecontext()取一个 worker 内部的上下文的副本，将得到的上下文的堆栈指针增加 8，这样它就会指向调用 rtlcaptrecontext()在堆栈中引入的地址，也就是最后这个函数的返回地址，我们可以用它作为我们所有函数的返回地址。

好的，这很好，但是当我们不能对 Rsp 进行修改时会发生什么呢？这就是我们去泡沫时发生的，我们将在一个新的线程中，所以旧的上下文的 Rsp 是无用的。我们需要一个新的上下文，取自新的线程，但是我们不能使用修改 Rsp 的老技巧来指向正确的地址。

## Rop 链条

所以我们不能修改获得的上下文，但这并不意味着它是无用的，实际上我们会使用它，但以不同的方式。如果我们只是用 NtContinue()恢复该上下文，而不修改它的 Rip，它将只是在调用 RtlCaptureContext()之后，使用正确的 Rsp 将执行重定向到下一条指令，这样我们就可以在使用修改的上下文调用 NtContinue()之后使用它，以便能够正确地结束任务的执行。为此，我们将使用一个 Rop 链，通过将第一个上下文的 Rsp 设置为指向一个手工创建的堆栈，该堆栈将保存重定向执行所需的所有内容，直到第二个 NtContinue()调用将正确的上下文设置为 end。

我们使用了两个 rop 小工具，一个用于固定或“跳过”我们函数的阴影空间，另一个负责将 NtContinue 的参数放在 rcx 中，然后返回。

找到这个 2 rop 小工具相当容易，用于修复阴影空间的小工具只是几乎任何函数的尾声(我发现仅在 Ntdll 中就有超过 500 个命中)，因为正如我们之前看到的，尾声主要是为了减少 Rsp，第二个只是一个 pop rcxret 这是 2 个字节，还发现了 Ntdll 和 Kernel32 dlls 之间的一些字节。

## 线程池 Api 的一点反转

正如我们看到的，使用 NtContinue 只需要填充它的第一个参数就可以工作，这对于旧的线程池 API 来说是完美的，但是在新的线程池 API 中，参数是在第二个位置传递的，所以，是的，仅仅这样是不行的。

几个小时后，我不知道如何解决最后一个问题，我想到这两个 API 在某些情况下使用相同的函数，这使我认为它们可能比它们看起来更相似，所以我决定研究它们之间的关系。

对于旧的 api，我们使用 CreateTimerQueueTimer()对我们的任务进行排队，在新的 API 中，我们需要两个函数来做同样的事情:CreateThreadpoolTimer()，它将接受回调函数和传递给它的参数，并将返回一个指向描述任务的 TP_TIMER 结构的指针；以及第二个用于对任务进行排队的函数:SetThreadpoolTimer()，它将接受前一个指针和一个指针 FILETIME 结构，后者描述任务何时执行。

所以我们可以看到 CreateThreadpoolTimer()只是 TpAllocTimer()的一个花哨的包装器，SetThreadpoolTimer()只是 TpSetTimer()的一个转发器。

现在让我们检查 CreateTimerQueueTimer()的内部。起初，它只是 Ntdll 中一个函数 RtlCreateTimer()的另一个花哨包装，神奇的事情就发生在这里。

正如您所看到的，在这个函数内部，实际上有一个对 TpAllocTimer()和 TpSetTimer()的调用，这类似于在函数内部调用 CreateThreadpoolTimer()和 SetThreadpoolTimer()。正如我们所看到的，我们正在排队的函数并不是我们给该函数的回调函数，而是将 RtlpTpTimerCallback()设置为回调函数。如果您还没有意识到所有这些意味着什么，我们正在使用 CreateThreadpoolTimer()对一个在第二个位置接收其参数的函数进行排队，RtlpTpTimerCallback()，它将执行另一个在第一个位置接收其参数的函数。

因此，我们唯一需要了解的是回调信息是如何传递给 RtlpTpTimerCallback()的，经过一些反转后，我以下面的结构结束，令人惊讶的是，它工作了！

现在我们可以调用在第一个位置接收参数的函数，同时我们可以关闭我们的池，并且不运行任何线程，赢赢。需要注意的是，这个函数不是在 Ntdll 中导出的，所以我决定通过它在 dll 中的字节形式来找到它。

这就是结尾，回顾了所有内容后，我想我给出了开发 POC 时产生的核心想法，以及为什么所有事情都是以我的方式完成的。

[**Download**](https://github.com/janoglezcampos/DeathSleep)