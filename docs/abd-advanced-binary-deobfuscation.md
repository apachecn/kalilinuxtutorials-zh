# ABD:高级二进制去模糊课程材料

> 原文：<https://kalilinuxtutorials.com/abd-advanced-binary-deobfuscation/>

[![ABD : Course Materials For Advanced Binary Deobfuscation](img/0a8aa51629dd971c2a7c83fbceeeae09.png "ABD : Course Materials For Advanced Binary Deobfuscation")](https://1.bp.blogspot.com/-8wBFKeVPA_A/Xlgspae4hkI/AAAAAAAAFKI/LAUtNh095zQ6pfHW6fr70WvLSSh4z4lJACLcBGAsYHQ/s1600/Advanced%2BBinary%2BDeobfuscation.png)

ABD 是 NTT 安全平台实验室的高级二进制去模糊课程材料

**高级二进制去模糊**

这个资源库包含了 2020 年东京全球网络安全营[的高级二进制去模糊化的课程资料。](https://www.security-camp.or.jp/event/gcc_tokyo_program.html)

**课程摘要**

逆向工程并不容易，尤其是当二进制代码被混淆时。一旦执行了混淆，仅用简单的技术将无法准确地分析二进制文件。

在本课程中，您将学习混淆原理(尤其是被恶意软件使用的)、混淆代码分析的理论和实践，以及如何编写自己的去混淆工具。

特别是，我们深入研究数据流分析和基于 SAT/SMT 的二进制分析(例如，符号执行)，以使混淆无效。

**也读作-[DLL passwordfilterplant:具有渗透能力的 DLL 密码过滤器植入](https://kalilinuxtutorials.com/dllpasswordfilterimplant-dll-password-filter-implant-with-exfiltration-capabilities/)**

**概述**

本课程是关于二进制去模糊化的，面向希望在自己的工具库中添加一套技能的安全分析师和研究人员(处于胚胎期)。本课程结束时，学员将能够:

*   对模糊处理的理论、实践和背后的见解有深入的理解
*   使用最先进的打包程序构建自定义模糊负载
*   将编译器优化技术应用于二进制分析任务
*   设计并实现基于符号执行引擎的自动化二进制分析工具
*   甚至分析 APT 活动中使用的混淆恶意软件

为此，该课程在 GCC 以课堂学习和实践培训相结合的形式进行。

**必备知识**

与会者应具备:

*   x86/x64 体系结构中强大的技能组合
*   C/C++和 Python 的基本经验
*   对低级 CS(如操作系统、编译器、解释器、连接器和加载器)有基本的了解

以下链接有助于缩小差距。

*   [逆向工程 101](https://malwareunicorn.org/workshops/re101.html)
*   [rpi sec 的现代二进制开发](https://github.com/RPISEC/MBE)

**快速启动**

我们假设 Ubuntu 18.04 带 Miasm，Z3，Jupyter 笔记本。

1.  安装 [VirtualBox](https://www.virtualbox.org/wiki/Linux_Downloads)
2.  下载 [Ubuntu 18.04.3 镜像](https://sourceforge.net/projects/osboxes/files/v/vb/55-U-u/18.04/18.04.3/18.04.3VB-64bit.7z/download)并安装在 VirtualBox 中
3.  克隆此存储库
4.  执行`./setup.sh ./`
5.  安装 [IDA 免费软件](https://www.hex-rays.com/products/ida/support/download_freeware.shtml)
6.  阅读`Advanced-Binary-Deobfuscation.pdf`并享受！

[**Download**](https://github.com/malrev/ABD)