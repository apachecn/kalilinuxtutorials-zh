# dir hunt–不用暴力就能找到网络目录

> 原文：<https://kalilinuxtutorials.com/dirhunt-directories-bruteforce/>

Dirhunt 是一个为搜索和分析目录而优化网络爬虫。如果服务器启用了模式的*“索引”，这个工具可以找到有趣的东西。如果没有启用目录列表，Dirhunt 也很有用。它检测目录与假 404 错误，目录中的一个空索引文件已被创建，以隐藏的东西和更多。*

```
$ dirhunt http://website.com/
```

Dirhunt 不使用蛮力。但它也不仅仅是一只爬虫。该工具比其他工具更快，因为它最大限度地减少了对服务器的请求。通常，该工具需要 5-30 秒，具体取决于网站和服务器。

**又读[XSS-有效载荷-列表:跨站脚本(XSS)漏洞有效载荷列表](https://kalilinuxtutorials.com/xss-payload-list/)**

## **Dirhunt 特征**

*   一次处理一个或多个站点。
*   处理“页的*索引，并报告感兴趣的文件。*
*   检测**个重定向器**。
*   检测到**目录上创建的空白索引文件**隐藏东西。
*   处理一些 html 文件以搜索新目录。
*   404 错误页面并检测出**假 404 错误**。
*   通过**标志**过滤结果。
*   最后分析结果。
*   使用 **robots.txt** 获取新目录

## **安装**

如果您的系统上安装了 Pip，您可以使用它来安装最新的 Dirhunt 稳定版本:

```
$ sudo pip3 install dirhunt
```

支持 Python 2.7 和 3.4-3.7，但建议使用 Python 3.x。使用`pip2`安装 Python2。

## **免责声明**

未经许可，不得在第三方服务器上使用本[软件](https://gbhackers.com/investing-fraud-detection-software/)。Dirhunt 是在被分析网站的所有者同意的情况下创建的，供审计团队使用。作者对该工具在法律之外的使用不负任何责任。

该软件受麻省理工学院许可。作者不提供任何担保。但是问题和拉动请求是受欢迎的。

![https://github.com/Nekmo/dirhunt](img/d861a9096555aeb1980fc054015933d7.png)