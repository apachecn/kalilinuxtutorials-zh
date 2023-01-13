# 白寡妇:SQL 漏洞扫描器

> 原文：<https://kalilinuxtutorials.com/whitewidow/>

[![Whitewidow : SQL Vulnerability Scanner](img/51be57e277ca110de0663c6a99a7c977.png "Whitewidow : SQL Vulnerability Scanner")](https://1.bp.blogspot.com/-WmLjE_xaSh0/XQFLQg3vkGI/AAAAAAAAAxk/TSQOK932fcgzhmdFnTOtgZ7nQqrt869ZgCLcBGAs/s1600/Whitewidow.png)

白寡妇是一个开源的自动化 SQL 漏洞扫描器，它能够运行一个文件列表，或者在谷歌上搜索潜在的易受攻击的网站。

它允许自动文件格式化，随机用户代理，IP 地址，服务器信息，多 SQL 注入语法，从程序启动 sqlmap 的能力，和一个有趣的环境。

该程序是为学习目的而创建的，旨在教导用户漏洞是什么样子的。最好是克隆库，或者你可以在这里下载 zip 和 tarball

**也可阅读—[PenTest 的 5 大 SQL 注入工具&黑客](https://kalilinuxtutorials.com/top-5-sql-injection-tools-for-pentest-hacking/)**

**基本用法**

*   这将在默认模式下运行 whitewidow，并使用随机搜索查询在谷歌上搜索可能的网站。
*   这将在一个给定的文件中运行 whitewidow，并将 SQL 语法添加到 URL 中。
*   `**ruby whitewidow.rb -h**`将运行帮助标志并显示帮助菜单。

有关用法和更多标志的更多信息，您可以查看 wiki 功能页面[这里](https://github.com/Ekultek/whitewidow/wiki/Functionality)。

**依赖关系**

*   `**gem 'mechanize'**`
*   `**gem 'nokogiri'**`
*   `**gem 'rest-client'**`
*   `**gem 'webmock'**`
*   `**gem 'rspec'**`
*   `**gem 'vcr'**`

要安装所有 gem 依赖项，请遵循以下模板:

**cd 白寡妇
捆绑安装**

在 Linux 系统(Kali、BlackArch、Parrot 等)上安装时，您可能会遇到问题..)要解决此问题，请尝试以下方法:

**sudo apt-get 安装 liblzma-dev
sudo apt-get 安装 zlib1g-dev
cd 白寡妇
捆绑安装**

这将安装所有需要的 gems，并允许您顺利运行程序。

[**Download**](https://github.com/WhitewidowScanner/whitewidow)