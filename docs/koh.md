# Koh:代币盗窃者

> 原文：<https://kalilinuxtutorials.com/koh/>

[![](img/6962e3c8f9c455af2617a553f5c5962a.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjIpZwVU2A5K6dDacSKbsAiv3XkfKPQPc0eusGAehjB9hIihUKs5rE1v6Mr8_bXr6dihORhNmV01K8HsGy9TSgif8KGx_NyKrHqEnT74T1WedwifdwHyR0Zn0luui0akdC6zj_44Pcj6p_a0s7LRl5sESlD_XOJqqZDzkv2Si1JDtN7pnDRKF11kRro/s728/Token_Stealer%20(1).png)

**Koh** 是一个 C#和信标对象文件(BOF)工具集，允许通过有目的的令牌/登录会话泄漏来捕获用户凭证材料。

一些代码的灵感来自 Elad Shamir 的内部独白项目(无许可证)，以及 KB180548。关于为什么这是可能的以及 Koh 的方法，请参见本自述文件的技术背景部分。

关于 Koh 背后的动机及其方法的更深入的解释，请参见 Koh:Token stealter 帖子。

@harmj0y 是这个代码库的第一作者。@tifkin_ 帮助了方法、BOF 实现和一些令牌机制。

## Koh 服务器

Koh“服务器”捕获令牌，并使用命名管道进行控制/通信。这可以包装在 Donut 中并注入到任何~~高完整性~~系统进程中(参见 Inline Shenanigans Bug)。

## 编译

我们不打算为 Koh 发布二进制文件，所以你必须自己编译🙂

Koh 是针对。NET 4.7.2 并兼容 Visual Studio 2019 社区版。只需打开项目。sln，选择“发布”，构建。`**Koh.exe**`装配和`**Koh.bin**`环形构建的 PIC 将被输出到主目录。Donut blob 同时兼容 x86/x64，并使用位于`**./Misc/Donut.exe**`的 Donut v 0 . 9 . 3 使用以下选项构建:

**【实例类型:嵌入式
【熵:随机名称+加密
【压缩:Xpress Huffman
【文件类型:。NET EXE
【参数:捕获
【目标 CPU:x86+amd64
【AMSI/WDLP:中止**

### 使用

`**Koh.exe Koh.exe <list | monitor | capture> [GroupSID... GroupSID2 ...]**`

*   **列表**–列出(非网络)登录会话
*   **监控**–监控新的/唯一的(非网络)登录会话
*   **捕获**–为新(非网络)登录会话的每个 SID 捕获一个唯一令牌

也可以通过命令行提供组 sid，从而使 Koh 只监视/捕获在其协商的令牌信息中包含指定组 sid 的登录会话。

## Koh 客户端

当前可用的客户端是在`**.\Clients\BOF\**`的信标对象文件。在您的 Cobalt Strike 客户端中加载`**.\Clients\BOF\KohClient.cna**`侵略者脚本，以启用 BOF 对 Koh 服务器的控制。使用捕获令牌的唯一要求是 **SeImpersonatePrivilege** 。通信命名管道有一个“every one”DACL，但是使用一个基本的共享密码(super securez)。

要在 Linux 上使用 Mingw 进行编译，请参见`**.\Clients\BOF\build.sh**`脚本。唯一的要求(至少在 Debian 上)应该是`**apt-get install gcc-mingw-w64**`

### 用法

**beacon>help KOH
KOH list–列出捕获的令牌
koh 组 LUID–列出捕获的令牌的组 SID
KOH 过滤器 list–列出用于捕获过滤的组 SID
KOH 过滤器添加 SID–添加用于捕获过滤的组 SID
KOH 过滤器删除 SID–从捕获过滤中删除组 SID
KOH 过滤器重置–重置 SID 组捕获过滤器
koh 模拟 LUID–模拟 带有给 LUID
koh 的已捕获令牌释放全部–释放所有已捕获令牌
koh 释放 LUID–释放指定 LUID 的已捕获令牌
koh 退出–通知 koh 服务器退出**

### 群组 SID 过滤

`**koh filter add S-1-5-21-<DOMAIN>-<RID>**`命令将只捕获包含所提供的组 SID 的令牌。该命令可以运行多次，以添加更多 sid 进行捕获。这有助于防止由于大量令牌泄漏而可能出现的稳定性问题。

## 技术背景

当在系统上建立新的登录会话时，LSASS 使用 NtCreateToken() API 调用创建登录会话的新令牌，并由 LsaLogonUser()的调用方返回。这增加了登录会话内核结构的 ReferenceCount 字段。当此 ReferenceCount 达到 0 时，登录会话将被销毁。由于“为什么这是可能的”一节中描述的信息，如果令牌句柄仍然存在，Windows 系统**将不会**释放登录会话(因此引用计数！= 0).

因此，如果我们可以通过令牌获得新创建的登录会话的句柄，我们就可以保持该登录会话打开，并在以后模拟该令牌以利用它包含的任何缓存凭据。

为什么这是可能的

MS16-111 被应用回 Windows 7/Server 2008，因此这种方法应该对除 Server 2003 系统之外的所有系统都有效。

## 接近

通过使用 lsenumeratelongsessions()Win32 API，枚举登录会话很容易(从提升的上下文中)。更困难的是获取一个特定的登录会话标识符(LUID)和*以某种方式*获取一个链接到该会话的可用令牌。

### 可能的方法

我们集思广益，想出了一些方法来 a)保持开放的登录会话，b)滥用这种方法进行令牌模拟/使用缓存的凭据。

1.  第一种方法是使用 **NtCreateToken()** ，它允许您指定登录会话 ID (LUID)来创建新令牌。
    *   不幸的是，你需要**secretatetokenprivilege**，传统上只有 LSASS 持有，这意味着你需要窃取 LSASS 的令牌，这并不理想。
    *   一种可能性是通过 LSA 策略修改将**secretatetokenprivilege**添加到 NT AUTHORITY\SYSTEM，但是这将需要重新启动/新的登录会话来表达新的用户权限。
2.  您还可以通过使用 **WTSQueryUserToken()** 来获得要克隆的新桌面会话的令牌，从而只关注远程交互式登录会话。
    *   这显然是 Ryan 演示的方法。
    *   不幸的是，这错过了新创建的本地会话和从 PSEXEC 等创建的传入会话。
3.  在新的登录会话中，打开每个可访问进程的句柄，并枚举所有现有句柄，克隆链接到新登录会话的令牌。
    *   这需要打开很多进程/句柄，看起来非常可疑。
4.  下面描述的**acquire credentialshandle()**/**InitializeSecurityContext()**/**acceptsecuriycontext()**方法就是我们所用的方法。

### 我们的方法

SSPI AcquireCredentialsHandle()调用具有一个 **pvLogonID** 字段，该字段声明:

**指向标识用户的本地唯一标识符(LUID)的指针。此参数是为文件系统进程(如网络重定向器)提供的。**

**注意:**为了利用与**acquire credentialshandle()**的登录会话 LUID，您需要 **SeTcbPrivilege** ，然而这通常比**secretatetokenprivilege**更容易获得。

在指定登录会话 ID/LUID 时使用此调用似乎会增加登录会话结构的 ReferenceCount，从而阻止其被释放。然而，我们没有遇到另一个问题:给定一个“泄漏的”/持有的开放登录会话，我们如何从中获得一个可用的令牌？WTSQueryUserToken() 仅适用于桌面会话，我们没有发现任何用户域 API 可以让您将 LUID 映射到可用的令牌。

*然而*我们可以使用两个额外的 SSPI 函数，InitializeSecurityContext()和 AcceptSecurityContext()来充当我们自己的客户端和服务器，协商一个新的安全上下文，然后我们可以使用 QuerySecurityContextToken()来获得一个可用的令牌。这在 KB180548(此处由 PKISolutions 反映)中有记录，用于凭据验证。这是一种类似于内心独白的方法，只是我们要完成整个握手过程，生成一个令牌，然后保存它以备后用。

然后可以通过 CheckTokenMembership()或 GetTokenInformation()对令牌本身进行过滤。例如，我们可以释放任何令牌，除了属于域管理员或我们希望锁定的特定组的令牌。

### 相对于传统凭据提取的优势/劣势

#### 优势

*   适用于本地和入站(非网络)登录。
*   适用于通过 Kerberos 和 NTLM 创建的入站会话。
*   不需要打开多个进程的句柄。
*   不创建新的登录事件或登录会话。
*   在正常的系统票证续订行为之外，不会在 DC 上创建额外的事件日志(我不认为？)
*   令牌上没有默认的生存期(我不认为？)因此，只要被捕获的帐户的凭证没有改变并且系统没有重新启动，*访问*就应该工作。
*   在系统上重用合法的捕获授权，所以应该“与噪声融合”得相当好。

#### 缺点

*   只有系统不重启，访问才可用。
*   不允许您在其他系统上重用访问权限
    *   但是，仍然可以在泄漏的登录会话中提取现有的票证/凭据。
*   如果泄漏了大量会话，可能会导致不稳定(虽然这可以通过令牌组 SID 过滤来缓解)并限制捕获的最大令牌数(此处默认为 1000)。

## 内联恶作剧 Bug

我已经编码很长时间了。这是我最近遇到的最奇怪、最令人沮丧的 bug 之一——请帮助我完成这个 lol。

*   当 Koh.exe 程序集从提升的(但非系统)上下文中运行时，一切都正常工作。
*   如果 Koh.exe 装配通过 Cobalt Strike 的 Beacon fork&run 流程从一个提升的(但非系统的)上下文中运行，那么一切正常。
*   如果 Koh.exe 程序集为运行在系统上下文中的 Cobalt Strike Beacon 运行*内联*(通过 InlineExecute-Assembly 或 Inject-Assembly)，那么一切都正常工作。
*   **然而**如果 Koh.exe 程序集运行*内联*(通过 InlineExecute-Assembly 或 Inject-Assembly)用于运行在提升的、而不是系统的上下文中的 Cobalt Strike Beacon，那么对 AcquireCredentialsHandle()的调用将失败，返回`**SEC_E_NO_CREDENTIALS**`，并且\_(ツ)_/的所有操作都将失败

我们已经尝试过(没有成功):

*   将所有事情都分离到一个单独的线程，指定一个 STA 线程单元。
*   试图诊断 RPC 的不可思议之处(这里还有更多需要研究)。
*   使用 DuplicateTokenEx 和 SetThreadToken 而不是 ImpersonateLoggedOnUser。
*   在 AcquireCredentialsHandle 调用之前检查我们是否有适当的 SeTcbPrivilege(我们有)。

对于所有意图和目的，调用 AcquireCredentialsHandle 之前的线程上下文在该上下文中工作，但是结果出错。我们不知道为什么。

如果你知道这可能是什么，请告诉我们！如果您想尝试使用更简单的程序集，请查看我的 GitHub 上的 AcquireCredentialsHandle repo 进行故障排除。

## IOCs

引用@tifkin_ *“一切都是隐秘的，直到有人去寻找它。”*虽然 Koh 的方法与其他方法略有不同，但仍有 IOC 可用于检测它。

C# Koh 收集器的唯一 TypeLib GUID 是`**4d5350c8-7f8c-47cf-8cde-c752018af17e**`，详见本报告中的 Koh.yar Yara 规则。如果这在编译时没有改变，那么它应该是 Koh 服务器的一个非常高保真的指示器。

当 Koh 服务器启动时，它会打开一个名为`**\\.\pipe\imposecost**`的命名管道，只要 Koh 在运行，这个管道就会保持打开状态。Koh 通信使用的默认密码是`**password**`，因此向任何`**\\.\pipe\imposecost**`管道发送`**password list**`将让您确认 Koh 是否确实在运行。使用的默认模拟管道是`**\\.pipe\imposingcost**`。

如果 Koh 在提升的上下文中启动，而不是作为系统启动，则执行`**winlogon**`的句柄/令牌克隆以执行`**getsystem**`类型提升。

我确信没有攻击者会改变上面提到的指标。

可能有一些我们希望研究的令牌捕获的 RPC 工件。如果我们在这些方面发现任何额外的检测工件，我们将更新自述文件的这一部分。可以研究挂钩 Koh 使用的一些可能不常见的 API(lsenumeratelongsessions 或特定的 AcquireCredentialsHandle/InitializeSecurityContext/AcceptSecurityContext，特别是在 acquire credentialshandle 中使用 LUID)的有效性，但唉，我不是 EDR。

## 缓解措施

在发布了 Koh:Token stealter 的帖子后，我在@cnotin 和@SteveSyfuhs 之间进行了一次很好的交流，讨论了最终如何部分缓解这种方法。

KB2871997 修补程序引入了一个`**TokenLeakDetectDelaySecs**`设置，该设置会触发“*…清除已注销用户的任何凭据……*”。事实上，默认情况下，“受保护用户”安全组的成员会强制执行此行为，而不管注册表设置如何。但是，将此项设置为非零值将在用户注销时从内存中清除所有凭据。具体来说，正如史蒂夫提到的:`**If set, it'll start a timer on a sessions *interactive* logoff event, and on fire will purge anything still tied to it. Off by default. Protected Users always on, with a default of 30s.**`

上一段有两个重要的地方需要注意:“注销事件”和“交互”。在某些情况下，这可能会导致用户的凭据未被清除:

*   如果凭证是通过`**runas**`或`**runas /netonly**`类型的 spawn 或类似的方式出现的，那么当进程停止时不会发生注销事件，并且凭证/令牌仍然可以被捕获。
*   如果凭据是通过 RDP 会话提供的，而用户只是断开连接而不是注销，则在进程停止时不会发生注销事件，并且凭据/令牌仍然可以被捕获。

(我需要测试像 NetworkClearText 这样的其他登录情况。)

但是，如果用户属于“受保护用户安全组”或 **`TokenLeakDetectDelaySecs`** 非零，并且用户主动注销交互或远程交互(RDP)会话，则凭据将被清除。我需要对 Koh 进行编程，以便更好地处理这些特定类型的情况。

TL；DR 您应该为敏感用户使用“受保护用户安全组”,看看将`**TokenLeakDetectDelaySecs**`设置为 30 这样的值在您的环境中是否可行。

[Download](https://github.com/GhostPack/Koh)