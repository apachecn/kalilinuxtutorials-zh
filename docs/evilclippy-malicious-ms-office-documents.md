# EvilClippy:用于创建恶意的 MS Office 文档

> 原文：<https://kalilinuxtutorials.com/evilclippy-malicious-ms-office-documents/>

**EvilClippy** 是一款跨平台的助手，用于创建恶意的 MS Office 文档。可以隐藏 VBA 宏，践踏 VBA 代码(通过 P 代码)和混淆宏分析工具。

可以在 Linux、OSX 和 Windows 上运行。EvilClippy 工具是在我们的 black hat Asia talk(2019 年 3 月 28 日)期间发布的。一段录像将在 90 天后上线。

**邪恶的夹子**

用于创建恶意 MS Office 文档的跨平台助手。可以隐藏 VBA 宏，践踏 VBA 代码(通过 P 代码)和混淆宏分析工具。可以在 Linux、OSX 和 Windows 上运行。

**特性**

*   在 GUI 编辑器中隐藏 VBA 宏
*   VBA 跺脚(P 代码滥用)
*   傻瓜分析师工具
*   通过 HTTP 提供 VBA 模板
*   设置/删除 VBA 项目锁定/不可见保护

**这有多有效？**

在撰写本文时，该工具能够获得默认的 Cobalt Strike 宏，以绕过所有主要的防病毒产品和大多数 maldoc 分析工具(通过使用 VBA 跺脚结合随机模块名称)。

**技术**

Evil Clippy 使用 OpenMCDF 库来操作 MS Office 复合文件二进制格式(CFBF)文件，并在此滥用 MS-OVBA 规范和功能。

它重用了卡沃德的代码。VBA.Compression 实现在 dir 和模块流中使用的压缩算法(参见 MS-OVBA 的相关规范)。

Evil Clippy 与 Mono C#编译器配合得非常好，并且已经在 Linux、OSX 和 Windows 上测试过。

也可以阅读-[DrAFL:模糊 Linux 上没有源代码的二进制文件](https://kalilinuxtutorials.com/drafl-fuzzing-binaries-linux/)

**编译**

跨平台编译的二进制文件可以在“releases”下找到。

OSX 和 Linux 确保你已经安装了 Mono。然后从命令行执行以下命令:

mcs /reference:OpenMcdf.dll，System。IO.Compression.FileSystem.dll/out:evil clippy . exe *。铯

现在从命令行运行 Evil Clippy:

莫诺 EvilClippy.exe-h

Windows 请确保您安装了 Visual Studio。然后在 Visual Studio 开发人员命令提示符下执行以下命令:

**csc /reference:OpenMcdf.dll，System。IO.Compression.FileSystem.dll/out:evil clippy . exe *。cs**

现在从命令行运行 Evil Clippy:

EvilClippy.exe-h

**用法举例**

**打印帮助**

EvilClippy.exe h

**从 GUI 中隐藏宏**

在 VBA 图形用户界面编辑器中隐藏所有宏模块(除了默认的“ThisDocument”模块)。这是通过从项目流中删除模块行来实现的[MS-OVBA 2.3.1]。

**EvilClippy.exe-g 宏文件. doc**

**跺脚 VBA(虐 P 码)**

将文本文件 fakecode.vba 中的假 VBA 代码放到所有模块中，同时保持 P 代码不变。这滥用了模块流的一个未记录的特性[MS-OVBA 2.3.4.3]。请注意，VBA 项目版本必须与主机程序匹配，以便执行 P 代码(参见下一个版本匹配示例)。

**EvilClippy.exe-s fake code . VBA macro file . doc**

注意:VBA 跺脚对保存在 Excel 97-2003 工作簿中的文件无效。xls)格式

**为 VBA 跺脚设置目标 Office 版本**

同上，但现在明确针对 x86 上的 Word 2016。这意味着 x86 上的 Word 2016 将执行 P 代码，而其他版本的 Word 将改为执行 fakecode.vba 中的代码。通过在 _ VBA _ 项目流中设置适当的版本字节来实现[MS-OVBA 2.3.4.1]。

**EvilClippy.exe-s fake code . VBA-t 2016×86 宏文件. doc**

**设置随机模块名称(傻瓜分析师工具)**

在目录流中设置随机 ASCII 模块名称[MS-OVBA 2.3.4.2]。这滥用了 MODULESTREAMNAME 记录中的模糊性[MS-OVBA 2 . 3 . 4 . 2 . 3 . 2 . 3]–大多数分析工具使用这里指定的 ASCII 模块名称，而 MS Office 使用 Unicode 变体。

通过设置一个随机的 ASCII 模块名，大多数 P-code 和 VBA 分析工具崩溃，而实际的 P-code 和 VBA 在 Word 和 Excel 中仍然运行良好。

**EvilClippy.exe-r 宏文件. doc**

**注意:**这是已知的欺骗 pcodedmp 和 VirusTotal 的有效方法

**通过 HTTP 提供 VBA 踩踏模板**

执行 VBA 跺脚后，通过 HTTP 端口 8080 服务 macrofile.dot。如果检索到该文件，它会自动匹配目标的 Office 版本(使用其 HTTP 头，然后相应地设置 _ VBA _ 项目字节)。

**EvilClippy.exe-s fake code . VBA-w 8080 macro file . dot**

**注意:**您提供的文件必须是模板(。点而不是。doc)。您可以通过 URL(.不需要点扩展！)从 Word 的开发工具列。

此外，fakecode.vba 必须为模板中的宏设置 VB_Base 属性(这意味着您的 facecode.vba 必须以一行开头，如 Attribute VB _ Base = " 0 { 00020906-0000-0000-C000-00000000046 } ")。

**设置/移除 VBA 项目锁定/不可见保护**

**使用“-u”选项设置锁定/不可见属性:**

EvilClippy.exe 大学宏文件. doc

**使用'-uu '选项移除锁定/不可见属性:**

**EvilClippy.exe-uu 宏文件. doc**

注意:您也可以移除未使用 EvilClippy 锁定的文件的锁定/不可见属性。

**限制**

为 Microsoft Word 和 Excel 文档操作而开发。

如上所述，VBA 跺脚对 Excel 97-2003 工作簿无效。xls)格式。

演职员表:斯坦·海格特，凯莉·罗伯兹，尼克·兰德斯

[Download](https://github.com/outflanknl/EvilClippy)