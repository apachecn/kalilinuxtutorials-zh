# SQLMap v 1 . 2 . 9–自动 SQL 注入和数据库接管工具

> 原文：<https://kalilinuxtutorials.com/sqlmap-v1-2-9-automatic-injection/>

**SQLMap v1.2.9** 是一款开源渗透测试工具，可以自动检测和利用 SQL 注入漏洞以及接管数据库服务器。它配备了一个强大的检测引擎，许多针对终极渗透测试器的利基功能，以及一系列广泛的开关，从数据库指纹识别、从数据库获取数据，到通过带外连接访问底层文件系统和在操作系统上执行命令。

## **SQLMap v1.2.9 安装**

点击[这里](https://github.com/sqlmapproject/sqlmap/tarball/master)可以下载最新的 tarball，点击[这里](https://github.com/sqlmapproject/sqlmap/zipball/master)可以下载最新的 zipball。

最好是，您可以通过克隆 [Git](https://github.com/sqlmapproject/sqlmap) 存储库来下载 sqlmap:

```
git clone --depth 1 https://github.com/sqlmapproject/sqlmap.git sqlmap-dev
```

sqlmap 在任何平台上都可以与 Python 版本 **2.6.x** 和 **2.7.x** 一起开箱即用。

**也可理解为[WinPwnage——提升、UAC 旁路、特权升级、dll 劫持技术](https://kalilinuxtutorials.com/winpwnage-dll-hijack-techniques/)**

## **用途**

要获得基本选项和开关的列表，请使用:

```
python sqlmap.py -h
```

要获得所有选项和开关的列表，请使用:

```
python sqlmap.py -hh
```

你可以在这里找到一个样本运行[。获得 sqlmap 功能的概述、支持的特性列表、所有选项和开关的描述以及示例。](https://asciinema.org/a/46601)

## **截图**

![](img/26d106cb4c409147c8ccc66e926760cf.png)

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/sqlmapproject/sqlmap) **信用:[网络安全扫描器](https://www.netsparker.com/?utm_source=github.com&utm_medium=referral&utm_content=sqlmap+repo&utm_campaign=generic+advert)**