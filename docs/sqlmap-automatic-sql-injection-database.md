# SQLMap:自动 SQL 注入和数据库接管工具

> 原文：<https://kalilinuxtutorials.com/sqlmap-automatic-sql-injection-database/>

[![SQLMap : Automatic SQL Injection & Database Takeover Tool](img/9f8ec5890aef1c24c82c78c1094cbfae.png "SQLMap : Automatic SQL Injection & Database Takeover Tool")](https://1.bp.blogspot.com/-7WAh9qTFHUY/XZhFMyiY0XI/AAAAAAAACzQ/_ZlJJKsguzoRps7LbNReEf0avEbMarSSgCLcBGAsYHQ/s1600/123%2B%25281%2529.png)

SQLMap 是一个开源渗透测试工具，它可以自动检测和利用 SQL 注入漏洞，接管数据库服务器。

它配备了一个强大的检测引擎，许多针对终极渗透测试器的利基功能，以及一系列广泛的开关，从数据库指纹识别、从数据库获取数据，到通过带外连接访问底层文件系统和在操作系统上执行命令。

**也读作-[Cryptondie:一个为研究目的开发的勒索软件](https://kalilinuxtutorials.com/cryptondie-ransomware-developed-study-purposes/)**

**安装**

点击[这里](https://github.com/sqlmapproject/sqlmap/tarball/master)可以下载最新的 tarball，点击[这里](https://github.com/sqlmapproject/sqlmap/zipball/master)可以下载最新的 zipball。

最好是，您可以通过克隆 [Git](https://github.com/sqlmapproject/sqlmap) 存储库来下载 sqlmap:

git 克隆–深度 1 https://github.com/sqlmapproject/sqlmap.git SQL map-dev

sqlmap 在任何平台上都可以与 [Python](http://www.python.org/download/) 版本 **2.6** 、 **2.7** 和 **3.x** 一起开箱即用。

**用法**

要获得基本选项和开关的列表，请使用:

python sqlpmap . py-h 格式

要获得所有选项和开关的列表，请使用:

python sqlmap.py -hh

你可以在这里找到一个样本运行[。要获得 sqlmap 功能的概述、支持的特性列表、所有选项和开关的描述以及示例，建议您查阅](https://asciinema.org/a/46601)[用户手册](https://github.com/sqlmapproject/sqlmap/wiki/Usage)。

**链接**

*   首页:[http://sqlmap.org](http://sqlmap.org/)
*   下载: [.tar.gz](https://github.com/sqlmapproject/sqlmap/tarball/master) 或者[。zip](https://github.com/sqlmapproject/sqlmap/zipball/master)
*   提交 RSS 源:[https://github.com/sqlmapproject/sqlmap/commits/master.atom](https://github.com/sqlmapproject/sqlmap/commits/master.atom)
*   问题跟踪者:[https://github.com/sqlmapproject/sqlmap/issues](https://github.com/sqlmapproject/sqlmap/issues)
*   用户手册:[https://github.com/sqlmapproject/sqlmap/wiki](https://github.com/sqlmapproject/sqlmap/wiki)
*   常见问题(FAQ):[https://github.com/sqlmapproject/sqlmap/wiki/FAQ](https://github.com/sqlmapproject/sqlmap/wiki/FAQ)
*   推特:[@ sqlcmap](https://twitter.com/sqlmap)
*   演示:[http://www.youtube.com/user/inquisb/videos](http://www.youtube.com/user/inquisb/videos)
*   截图:[https://github.com/sqlmapproject/sqlmap/wiki/Screenshots](https://github.com/sqlmapproject/sqlmap/wiki/Screenshots)

**译文**

*   [保加利亚语](https://github.com/sqlmapproject/sqlmap/blob/master/doc/translations/README-bg-BG.md)
*   [中文](https://github.com/sqlmapproject/sqlmap/blob/master/doc/translations/README-zh-CN.md)
*   克罗地亚语
*   [法语](https://github.com/sqlmapproject/sqlmap/blob/master/doc/translations/README-fr-FR.md)
*   [德语](https://github.com/sqlmapproject/sqlmap/blob/master/doc/translations/README-de-GER.md)
*   [希腊语](https://github.com/sqlmapproject/sqlmap/blob/master/doc/translations/README-gr-GR.md)
*   [印度尼西亚语](https://github.com/sqlmapproject/sqlmap/blob/master/doc/translations/README-id-ID.md)
*   [意大利语](https://github.com/sqlmapproject/sqlmap/blob/master/doc/translations/README-it-IT.md)
*   [日语](https://github.com/sqlmapproject/sqlmap/blob/master/doc/translations/README-ja-JP.md)
*   [韩语](https://github.com/sqlmapproject/sqlmap/blob/master/doc/translations/README-ko-KR.md)
*   [波兰](https://github.com/sqlmapproject/sqlmap/blob/master/doc/translations/README-pl-PL.md)
*   [葡萄牙语](https://github.com/sqlmapproject/sqlmap/blob/master/doc/translations/README-pt-BR.md)
*   [俄语](https://github.com/sqlmapproject/sqlmap/blob/master/doc/translations/README-ru-RUS.md)
*   [西班牙语](https://github.com/sqlmapproject/sqlmap/blob/master/doc/translations/README-es-MX.md)
*   [土耳其语](https://github.com/sqlmapproject/sqlmap/blob/master/doc/translations/README-tr-TR.md)
*   [乌克兰语](https://github.com/sqlmapproject/sqlmap/blob/master/doc/translations/README-uk-UA.md)

[**Download**](https://github.com/sqlmapproject/sqlmap)