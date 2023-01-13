# Lupo:恶意软件 IOC 提取器。用于恶意软件分析自动化的调试模块

> 原文：<https://kalilinuxtutorials.com/lupo/>

[![](img/14b881d58e9f7300d2dc28c45327b75d.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiN0WHChLdc_H7F7AftVigdboHKbM2VKbNyxb-nmsaZnshywORx9HWl_PKJkmgLUKC3ikq8RNC_zYA8Clo9ynYUQ-ZNpYBlpgzI12xmwfJhg9tVtyEkEXlwQKPqA5whxLcme-8874eFnUxj4ZCumMaUEQZST18LlEXxS8UQ2zTTuwPDHj0nrG3S0Nli/s728/1_IywwocerMkLQiw5xohFglg%20(1).png)

Lupo 是一个用于恶意软件分析自动化的调试模块。

在处理涉及恶意软件的安全事件时，我们经常会遇到这样的情况，我们觉得有必要自动执行部分分析流程，因为由于许多因素(时间、技能、规模等),完全的手动分析通常无法适用于所有情况。).

我写 Lupo 主要是为了尽可能地自动化和加速这个过程。Lupo 是一个动态分析工具，可以作为一个模块与调试器一起使用。第一个版本使用流行的 Windows 调试器 WinDbg。将来我会为其他调试器发布版本。

该工具的工作方式非常简单。您将 Lupo 加载到调试器中，然后执行它。它运行恶意软件，收集预定义的 IOC，并将其写入磁盘上的文本文件。然后，您可以使用这些信息来遏制和消除恶意软件活动，或者简单地响应您正在处理的安全事件。

## lupo——工具

我将给出更多关于工具本身的细节，但不会太多关于它的内部工作原理，至少在这里不会。我们需要记住，恶意软件的作者足够聪明，可以快速修改代码来给我们制造问题！

该工具是用 C++编写的，使用 Windows 调试框架来执行代码。它可以作为“插件”与 WinDbg 一起使用，以帮助自动化分析过程。

如果你想了解更多关于这个工具的信息，欢迎联系我或者在下面评论。

## 下载

从这个 repo 下载所有的 dll。您还需要所有的 VC++依赖项，最简单的方法是安装 Visual Studio(Community version works)并选择所有的 C++组件。

## 用法

使用这个工具非常容易。它是这样工作的:

将 Lupo 扩展保存在您的扩展目录中(默认:安装目录的 sdk\samples\exts 子目录)。您也可以使用命令'来定义扩展路径。ext path[+][目录[；…]]'.

启动调试器

附加要调试的进程(本例中是恶意软件)

使用加载 Lupo。“加载”命令。

使用以下命令执行 Lupo:“Lupo . go”

所有结果都将显示在控制台中，并写入磁盘上的新文本文件中。此文本文件的路径和名称也将显示在控制台中。全部完成！

你可以选择使用 Lupo 的结果和我写的另一个工具——Ragno，通过为你可能正在处理的活动的更广泛的足迹聚集 OSINT 来推进你的研究和响应。你可以在这里的另一个帖子中阅读关于 Ragno 的内容:https://medium . com/@ vishal _ tha kur/introducing-Ragno-IOC-multiplier-9b 75834353 bb

[Download](https://github.com/malienist/lupo)