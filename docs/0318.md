# Invisi-Shell:隐藏 Powershell 脚本(绕过所有 Powershell 安全特性)

> 原文：<https://kalilinuxtutorials.com/invisi-shell-hide-powershell-script/>

Invisi-Shell 是一个用来隐藏 powershell 脚本的工具！Invisi-Shell 通过挂钩绕过了 Powershell 的所有安全特性(脚本块日志记录、模块日志记录、转录、AMSI)。Net 程序集。挂钩是通过 CLR 探查器 API 执行的。

## **隐形外壳用法**

*   将/x64/Release/文件夹中编译好的 InvisiShellProfiler.dll 与根目录(runwithpathasadmin . bat & runwitregistrynonadmin . bat)中的两个批处理文件复制到同一个文件夹中。
*   运行任一批处理文件(取决于您是否有本地管理员权限)
*   Powershell 控制台将运行。使用 Exit 命令(不要关闭窗口)退出 powershell，以允许批处理文件执行适当的清理。

**也读作 [强盗:查找容易发生 DLL 劫持的可执行文件的工具](https://kalilinuxtutorials.com/robber-dll-hijacking/)**

## **参考**

项目是用 Visual Studio 2013 创建的。您应该安装 Windows Platform SDK 来正确编译它。

## **视频教程**

[https://www.youtube.com/embed/Y3oMEiySxcc?feature=oembed](https://www.youtube.com/embed/Y3oMEiySxcc?feature=oembed)

## **免责声明**

这仍然是一个初步的概念验证版本。该代码只能在 x64 进程上运行，并针对 Powershell V5.1 进行了测试

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/OmerYa/Invisi-Shell) **贷方:CorProfiler by。NET 基金会，埃亚尔·内马尼，盖伊·弗兰科，伊弗雷姆·纽伯格，尤西·萨希&奥迈尔·耶尔**