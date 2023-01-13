# Flare-Qdb:用于检测和修改本机软件的命令行和 Python 调试器

> 原文：<https://kalilinuxtutorials.com/flare-qdb/>

[![](img/3d363ddbdda3693a970e9e0e80e166b4.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgdRiNhqVTWoeyu46YC70DIlN0k8newWx8Zd7_BWzJAka-yRJmjznPY6tNHFkHHO7M1zNiPlym5D5xZBzlIx-OcMoBbhTMOFw9f8Wku4s7IlQj8ALAhm18Zlx6-hTpmzgmnPzJOxZcYQ-Z5ooLPxrEPakDbRSbquEKxW122HJW1Kv_3k47XvnmVbnM5/s730/images.png)

Flare-qdb 是一个基于 Python 的命令行和脚本化工具，用于评估和操作本机程序状态。它使用 Vivisect 在每个查询的指令上设置断点，并在命中时执行 Python 代码。

flare-qdb 解放了分析人员，使他们能够采用非线性方法进行动态分析，从而解决正常调试和静态分析过程中出现的问题。flare-qdb 回答了这些问题，不需要分析师手动设置交互式调试器会话并将程序计数器导航到该代码位置。

以下是 flare-qdb 可以回答的一些现场问题示例:

*   eax 在这一点上总是等于这个值吗？
*   eax 在这个分支之前等于什么？
*   在这个循环中，这个字符串会取什么值？
*   在内循环的*第一次*迭代时，用的是什么基址？
*   这个程序会符合这个逻辑吗？
*   哪个代码先执行？
*   循环迭代次数是否取决于`**argv[1]**`的值？
*   我可以改变命令行参数来避免这种情况吗？

flare-qdb 还可用于促进程序执行的自动化、可重复操作。以下是一些有用的应用示例:

*   执行具有不同参数的字符串解码器，以快速提取恶意软件样本使用的所有字符串。
*   覆盖参数到`**Sleep()**`以允许快速迭代测试一个定制的命令和控制(C2)服务器。
*   告知权限提升工具其完整性级别为 0x1000 ( `**MANDATORY_LOW_RID**`)，以诱使其执行其漏洞利用代码。
*   可重复地自动打开跳转到一个或多个非确定性堆位置的打包器。

flare-qdb 接受多个查询，这些查询采用程序计数器或 Vivisect 表达式的形式，并与一些 Python 文本配对，以便在 flare-qdb 脚本环境中进行评估。Vivisect 表达式可用于指定简单的常量程序计数器值，如`**"0x401000"**`，符号表达式，如`**"kernel32.Sleep"**`，等等。活体解剖表达式也可以结合寄存器和内存状态来表达复杂的条件，如`**"not eax or** (**( edx > 3) and (poi(ebp-8) < 5))"**`。

此命令的命令行参数格式为:

**-at<vexpr-PC><python text**>

flare-qdb 还支持基于活体解剖表达式的真值的条件评估:

**-at-if<vexpr-PC><vexpr-conds><python text**>

lare-qdb 为方便调试提供了几个内置函数，它们既可以从命令行获得，也可以作为其`**Qdb**`类的方法获得。

flare-qdb 主要在 Windows 上进行了测试，但也适用于 Linux。遗憾的是，Vivisect 的`**vtrace.Trace**`类的 Darwin 端口不完整，所以 flare-qdb 不支持 OSX。

## 示例脚本

flare-qdb 附带了 De-DOSfuscator，这是一个通过运行模糊批处理文件来解码它们的工具。详细信息可以在 De-DOSfuscator 指南中找到，也可以通过阅读博客 Cmd and Conquer:De-DOSfuscation with flare-qdb 找到。

[**Download**](https://github.com/mandiant/flare-qdb)