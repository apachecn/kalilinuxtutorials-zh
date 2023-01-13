# FridaExtract:基于 Frida.re 的 RunPE 提取工具

> 原文：<https://kalilinuxtutorials.com/fridaextract/>

FridaExtract 是一个基于 [RunPE](http://www.adlice.com/runpe-hide-code-behind-legit-process/) 的 [Frida.re](http://www.frida.re/) 提取工具。RunPE 类型注入是恶意软件用来在另一个进程中隐藏代码的常用技术。这也是很多包装工的最后阶段: )

注意:Frida 现在也支持使用这里描述的“MapViewOfSection”技术提取注入的 PE 文件。

使用 FridaExtract，你可以自动提取并重建一个使用 RunPE 方法注入的 PE 文件…并绕过这些打包程序！

**为什么是弗里达？**

有很多很棒的工具已经提取了 RunPE 注入代码，FridaExtract 比这些好不了多少。但是更容易安装，更容易构建(lol)，更容易运行，更容易被黑。没有编译器，没有构建环境，只需简单的“pip 安装”,您就可以开始运行了。

代码经过特别的注释和组织，作为你构建自己的 Frida 项目的模板。这更像是一个概念验证，演示了如何在 Windows 环境中设置挂钩。请用你喜欢的任何方式复制-粘贴-黑掉它！

**也读-[Xori:一个自动化就绪的反汇编&静态分析库](https://kalilinuxtutorials.com/xori/)**

**入门**

**警告:** FridaExtract 只在 Windows 32bit 下工作。wow64 目前有一些神秘的错误，所以我们建议坚持使用 Windows 7 32 位或 Windows Server 2008 32 位。

*   如果你要解压恶意软件，首先启动一个虚拟机(见上面的警告)。
*   安装 [Python 2.7](https://www.python.org/downloads/)
*   记得[设置你的 python 和 pip 路径](http://docs.python-guide.org/en/latest/starting/install/win/)；)
*   通过在 cmd 中键入`pip install frida`来安装 Frida
*   克隆这个库，您就可以开始解压了！

**提取 PE 文件**

FridaExtract 只能提取 RunPE 注入的 PE 文件，所以它相当有限。如果你使用的是易于快照-运行-恢复的虚拟机，那么你可以在每个恶意软件样本上盲目地尝试 FridaExtract，看看会出现什么，但我们不建议这样做。相反，FridaExtract 是对沙盒的很好的补充(we <3  [malwr](https://malwr.com/) )。首先在沙箱中运行示例，注意 API 调用。

对于 RunPE 技术，如果您看到以下 API 调用，那么 FridaExtract 可能是您的工具:

*   创建流程
*   WriteVirtualMemory(到远程进程)
*   ResumeThread(在远程进程中)

对于 MapViewOfSection 技术，如果您看到以下 API 调用，那么 FridaExtract 可能是您需要的工具:

*   创建流程
*   NtCreateSection
*   NtUnmapViewOfSection(远程进程)
*   NtMapViewOfSection(远程进程)

**例题**

默认情况下，FridaExtract 将尝试自动提取注入的 PE 文件，重新构建它，并将其转储到一个名为 dump.bin 的文件中。

**python Frida extract . py bad.exe**

**转储到文件**

可以使用–out _ file 命令指定转储文件。

**python Frida extract . py bad.exe–out _ file extracted.exe**

**传递参数**

如果您试图提取的打包 PE 文件需要参数，您可以使用–args 命令传递它们。多个参数可以以逗号分隔的形式传递。

**python Friday xtract . py bad . exe–args 密码**

**转储原始数据**

FridaExtract 将自动尝试将转储的内存重建到 PE 文件中。

如果这不起作用，并且您只想将所有内存的原始转储写入子进程，那么您可以使用–raw 命令。原始内存段将按地址顺序写入，而不是将重建的 PE 写入转储文件。

**python Friday xtract . py bad . exe–raw**

**啰嗦**

FridaExtract 使用以下 API 上的钩子来提取注入的 PE 文件:

*   出口流程
*   NtWriteVirtualMemory
*   NtCreateThread
*   NtResumeThread
*   NtDelayExecution
*   CreateProcessInternalW
*   NtMapViewOfSection
*   NtUnmapViewOfSection
*   NtCreateSection

要跟踪这些 API 并打印结果，使用`-v`或`--verbose`命令。

**python Frida extract . py bad.exe–详细**

[**Download**](https://github.com/OALabs/frida-extract)