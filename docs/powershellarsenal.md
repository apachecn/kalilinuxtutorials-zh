# PowerShellArsenal:专门用于逆向工程的 PowerShell 模块

> 原文：<https://kalilinuxtutorials.com/powershellarsenal/>

PowerShellArsenal 是一个用于帮助逆向工程的 PowerShell 模块。该模块可用于反汇编托管和非托管代码，执行。NET 恶意软件分析，分析/抓取内存，解析文件格式和内存结构，获取内部系统信息等。powershell 阿森纳由以下工具组成:

**拆卸**

反汇编本机代码和托管代码。

**Get-CSDisassembly**

使用顶点引擎反汇编框架反汇编一个字节数组。

**获取-ILDisassembly**

以类似于 Ildasm 的方式反汇编从 MethodInfo 对象传入的原始 MSIL 字节数组。

**也可阅读—[PenTest 的 5 大 SQL 注入工具&黑客](https://kalilinuxtutorials.com/top-5-sql-injection-tools-for-pentest-hacking/)**

**恶意软件分析**

执行恶意软件分析时的有用工具

**新功能委托**

为 X86 或 X86_64 函数提供可执行包装。

调用-加载库

将 DLL 加载到当前 PowerShell 进程中

New-DllExportFunction

围绕非托管导出函数创建可执行包装委托

Get-HostsFile

解析主机文件。

新主机文件条目

将条目替换或附加到主机文件。

Remove-HostsFileEntry

从主机文件中删除一个条目或一系列条目

get-assembly string

输出. NET 可执行文件中的所有字符串。

Get-AssemblyResources

从. NET 程序集中提取托管资源

remove-assemblysuppressildassmartibute

从. NET 程序集中剥离 SuppressIldasmAttribute 属性

get-assemblyimpllemonedmethods

返回程序集中在 MSIL 实现的所有方法。

**内存工具**

检查和分析进程内存

get-process 字符串

从进程的用户模式内存中输出所有可打印的字符串。

Get-VirtualMemoryInfo

kernel32 的包装！虚拟查询

Get-ProcessMemoryInfo

检索用户内存中每个唯一页面集的虚拟内存信息。这个函数类似于！vadump WinDbg 命令

get-structfromemory

将数据从任意进程中的非托管内存块封送到新分配的指定类型的托管对象。

**解析器**

解析文件格式和内存结构

Get-PE

磁盘上和内存中的 PE 解析器和进程转储器

查找流程

在内存中查找可移植的可执行文件，不管它们是否以合法的方式加载

Get-LibSymbols

显示 Windows LIB 文件中的符号信息

Get-ObjDump

显示有关 Windows 对象(OBJ)文件的信息。

**窗户内部**

获取和分析低级 Windows 操作系统信息。

Get-NtSystemInformation

一个调用和解析 ntdll 输出的实用程序！NtQuerySystemInformation 函数。该实用程序可用于查询通常对用户不可见的内部操作系统信息。

去 PEB

返回进程的进程环境块(PEB)。

寄存器-进程模块跟踪

开始跟踪加载的进程模块

Get-ProcessModuleTrace

显示自调用 Register-ProcessModuleTrace 以来已加载的进程模块

取消注册-ProcessModuleTrace

停止正在运行的进程模块跟踪

获取系统信息

kernel32 的包装！GetSystemInfo

**杂项**

杂项助手功能

获取成员

用于扩展内置 Get-Member cmdlet 的代理函数。它添加了'-Private '参数，允许您显示非公共的。网络成员

获取字符串

转储 Unicode 和 Ascii 文件中的字符串。这个 cmdlet 从 Sysinternals 复制了 strings.exe 的功能。

转换成字符串

将文件的字节转换为字符串，该字符串与文件的原始字节具有一对一的映射关系。ConvertTo-String 对于执行二进制正则表达式很有用。

获取熵

计算文件或字节数组的熵。

**Lib**

一些 RE 函数所需的库。

顶点

顶石拆卸引擎 C#绑定。

De4dot

一个强大的。净去泡沫和。NET PE 解析库。

PSReflect

用于轻松定义内存中枚举、结构和 Win32 函数的模块。

格式化程序

ps1xml 文件用于格式化各种 PowerShellArsenal 函数的输出。

**执照**

除非另有明确说明，否则 PowerShellArsenal 模块和所有单独的脚本都受 BSD 3 条款许可证的约束。

**用途**

有关详细的用法信息，请参考每个脚本中基于注释的帮助。

要安装此模块，请将整个 PowerShellArsenal 文件夹放入其中一个模块目录中。默认的 PowerShell 模块路径在$Env:PSModulePath 环境变量中列出。

默认的每用户模块路径是:**" $ Env:home drive $ Env:home path \ Documents \ windows powershell \ Modules "**默认的计算机级模块路径是:**" $ Env:windir \ System32 \ windows powershell \ v 1.0 \ Modules "**

要使用该模块，请键入 Import-Module PowerShellArsenal

要查看导入的命令，请键入**Get-Command-Module powershell arsenal**

如果您运行的是 PowerShell v3，并且希望消除恼人的“您真的想运行从互联网下载的脚本吗”警告，那么一旦您将 PowerShellArsenal 放入您的模块路径中，运行下面的一行程序: **$Env:PSModulePath。拆分('；')| % { if(Test-Path(Join-Path $ _ powershell arsenal)){ Get-child item $ _-Recurse | Unblock-File } }**

对于每个单独命令的帮助，Get-Help 是您的好朋友。

**注意:**本模块中包含的工具都被设计为可以单独运行。将它们包含在一个模块中只是增加了可移植性。

**脚本风格指南**

对于 PowerShellArsenal 的所有贡献者和未来的贡献者，我要求你们在编写脚本/模块时遵循这个风格指南。

*   不惜一切代价避免写主机。PowerShell 函数/cmdlet 不是命令行实用程序！将不考虑包含使用写主机的代码的拉请求。您应该输出自定义对象。有关创建自定义对象的更多信息，请阅读以下文章:
    *   http://blogs.technet.com/b/heyscriptingguy/archive/2011/05/19/create-custom-objects-in-your-powershell-script.aspx
    *   http://technet.microsoft.com/en-us/library/ff730946.aspx
*   如果您想在屏幕上显示相关的调试信息，请使用 Write-Verbose。用户总是可以加上“-Verbose”。
*   始终为每个脚本提供描述性的、基于注释的帮助。此外，一定要包括你的名字和 BSD 3 条款许可证(除非有情有可原的情况阻止 BSD 许可证的应用)。
*   确保所有函数都遵循正确的 PowerShell 动词-名词协议。使用 Get-Verb 列出 PowerShell 使用的默认动词。受支持动词的例外将根据具体情况考虑。
*   我更喜欢变量名大写，并且尽可能的描述性。
*   在代码之间提供逻辑间距。缩进你的代码，使其可读性更好。
*   如果你发现自己在重复代码，写一个函数。
*   捕捉所有预期的错误并提供有意义的输出。如果您遇到了应该停止脚本执行的错误，请使用“Throw”。如果你有一个不需要停止执行的错误，使用 Write-Error。
*   如果您正在编写与 Win32 API 交互的脚本，请尽量避免使用 Add-Type 内联编译 C#。如果可能，请尝试使用 PSReflect 模块。
*   不要使用硬编码的路径。脚本应该开箱即用。任何人都不应该修改代码，除非他们想这样做。
*   PowerShell v2 兼容性是非常需要的。
*   使用位置参数，并在有意义时强制使用参数。例如，我正在寻找类似以下的东西:
    *   [参数(Position = 0，Mandatory = $True)]
*   除非别名对接收管道输入有意义，否则不要使用别名。对于不熟悉特定别名的人来说，它们使得代码更难阅读。
*   尽量不要让命令运行太长时间。例如，管道是换行的自然位置。
*   不要过分使用行内注释。只有当代码的某些方面可能会让读者感到困惑时，才使用它们。
*   与其使用 Out-Null 来抑制不需要的/不相关的输出，不如将不需要的输出保存到$null。这样做可以稍微提高性能。
*   当有意义时，使用参数的默认值。理想情况下，您需要一个不需要任何参数就能工作的脚本。
*   在基于注释的帮助中为您的函数显式声明所有必需的和可选的依赖项。所有库依赖项都应该位于“Lib”文件夹中。
*   如果脚本创建复杂的自定义对象，请包含一个 ps1xml 文件，该文件将正确格式化对象的输出。ps1xml 文件存储在 Lib\Formatters 中。

[**Download**](https://github.com/mattifestation/PowerShellArsenal)