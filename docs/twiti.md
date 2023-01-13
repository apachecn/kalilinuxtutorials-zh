# TwiTi:从 tweet 中提取 IOC 的工具

> 原文：<https://kalilinuxtutorials.com/twiti/>

[![Linux Smart Enumeration : Tool For Pentesting & CTFs With Verbosity Levels](img/a32e6904ba81b9895fb31a6589fd8d09.png "Linux Smart Enumeration : Tool For Pentesting & CTFs With Verbosity Levels")](https://1.bp.blogspot.com/-AE3FJuZnWZM/XSUbQ4N46nI/AAAAAAAABSQ/TQSDFUOFZ0Y5wzWN8UdLnpQncrTUUMh3wCLcBGAs/s1600/demo-1.gif)

**TwiTi** ，一个从推文中提取 IOC 的工具，可以收集到大量新鲜、准确的 IOC。
TwiTi 确实如此

*   对一条推文是否包含 IOC 进行分类。
*   从 tweet 和 tweet 中提到的链接中提取 IOC。

有关更多详细信息，请参考我们的论文
“# Twiti:威胁情报的社交监听”(TheWebConf 2021)
另外，您可以在数据目录中找到论文的补充材料。

**要求**

**Python**

**pip install-r requirements . txt**

**Python 3.7.0**

Python 3.7.0 是 Python 3.7 最初的 ***特性发布*** 。

**注**

现在，Python 3.7 的**个更新的 bugfix 版本**取代了 3.7.0，Python 3.8 现在是 Python 3 的**最新特性版本**。在此获取 3.7.x 和 3.8.x 的最新版本。我们计划在 2020 年年中之前继续为 3.7.x 提供*错误修复版本*，在 2023 年年中之前继续提供*安全修复版本*。

Python 3.7 的主要新特性包括:

*   PEP 539，用于线程本地存储的新 C API
*   PEP 545，Python 文档翻译
*   新文档翻译:日语、法语和韩语。
*   PEP 552，确定性 pyc 文件
*   PEP 553，内置断点()
*   PEP 557，数据类别
*   PEP 560，对类型模块和泛型类型的核心支持
*   PEP 562，访问模块属性的定制
*   PEP 563，注释的延期评估
*   PEP 564，具有纳秒分辨率的时间函数
*   PEP 565，改进了弃用警告处理
*   PEP 567，上下文变量
*   避免使用 ASCII 作为默认的文本编码(PEP 538，传统 C 语言环境强制和 PEP 540，强制 UTF-8 运行时模式)
*   dict 对象的插入顺序保持特性现在是 Python 语言规范的正式部分。
*   许多领域的显著性能改进。

有关更多信息，请参见 Python 3.7 中的新特性。

**更多资源**

*   在线文档
*   PEP 537，3.7 发布时间表
*   报告 https://bugs.python.org 的漏洞。
*   帮助资助 Python 及其社区。

**Windows 用户**

*   AMD64 的二进制文件也可以在采用英特尔 64 架构的处理器上运行。(也称为“x64”体系结构，以前称为“EM64T”和“x86-64”。)
*   现在有“基于网络”的 Windows 平台安装程序；安装程序将在安装时下载所需的软件组件。
*   有包含 Windows 构建的可再发行的 zip 文件，使得将 Python 作为另一个软件包的一部分再发行变得容易。有关更多信息，请参见关于嵌入式分发的文档。

**macOS 用户**

*   对于 3.7.0，我们提供了两个二进制安装程序选项供下载。默认版本是 64 位版本，适用于 macOS 10.9 (Mavericks)和更高版本的系统。我们还继续提供 64 位/32 位版本，适用于从 10.6(雪豹)开始的所有 macOS 版本。这两种变体现在都带有电池版的 Tcl/Tk 8.6，供空闲用户和其他基于 tkinter 的 GUI 应用程序使用；不再使用 Tcl/Tk 的第三方和系统版本。考虑使用新的 10.9 64 位安装程序变体，除非您正在构建也需要在旧的 macOS 系统上工作的 Python 应用程序。
*   两个 python.org 安装程序变体都包含 OpenSSL 1.1.0 的私有副本。有关 SSL/TLS 证书验证和 Install Certificates.command 的信息，请仔细阅读安装过程中显示的重要信息

完整变更日志

**文件**

| 版本 | 操作系统 | 描述 | MD5 总和 | 文件大小 | 每加仑格令数(Grains Per Gallon) |
| --- | --- | --- | --- | --- | --- |
| [g 压缩源文件 tarball](https://www.python.org/ftp/python/3.7.0/Python-3.7.0.tgz) | 源发布 |  | 41b 6595 deb 4147 a1 ed 517 a7d 9 a 580271 | Twenty-two million seven hundred and forty-five thousand seven hundred and twenty-six | [自己](https://www.python.org/ftp/python/3.7.0/Python-3.7.0.tgz.asc) |
| [XZ 压缩源 tarball](https://www.python.org/ftp/python/3.7.0/Python-3.7.0.tar.xz) | 源发布 |  | EB 8 C2 a6b 1447d 50813 c 02714 af 4681 f 3 | Sixteen million nine hundred and twenty-two thousand one hundred | [自己](https://www.python.org/ftp/python/3.7.0/Python-3.7.0.tar.xz.asc) |
| [macOS 64 位/32 位安装程序](https://www.python.org/ftp/python/3.7.0/python-3.7.0-macosx10.6.pkg) | 马科斯 | 适用于 Mac OS X 10.6 及更高版本 | ca 3eb 84092d 0 ff 6d 02 e 42 f 63 a 734338 e | Thirty-four million two hundred and seventy-four thousand four hundred and eighty-one | [自己](https://www.python.org/ftp/python/3.7.0/python-3.7.0-macosx10.6.pkg.asc) |
| [macOS 64 位安装程序](https://www.python.org/ftp/python/3.7.0/python-3.7.0-macosx10.9.pkg) | 马科斯 | 对于 OS X 10.9 及更高版本 | AE 0717 a 02 efea 3 b 0 EB 34 aadc 680 DC 498 | Twenty-seven million six hundred and fifty-one thousand two hundred and seventy-six | [自己](https://www.python.org/ftp/python/3.7.0/python-3.7.0-macosx10.9.pkg.asc) |
| [Windows 帮助文件](https://www.python.org/ftp/python/3.7.0/python370.chm) | Windows 操作系统 |  | 46562 af 86c 2049d 76808180dca | Eight million five hundred and forty-seven thousand six hundred and eighty-nine | [自己](https://www.python.org/ftp/python/3.7.0/python370.chm.asc) |
| [Windows x86-64 嵌入式 zip 文件](https://www.python.org/ftp/python/3.7.0/python-3.7.0-embed-amd64.zip) | Windows 操作系统 | for AMD64/EM64T/x64 | CB 8 B4 f 0d 979 a 36258 f 73 ed 541 def 10a 5 | Six million nine hundred and forty-six thousand and eighty-two | [自己](https://www.python.org/ftp/python/3.7.0/python-3.7.0-embed-amd64.zip.asc) |
| [Windows x86-64 可执行安装程序](https://www.python.org/ftp/python/3.7.0/python-3.7.0-amd64.exe) | Windows 操作系统 | for AMD64/EM64T/x64 | 531 C3 fc 821 ce 0 a 4107 b 6 D2 C6 a 129 be 3 e | Twenty-six million two hundred and sixty-two thousand two hundred and eighty | [自己](https://www.python.org/ftp/python/3.7.0/python-3.7.0-amd64.exe.asc) |
| [Windows x86-64 基于网络的安装程序](https://www.python.org/ftp/python/3.7.0/python-3.7.0-amd64-webinstall.exe) | Windows 操作系统 | for AMD64/EM64T/x64 | 3 cfda F4 c8 d3b 0475 aaec 12 ba 402d 04d 2 | One million three hundred and twenty-seven thousand one hundred and sixty | [自己](https://www.python.org/ftp/python/3.7.0/python-3.7.0-amd64-webinstall.exe.asc) |
| [Windows x86 嵌入式 zip 文件](https://www.python.org/ftp/python/3.7.0/python-3.7.0-embed-win32.zip) | Windows 操作系统 |  | ed 9 a1c 028 C1 e 99 f 5323 b 9 c 20723d 7d 6 f | Six million three hundred and ninety-five thousand nine hundred and eighty-two | [自己](https://www.python.org/ftp/python/3.7.0/python-3.7.0-embed-win32.zip.asc) |
| [Windows x86 可执行安装程序](https://www.python.org/ftp/python/3.7.0/python-3.7.0.exe) | Windows 操作系统 |  | ebb 6444 c 284 c 1447 e 902 e 87381 aeff 0 | Twenty-five million five hundred and six thousand eight hundred and thirty-two | [自己](https://www.python.org/ftp/python/3.7.0/python-3.7.0.exe.asc) |
| [Windows x86 基于网络的安装程序](https://www.python.org/ftp/python/3.7.0/python-3.7.0-webinstall.exe) | Windows 操作系统 |  | 779 c 4085464 EB 3 ee 5b 1 a4 fffd 0 eabca 4 | One million two hundred and ninety-eight thousand two hundred and eighty | [自己](https://www.python.org/ftp/python/3.7.0/python-3.7.0-webinstall.exe.asc) |

**下**

TwiTi 利用 NER 模型进行文本处理。运行前应建立 NER 模型。
更多信息请参考 ner/README.md。

**跑**

在`TwiTi`目录中运行下面的命令

**IOC 抽取**

**python-m IOC _ extractor–帮助**

**推文分类**

**python -m 分类器–帮助**

[**Download**](https://github.com/SamsungLabs/TwiTi)