# ZipExec:从受密码保护的 Zip 文件中执行二进制文件的独特技术

> 原文：<https://kalilinuxtutorials.com/zipexec/>

[![](img/0cca061b9c7072529a4f1970147e872e.png)](https://blogger.googleusercontent.com/img/a/AVvXsEg_96lH6nOYw0JFWLukiWXp_4kFJi5jErFd-Xp1lUARCGhRrqX7ozd6dgsD8GQ9uAyaIWK_0YcP16YOjomQlLgpc2XnrC35YFS0L-sdjbBo9ZXxQJQb33-UUOCHD7IsMyxgczKHqHzSpLlqH_Yk23KzK1dpVvmWJ-P4ya8BqDlDtBLX-VJIkntk9_AU=s728)

ZipExec 是一个概念验证(POC)工具，它将基于二进制的工具打包成一个受密码保护的 zip 文件。然后，这个 zip 文件被 base64 编码成一个字符串，并在磁盘上重建。然后，该编码字符串被加载到一个 JScript 文件中，当执行该文件时，将在磁盘上重新生成受密码保护的 zip 文件并执行它。这是通过使用 COM 对象经由生成的 JScript 加载程序来访问 Windows 中基于 GUI 的函数，在受密码保护的 zip 中执行加载程序，而不必先将其解压缩，以编程方式完成的。通过密码保护 zip 文件，它可以保护二进制文件免受 EDRs 和基于磁盘或反恶意软件扫描机制的攻击。

**安装**

一如既往，第一步是克隆回购协议。在编译 ZipExec 之前，您需要安装依赖项。要安装它们，请运行以下命令:

去找 github.com/yeka/zip

那就建造它

**去构建 ZipExec.go**

或者

去找 github.com/Tylous/ZipExec

**帮助**

**。/ZipExec -h
**_* 。*
_ _ _ _ _ _ _/|*_*/_*/_
//| _*|)*\ \///_/*\//*|*|>|>><\*/\ _*
/*| _*|/*/_*>>/ZipExec:
-I string
包含二进制到 zip 的文件的路径。
-O string
输出文件名称(如 loader . js)
-沙盒
使用 IsDomainedJoined 启用沙盒规避。**

[Download](https://github.com/Tylous/ZipExec)