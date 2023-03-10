# xs spy–Web 应用程序 XSS 扫描器

> 原文：<https://kalilinuxtutorials.com/xsspy-web-application/>

XssPy 是一个 web 应用程序 XSS 扫描器。Xsspy 最近被微软的一名工程师用来发现五角大楼 bug Bounty 计划中的一个 Bug。

**也可理解为[【CVE-搜索:对已知漏洞进行本地搜索的工具](https://kalilinuxtutorials.com/cve-search-tool-vulnerabilities/)**

## **安装 xs spy**

在终端中键入以下内容。

**`git clone https://github.com/faizann24/XssPy/` /opt/xsspy**

该工具适用于 Python 2.7，您应该已经安装了 mechanize。如果没有安装 mechanize，在终端中键入“pip install mechanize”。

## **用法**

运行下面的命令。

`python XssPy.py website.com`

## **描述**

XssPy 是一个 python 工具，用于查找网站中的跨站脚本漏洞。这个工具是同类中的第一个。这个工具不是像大多数工具那样只检查一个页面，而是遍历整个网站，首先找到所有的链接和子域。之后，它开始扫描遍历时找到的每一页上的每一个输入。它使用小而有效的有效载荷来搜索 XSS 漏洞。

该工具已经与付费漏洞扫描器进行了平行测试，大多数扫描器未能检测到该工具能够发现的漏洞。此外，大多数付费工具只扫描一个站点，而 XSSPY 首先找到许多子域，然后扫描所有链接。该工具附带:

1.  短扫描
2.  全面扫描
3.  查找子域
4.  检查每页上的每个输入

借助该工具，在麻省理工学院、斯坦福大学、杜克大学、Informatica、Formassembly、ActiveCompaign、Volcanicpixels、牛津大学、摩托罗拉大学、伯克利大学等网站中发现了跨站点脚本漏洞。

[![https://github.com/faizann24/XssPy](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/faizann24/XssPy)