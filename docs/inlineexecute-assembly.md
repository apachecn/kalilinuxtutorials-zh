# InlineExecute-Assembly:一个 PoC 信标对象文件(BOF ),允许安全专业人员在进程中执行。NET 程序集执行

> 原文：<https://kalilinuxtutorials.com/inlineexecute-assembly/>

[![](img/3e551797c012effb62376a14d5cef819.png)](https://1.bp.blogspot.com/-vUizfLEGHE0/YUsEeIfoYvI/AAAAAAAAK6Q/VR8TfM2QM50f1GargZIsbblgrmL9DpeiwCLcBGAsYHQ/s728/10590865%2B%25281%2529.png)

**InlineExecute-Assembly** 是一个概念证明信标对象文件(BOF)，允许安全专业人员在进程中执行。NET assembly execution 作为 Cobalt 的替代方案打击了传统的 fork 并运行 execute-assembly 模块。InlineExecute-Assembly 将执行任何入口点为`**Main(string[] args)**`或`**Main()**`的程序集。这应该允许您运行大多数发布的工具，而不需要任何预先的修改。

BOF 将在执行之前自动确定需要将哪个公共语言运行时(CLR)加载到您的程序集的进程中(v2.0.50727 或 v4.0.30319 ),并且在大多数情况下，如果出现任何问题，应该会正常存在。BOF 还支持几个标志，允许操作员在之前指定几个行为。NET 执行，包括通过内存修补禁用 AMSI，通过内存修补禁用和恢复 ETW，自定义要创建的 CLR 应用程序域名，是否创建程序集的控制台输出并将其定向到命名管道或邮件槽，以及允许操作员将 main(string[] args)的默认入口点切换到 Main()。有关用法、用例以及可能的检测的更多详细信息，请参见以下内容和 https://security intelligence . com/posts/net-execution-inline execute-assembly/。

最后，执行我们的。我们避免了 Cobalt Strike 的 execute-assembly 模块的默认行为，它创建了一个新的进程来加载/注入 CLR/NET 程序集。但是，其他 opsec 注意事项仍然存在，例如，我们正在其中执行的进程是否正常加载 CLR，或者。NET 程序集有任何已知的签名吗？因此，缺点是如果某些东西被检测到并被杀死，例如被 AMSI，你的信标也会被杀死。

**入门**

*   将 inlineExecute-Assembly 文件夹及其所有内容复制到您计划通过 Cobalt Strike GUI 应用程序连接的系统中。
*   加载 inlineExecute-Assembly.cna 攻击者脚本
*   运行 inline execute-Assembly–dotnet Assembly/path/to/Assembly . exe 进行最基本的执行(具体标志示例见下面的用例)

**打造自己的**

通过 VS 2019 的 x64 原生工具命令提示符在 src 目录中运行以下命令

**cl.exe/c inline execute-assembly . c/GS-/foinline execute-assembly x64 . o**

通过 VS 2019 的 x86 本机工具命令提示符在 src 目录中运行以下命令

**cl.exe/c inline execute-assembly . c/GS-/foinline execute-assembly x86 . o**

**标志**

**–所需程序集的 dotnetassembly 目录路径
–Assembly args 要传递的程序集参数
–appdomain 更改发送的 AppDomain 的默认名称(默认值为 totesLegit，通过包含的攻击者脚本设置)*域始终卸载*
–amsi 尝试通过内存修补禁用 amsi(如果成功，AMSI 将在整个进程生命周期内被禁用)
–etw 尝试通过内存修补禁用 etw(如果成功，除非恢复，否则 ETW 将在进程的整个生命周期内被禁用)
–revertetw 尝试通过内存修补禁用 ETW，然后将其重新修补回原始状态
–管道更改命名管道的默认名称(默认值为 totesLegit，并通过包含的攻击者脚本设置)
–邮件槽切换到使用邮件槽来重定向控制台输出。 更改邮件槽的默认名称(如果留空，默认值为 totesLegit 并通过包含的攻击者脚本设置)
–main 将入口点更改为 Main()(默认值为 Main(string[] args))**

**用例**

*执行。净装配*

**语法**

**beacon>inline execute-Assembly–dotnet Assembly/root/Desktop/seat belt . exe**

**用例**

*执行。带参数的. NET 程序集*

**语法**

**beacon>inline execute-Assembly–dotnet Assembly/root/Desktop/season . exe–Assembly args anti virus app locker**

**用例**

*执行。带参数的. NET 程序集并禁用 AMSI*

**语法**

**beacon>inline execute-Assembly–dotnet Assembly/root/Desktop/season . exe–Assembly args anti virus app locker–amsi**

**用例**

*执行。带参数的. NET 程序集并禁用 ETW*

**语法**

**beacon>inline execute-Assembly–dotnet Assembly/root/Desktop/season . exe–Assembly args anti virus app locker****–etw**

**用例**

*执行。NET 程序集，并通过邮件槽而不是默认的命名管道*重定向输出

**语法**

**beacon>inline execute-Assembly–dotnet Assembly/root/Desktop/season . exe–mailslot**

**用例**

*执行。NET 程序集，并更改攻击者脚本中设置的默认命名管道名称*

**语法**

**beacon>inline execute-Assembly–dotnet Assembly/root/Desktop/season . exe–pipe for real legit**

**用例**

*执行。NET 程序集并更改攻击者脚本中设置的默认应用程序域*

**语法**

**beacon>inline execute-Assembly–dotnet Assembly/root/Desktop/season . exe–appdomain for real legit**

**用例**

*执行。NET 程序集用 Main()入口点代替默认的 Main(string[] args)*

**语法**

**beacon>inline execute-Assembly–dotnet Assembly/root/Desktop/simple main . exe–main**

**用例**

*去火腿*

**语法**

**beacon>inline execute-Assembly–dotnet Assembly/root/Desktop/seat belt . exe–Assembly args anti virus app locker–amsi–etw–appdomain for real legit–mail slot for real legit**

**注意事项**

*   虽然我已经尽可能地使它稳定，但不能保证事情永远不会崩溃，信标不会消失。我们没有额外的奢侈，如果出了问题，我们的灯塔就在那里。这是与 BOFs 的权衡。也就是说，我不能强调预先测试您的程序集以确保它们能够与工具一起正常工作的重要性。
*   由于 BOF 是在进程中执行的，并且在运行时接管信标，因此在用于长时间运行的程序集之前，应该考虑到这一点。如果您选择运行需要很长时间才能返回结果的程序，那么在结果返回并且您的程序集完成运行之前，您的信标不会被激活来运行更多的命令。这也不符合睡眠设定。例如，如果您的睡眠时间设置为 10 分钟，并且您运行 BOF，那么只要 BOF 完成执行，您就会得到结果。
*   除非对在内存中加载 PE 的工具进行修改(例如，SafetyKatz)，否则这些工具很可能会杀死您的信标。这些工具中的许多都可以很好地使用 execute assembly，因为它们能够在退出之前从牺牲性进程发送控制台输出。当它们通过我们的进程内 BOF 退出时，它们杀死了我们的进程，从而杀死了我们的信标。这些可以被修改来工作，但是我建议通过 execute assembly 运行这些类型的程序集，因为其他非 OPSEC 友好的东西可能会被加载到您的进程中而不会被删除。
*   如果您的程序集使用环境。退出这将需要删除，因为它会杀死进程和信标。
*   命名管道和邮件插槽需要唯一。如果您没有收到返回的数据，而您的信标仍然存在，问题很可能是您需要选择一个不同的命名管道或邮件插槽名称。

**探测**

可以使用的一些检测和缓解策略:

*   在执行 AMSI 和 ETW 内存修补时，使用 PAGE_EXECUTE_READWRITE。这是故意的，应该是一个危险信号，因为很少有程序的内存范围具有 PAGE_EXECUTE_READWRITE 的内存保护。
*   创建的命名管道的默认名称是 totesLegit。这是故意这样做的，并且可以使用签名检测来对此进行标记。
*   创建的邮件槽的默认名称是 totesLegit。这是故意这样做的，并且可以使用签名检测来对此进行标记。
*   加载的 AppDomain 的默认名称是 totesLegit。这是故意这样做的，并且可以使用签名检测来对此进行标记。
*   检测恶意使用。NET (by @bohops)这里，(by F-Secure)这里，还有这里
*   寻找。NET CLR 加载到可疑的进程中，例如不应该加载 CLR 的非托管进程。
*   此处的事件跟踪
*   寻找其他已知的钴罢工信标国际奥委会或 C2 出口/通信国际奥委会。

[**Download**](https://github.com/anthemtotheego/InlineExecute-Assembly)