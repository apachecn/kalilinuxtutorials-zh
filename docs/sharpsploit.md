# SharpSploit——用 C#编写的. NET 后期开发库

> 原文：<https://kalilinuxtutorials.com/sharpsploit/>

SharpSploit 是一个用 C#编写的. NET 后开发库，旨在突出。网，并利用进攻。对红队队员来说更容易。

它的命名部分是为了向 PowerSploit 项目致敬，这是我个人最喜欢的项目！虽然 SharpSploit 确实从 PowerSploit 移植了一些功能，但我的意图根本不是创建 PowerSploit 的直接移植。这将是它自己的项目，尽管目标与 PowerSploit 相似。

**也读作**[Vboxdie Cracker——虚拟盒磁盘镜像加密密码破解](https://kalilinuxtutorials.com/vboxdie-cracker-password-cracker/)

## **c#的 SharpSploit 上诉**

将现有的 PowerShell 工具集移植到 C#似乎是安全社区的一个发展趋势。SharpSploit 是这个谜团的另一部分。PowerShell 中添加的安全功能(即脚本块日志记录、AMSI 等。)，红队队员投资其他选项是有道理的。而 C#是 PowerShell 的下一步，因为它们都是基于。将工具集从 PowerShell 移植到 C#是相当容易的。

然而，从攻击性的角度来看，C#并不是没有自己的一套问题。看起来似乎光学。从运营商可用性的角度来看，从 PowerShell 这样的脚本语言迁移到 C#这样的编译语言，我们失去了相当多的灵活性。

我们也需要开始担心。NET 版本。你会发现。默认情况下，大多数 Windows 操作系统版本上都有. NET v3.5，但较新的 Windows 10 和 Server 2016 系统将只有。默认安装. NET v4.0+版本。另一个“问题”是。NET 在所有 Windows 操作系统版本上也不是默认启用的，您会发现它需要在 Windows Server 2008 和更早的服务器操作系统版本上显式启用。SharpSploit 试图通过定位来解决这个问题。NET v3.5 和 v4.0 来获得尽可能大的覆盖范围，但是您需要注意在正确的系统上使用正确的版本。

## **SharpSploit 控制台还是不控制台？**

到目前为止，SharpSploit 和大多数其他已经发布的攻击性 C#库之间最显著的区别就是没有`SharpSploit.exe`！SharpSploit 被设计成一个库，所以只有一个`SharpSploit.dll`。

我的意图是让 SharpSploit 主要用作一个库，供操作人员在他们自己的工具集中引用。然而，我预计这种实现会有一些限制，最终可能会迫使我添加一个基于控制台的界面。例如，Cobalt Strike 的`execute-assembly`模块期望一个应用程序有一个入口点(即“main”函数)来执行，所以 SharpSploit 目前不容易与 Cobalt Strike 一起操作。这是一个很好的例子，说明了在从 PowerShell 过渡到进攻型 C#时，我们必须解决的一些灵活性问题。

现在不要太担心这个，在不久的将来，你会从我这里看到一些其他创造性的 SharpSploit 执行方法🙂我可能会在某个时候添加一篇后续文章，介绍执行 SharpSploit 函数的方便方法。

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/cobbr/SharpSploit)