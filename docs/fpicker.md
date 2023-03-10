# Fpicker:一个基于 Frida 的 Fuzzing 套件，支持多种模式

> 原文：<https://kalilinuxtutorials.com/fpicker/>

[![](img/d79a6cc848f7ecf1c223edc79a9df1ee.png)](https://1.bp.blogspot.com/-eHrVdLN1ijo/YTGk80k1oNI/AAAAAAAAKp4/Lk1WHN5gfAwXq-ZBZD9uVXyhCyNEM-0NgCLcBGAsYHQ/s728/fpicker_logo%2B%25281%2529.png)

Fpicker 是一个基于 Frida 的 fuzzing 套件，它为进程内 fuzzing 提供了多种 fuzzing 模式，例如 AFL++模式或被动跟踪模式。它应该可以在 Frida 支持的所有平台上运行。

*   安装说明
*   构建和运行
*   创建一个模糊的线束
*   模式和配置

一些背景信息和 fpicker 背后的思想和观点可以在我写的一篇博客中找到。

Fpicker 是在我硕士论文期间开发的牙签工具的基础上开发的。fpicker 大部分是在我的雇主(ERNW)工作时间开发的。

**要求和安装**

运行 fpicker 需要:

*   frida_compile 将线束脚本编译成一个 JS 文件
*   在 Frida 上找到的各个平台的`**frida-core-devkit**`在 GitHub 上发布
    *   根据您想要的平台，将库存储为`**frida-core-ios.a**`、`**frida-core-macos.a**`或`**frida-core-linux.a**`。另外，linux 和 macOS/iOS 显然有不同的头文件。

仅在 AFL++模式下运行时需要:

*   AFL++
    *   在 macOS 上:
        *   用 **`CFLAGS="-DUSEMMAP=1"`编译。**
    *   在 iOS 上:
        *   应用 aflpp-ios.patch。这将共享内存和输出文件模式更改为 666，而不是 600。Fpicker 需要在 iOS 上以 root 身份运行。如果目标没有以 root 用户身份运行，它将无法读写共享内存。
        *   用 **`CFLAGS="-DUSEMMAP=1"`编译。**

**建设和运行**

Fpicker 可以为`**macOS**`、`**iOS**`或`**Linux**`打造。Makefile 目前只支持在 macOS 上构建 iOS，但是在 Linux 上使用 iOS 工具链构建 fpicker 应该是完全可能的。

根据所需的目标运行:

**制作 fpicker-macos
制作 fpicker-ios
制作 fpicker-linux**

来构建 fpicker。

一旦 fpicker 建立起来，接下来需要建立 fuzzing 线束:

请参见示例文件夹，了解不同的模糊案例示例。一般方法如下:

*   为目标创建一个自定义线束(如`**examples/test/test.js**`)(参见此处了解更多线束信息)
*   使用 frida-compile `**frida-compile test.js -o harness.js**`编译定制线束

现在 fpicker 可以开始起毛了。确切的命令高度依赖于配置和设置。下面给出几个例子。这些大多对应于示例文件夹中的示例。

*   将 fpicker 作为附加到目标进程的 AFL++代理运行，模糊化进程中的特定函数:

**afl-fuzz -i 示例/测试网络/in-o ./示例/测试网络/out — \
。/fpicker–fuzzer-mode AFL-e attach-p test-network-f ./examples/test-network/harness . js**

*   以独立模式运行 fpicker，连接到服务器并运行客户端程序来发送模糊输入:

**。/fpicker–fuzzer-mode standalone-e attach-p server-process-f harness . js–input-mode cmd \
–command "。/client-send @ @ "-I indir-o outdir**

*   在独立模式下运行 fpicker，连接到服务器，使用自定义的 mutator cmd:

**。/fpicker–fuzzer-mode active–communication-mode shm-e attach-p server-process-f harness . js \
-I indir-o outdir–standalone-mutator cmd–mutator-command " Rada MSA "**

*   以被动模式运行 fpicker，连接到收集覆盖率和有效负载的服务器:

*   **。/fpicker–fuzzer-mode passive–communication-mode send-e attach-p server-process-o outdir-f harness . js**

*   以独立模式运行 fpicker，连接到远程设备上正在运行的进程，使用自定义的 mutator cmd 对进程内进行模糊处理:

**。/fpicker–fuzzer-mode active-e attach-p test-D remote-o examples/test/out/-I examples/test/in/\
-f fuzzer-agent . js–standalone-mutator cmd–mutator-command " Rada MSA "**

**创建起毛线束**

每个目标都需要自己的模糊装具。这个工具最重要的部分是定义 Frida 的跟踪者的入口函数，它有效地决定了仪器插入的点。在`**in-process**`模式下，这很简单。该函数通常是在每次模糊迭代中调用的函数。然而，它也可以是不同的。

最低限度的利用实现(在`**command**`模式下)可能是这样的:

/ **/导入 fuzzer 基类
const Fuzzer = require(" harness/Fuzzer . js ")；
//自定义 fuzzer 需要继承 Fuzzer 类才能正常工作
类 TestFuzzer 扩展 Fuzzer。Fuzzer {
构造函数(){
//构造函数需要指定目标函数的地址和一个 NativeFunction
//对象，以便 Fuzzer 调用。
const FUZZ _ FUNCTION _ ADDR = module . getexportbyname(null，“FUZZ _ FUNCTION”)；
const FUZZ _ FUNCTION = new native FUNCTION(
FUZZ _ FUNCTION _ ADDR，
"void "，["pointer "，" int64"]，{
})；
超级("测试"，模糊 _ 函数 _ADDR，模糊 _ 函数)；
}
}
const f = new TestFuzzer()；
exports . fuzzer = f；**

该线束将仪器配置为遵循功能`**FUZZ_FUNCTION**`。当进入该函数时，检测将开始，当该函数返回时，检测将停止。应该仔细选择这个函数，因为它很昂贵，而且检测的过程部分越多(潜在的不重要), fuzzer 就越慢。当然，这是在速度和预期覆盖范围之间的考虑。此外，模糊化器目前仅支持在一次模糊化迭代期间仅输入一次的函数，即，在一次模糊化的情况下，该函数不应被调用超过一次，否则覆盖信息可能变得不可靠。

当使用`**in-process**`模式时，fuzzer 脚本中需要另一个功能。`**fuzz**`法。它将在每次迭代中被调用。将使用两个参数调用它，一个指向缓冲区的指针和缓冲区的长度。我们的示例性目标函数有两个参数，一个指向缓冲区的指针和它的长度。因此，我们可以只传递在`**fuzz**`方法中得到的参数。

**fuzz(payload，len){
this . target _ function(payload，parse int(len))；
}**

在`**passive**`模式中，需要指定一个处理所需数据的回调。fuzzer 期望接收有效载荷缓冲区及其长度。根据被模糊化的目标函数，需要提取这些数据。在下面的例子中，我们又有一个有两个参数的函数:指向缓冲区的指针和它的长度。`**args**`参数包含目标函数接收到的所有潜在参数，因此长度参数(在我们的例子中是第二个)可以通过`**args[1]**`访问。然后我们读取缓冲区为`**Uint8Array**`，并使用`**sendPassiveCorpus**`方法将其发送回模糊化器。

**passive callback(args){
const len = args[1]；
const data = new uint 8 array(memory . readbytearray(args[0]，parse int(len))；
// this 对数据进行编码，并发送回 fuzzer
this . sendpassivecorpus(data，len)；
}**

如果目标需要在 fuzzer 启动前做一些准备，fpicker 提供了一个在 fuzzer 初始化期间调用的`**prepare**`方法。准备可以是例如通过实例化对象来建立状态。这种准备功能可能如下所示:

**prepare() {
//可以将对象附加到 fuzzer 实例上，以便稍后可以在
// fuzz()方法中使用。
this . required _ object = call _ native _ function _ that _ creates _ object()；
}**

**模式和配置**

pficker 提供了大量的模式和配置，下面将对此进行解释。这些模式中的大多数可以以不同的方式组合。本节末尾的表格显示了哪些选项可以组合以及它们的实施状态。

**模糊模式**

Fpicker 有三种不同的*模糊模式* : AFL++模式、独立主动模式和独立被动模式:

*   **AFL++模式:**在 AFL++模式下，fpicker 充当 AFL++和目标进程之间的代理。使用 Frida 的检测功能，AFL 的覆盖位图被填充，而目标被 AFL++生成的输入数据模糊化。
*   **独立主动模式:**在独立主动模式下，模糊化器使用 Frida 的跟踪者调用摘要来收集迭代期间执行的基本块形式的覆盖范围。这不是什么新鲜事，以前已经以各种形式实现过。然而，结合其他一些模糊设置，这可以有各种好处。如果 AFL++在给定的环境或情况下不适用或不需要，这也是一个很好的选择。
*   **独立被动模式:**被动模式不太像引信，更像追踪器。本质上，它与独立活动模式的作用相同。然而，它不*而不是*发送自己的输入。它只是依附于某个功能，收集覆盖率。一旦观察到新的覆盖范围，覆盖范围和输入都被存储。

**输入模式**

虽然 fpicker 主要被设计为一个进程内模糊化器，但它也支持通过外部命令进行模糊化。为此，fpicker 提供了两种输入模式。

*   **进程内输入模式:**在进程内输入模式下，线束直接调用目标进程中指定的函数。fuzzer 将有效载荷发送到 harness，harness 准备有效载荷，以便调用目标函数。
*   **输入模式 CMD:** 在命令输入模式下，有效载荷被重定向到外部命令。这是有用的，当直接调用目标函数时，准备其它状态的参数太复杂了。覆盖率集合仍然需要附加到某个函数上。也许有一个客户端可以提供一个有效载荷，然后触发目标函数。

**通信模式**

通信模式决定了注入的线束如何与引信通信。这很大程度上取决于目标应用程序。Frida 提供了一个 API 来发送和接收来自注入代理脚本的消息。这种类型的通信是相当昂贵的。其中一个因素是传输的消息需要用 JSON 编码。所以发送二进制数据非常简单。因此，fpicker 在共享内存上提供了第二种通信模式。然而，这只有在 fuzzer 和目标应用程序之间可以建立共享内存的情况下才有效，这意味着当目标通过 USB 连接到 fuzzer 主机时，不能使用这种模式。在 CMD 输入模式下，通信模式仅指如何将覆盖信息传送回模糊器，而不是如何发送有效载荷，因为这取决于外部命令。

*   **通信模式发送:**在发送通信模式下，通过使用 Frida 的 RPC 调用机制发送有效载荷。这让 fuzzer 在注入的线束脚本中执行 JavaScript 函数。线束中的这个函数可以为调用目标函数做所有必要的准备。一旦目标函数从返回，覆盖收集将停止，并且线束可以向模糊器发出信号，表明迭代已经完成。这是通过使用 Frida 的 send API 将覆盖信息发送回 fuzzer 来完成的。
*   **通信模式 SHM:** 在 SHM 通信模式下，fuzzer 和线束脚本通过共享内存和信号量进行通信。共享内存中的缓冲区用于发送有效载荷和接收覆盖信息。这两个组件不是发送和接收，而是等待和发送到信号量。根据系统和目标的不同，这会带来相当多的性能提升。尤其是，因为二进制有效载荷被写入存储器一次，并且不必被编码和解码或复制到其他存储器位置。不幸的是，当使用 AFL++运行时，这种模式有时会导致较低的稳定性。还不知道为什么。

**执行模式**

执行模式可以是*衍生*或*附加*。这是不言自明的。fpicker 既可以附加到正在运行的进程，也可以派生一个进程。这两种模式的一个主要区别是，如果连接的目标崩溃，fpicker 不会尝试重生。

**独立变异体**

在独立模式下，fpicker 提供了三种不同的输入变异策略。说得好，输入突变当然有很大的改进空间。

*   **独立的赋值器 NULL:** 这个赋值器不会对有效载荷进行赋值，只是返回相同有效载荷的一个副本。主要用于测试目的。否则没什么用。
*   **独立变异器 Rand:** 一个非常糟糕的随机变异器。它所做的只是随机替换原始有效载荷中随机位置的值。它不会改变有效负载长度。
*   **独立的 mutator 自定义:**这个 Mutator 可以调用外部命令来变异有效载荷。它将有效负载写入标准输入，并从标准输出接收变异的有效负载。由于它的浅实现，它有相当大的性能影响。

**网络设备**

使用选项`**-D remote**`可以模糊网络设备上运行的进程。为此，远程设备必须运行`**frida-server**`。作为一个示例配置，使用带端口转发的 SSH 将远程设备上的`**frida-server**`默认监听端口`**27042**`绑定到本地客户机上的一个套接字。

**ssh-N user @ network . device-L**127 . 0 . 0 . 1:27042:127 . 0 . 0 . 1:27042

然后使用`frida-ps`通过列出远程设备上的进程来验证配置:

**芙烈达-PS-r￥t1**

[**Download**](https://github.com/ttdennis/fpicker)