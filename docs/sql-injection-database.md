# SQL map–SQL 注入和数据库自动接管工具

> 原文：<https://kalilinuxtutorials.com/sql-injection-database/>

SQLMap 是一个开源渗透测试工具，它可以自动检测和利用 SQL 注入漏洞，接管数据库服务器。它配备了一个强大的检测引擎，许多针对终极渗透测试器的利基功能，以及一系列广泛的开关，从数据库指纹识别、从数据库获取数据，到通过带外连接访问底层文件系统和在操作系统上执行命令。

## **SQLMap 安装**

点击[这里](https://github.com/sqlmapproject/sqlmap/tarball/master)可以下载最新的 tarball，点击[这里](https://github.com/sqlmapproject/sqlmap/zipball/master)可以下载最新的 zipball。

最好，您可以通过克隆 Git 存储库来下载 sqlmap:

```
git clone --depth 1 https://github.com/sqlmapproject/sqlmap.git sqlmap-dev
```

sqlmap 在任何平台上都可以与 Python 版本 **2.6.x** 和 **2.7.x** 一起开箱即用。

**又读[micro ctfs——小 CTF 挑战跑码头](https://kalilinuxtutorials.com/microctfs-ctf-running-docker/)**

## **利用率**

要获得基本选项和开关的列表，请使用:

```
python sqlmap.py -h
```

要获得所有选项和开关的列表，请使用:

```
python sqlmap.py -hh
```

要获得 sqlmap 功能的概述、支持的特性列表、所有选项和开关的描述以及示例，建议您查阅[用户手册](https://github.com/sqlmapproject/sqlmap/wiki/Usage)。

## **重要链接**

*   首页:[http://sqlmap.org](http://sqlmap.org)
*   下载: [.tar.gz](https://github.com/sqlmapproject/sqlmap/tarball/master) 或者[。zip](https://github.com/sqlmapproject/sqlmap/zipball/master)
*   提交 RSS 源:[https://github.com/sqlmapproject/sqlmap/commits/master.atom](https://github.com/sqlmapproject/sqlmap/commits/master.atom)
*   问题跟踪者:[https://github.com/sqlmapproject/sqlmap/issues](https://github.com/sqlmapproject/sqlmap/issues)
*   用户手册:[https://github.com/sqlmapproject/sqlmap/wiki](https://github.com/sqlmapproject/sqlmap/wiki)
*   常见问题(FAQ):[https://github.com/sqlmapproject/sqlmap/wiki/FAQ](https://github.com/sqlmapproject/sqlmap/wiki/FAQ)
*   推特:[@ sqlcmap](https://twitter.com/sqlmap)
*   演示:[http://www.youtube.com/user/inquisb/videos](http://www.youtube.com/user/inquisb/videos)
*   截图:[https://github.com/sqlmapproject/sqlmap/wiki/Screenshots](https://github.com/sqlmapproject/sqlmap/wiki/Screenshots)

## **截图 SQL 注入**

 **![](img/74f2b4e79f7c8294c4e3d5dd8b64482a.png) [ ![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/sqlmapproject/sqlmap)** **信用:Netsparker 网络应用安全扫描器**