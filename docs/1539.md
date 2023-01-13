# Reconspider:最先进的开源智能(OSINT)框架

> 原文：<https://kalilinuxtutorials.com/reconspider/>

[![Reconspider : Most Advanced Open Source Intelligence (OSINT) Framework](img/55940f4fb059073556da8357764a8d9b.png "Reconspider : Most Advanced Open Source Intelligence (OSINT) Framework")](https://1.bp.blogspot.com/-fBq3r6yuWhY/X0gTe3ByCzI/AAAAAAAAHbs/GiMsW5JSEfsKpb_6X0aybWJSr6noxKcWgCLcBGAsYHQ/s728/ReconSpider%25281%2529.png)

ReconSpider 是最先进的开源智能(OSINT)框架，用于扫描 IP 地址、电子邮件、网站、组织，并从不同来源找到信息。

信息安全研究人员、渗透测试人员、漏洞猎人和网络犯罪调查人员可以使用 ReconSpider 来查找有关其目标的深层信息。

ReconSpider 聚合所有原始数据，在仪表板上直观显示，并促进对数据的警报和监控。

侦察蜘蛛还结合了[波](https://github.com/adithyan-ak/WAVE)、[光子](https://github.com/s0md3v/Photon)和[侦察犬](https://github.com/s0md3v/ReconDog)的能力，对攻击面做全面的枚举。

**为什么叫 ReconSpider？**

**`ReconSpider` = `Recon` + `Spider`**

*   侦察=侦察

侦察是通过各种探测手段获取关于敌人或潜在敌人的活动和资源，或特定区域的地理特征的信息的任务。

*   **蜘蛛=网络爬虫**

网络爬虫，有时称为蜘蛛或蜘蛛机器人，通常简称为爬虫，是系统地浏览万维网的互联网机器人，通常用于网络索引(网络蜘蛛搜索)。

**版本(测试版)**

**搜索引擎:** 1.0.6

**工具概述**

*   对 IP 地址、电子邮件、网站、组织进行在线扫描，并从不同来源查找信息。
*   关联和协作结果，以统一的方式显示它们。
*   对整合数据使用特定脚本/启动自动化 OSINT。
*   目前仅在命令行界面(CLI)中可用。

**思维导图(v1)**

查看我们的思维导图，可以看到这个工具关于 api、服务和技术等的可视化组织信息。

[**http://bhavkaran.com/reconspider/mindmap.html**](http://bhavkaran.com/reconspider/mindmap.html)

 ****文档**

安装和使用 ReconSpider 非常容易。安装过程非常简单。

1.  下载或克隆 ReconSpider github 库。
2.  正在安装所有依赖项。

我们开始吧！！

*   **设置环境(Linux 操作系统)**

**步骤 1—**在您的 linux 系统上克隆 ReconSpider。

为了下载 ReconSpider，只需克隆 github 库。下面是您可以用来克隆 ReconSpider 库的命令。

**git 克隆 https://github . com/bhavsec/reconspider . git**

**步骤 2—**确保您的系统上安装了 python3 和 python3-pip。

您也可以通过在终端中键入以下命令来执行检查。

sudo 安装 python3 python3-pip

**步骤 3—**安装所有依赖项。

一旦您克隆并检查 python 安装，您将发现目录名为 **reconspider** 。只需转到该目录，使用以下命令进行安装:

**CD recon spider
sudo python setup . py 安装**

*   **设置环境(Windows 操作系统)**

**步骤 1—**在您的 windows 系统上下载 ReconSpider。

要从 github 仓库下载 ReconSpider，只需将此 URL 复制并粘贴到您最喜欢的浏览器中。

**https://github.com/bhavsec/reconspider/archive/master.zip**

**步骤 2—**解压文件

下载后，你会发现压缩后的文件名为 **datasploit-master.zip** 。只需右键点击压缩文件，然后使用任何软件解压文件，如 [WinZip](https://www.winzip.com/) 、 [WinRAR](https://www.win-rar.com) 。

**步骤 3—**安装所有依赖项。

解压缩后，使用命令提示符进入该目录，并键入以下命令。

**python setup.py 安装**

**步骤 4—**数据库

*   **IP2Proxy 数据库**

**https://lite . IP 2 location . com/database/px8-IP-proxy type-country-region-city-ISP-domain-usage type-ASN-last seen**

下载数据库，将其解压缩并移动到 reconspider/plugins/目录。

**也可阅读-[帕果多:自动化谷歌黑客数据库抓取和搜索](https://kalilinuxtutorials.com/pagodo/)**

**用途**

ReconSpider 是一个非常方便的工具，易于使用。你所要做的就是把值传递给参数。要启动 ReconSpider，只需键入:

**python reconspider.py**

*   **IP**

该选项从公共资源中收集给定 IP 地址的所有信息。

**侦察员>>1
IP>>8.8.8.8**

*   **域**

此选项收集给定 URL 地址的所有信息，并检查漏洞。

**搜索引擎>2
主机(URL/IP)>vulnweb.com
端口>443**

*   **电话号码**

此选项允许您收集给定电话号码的信息。

**搜索> > 3
电话号码(919485247632) > >**

*   **DNS 映射**

此选项允许您使用与目标组织相关联的 DNS 记录的虚拟 DNS 映射来映射组织的攻击面。

**recon spider>>4
DNS MAP(URL)>>vulnweb.com**

*   **元数据**

此选项允许您提取文件的所有元数据。

**Reconspider > > 5
元数据(路径)>>/root/Downloads/images . JPEG**

*   **反向图像搜索**

此选项允许您获取互联网上的信息和类似图像。

**recon spider>6
反向图片搜索(路径)>>/root/Downloads/images . JPEG
在 web broser 中打开搜索结果？(是/否):y**

*   **蜜罐**

此选项允许您识别蜜罐！一个 IP 是一个蜜罐的概率在一个范围从 0.0 到 1.0 的“Honeyscore”值中被捕获

**ReconSpider > > 7
蜜罐(IP)>>1.1.1.1**

*   **MAC 地址查找**

此选项允许您识别 Mac 地址的详细信息，如制造商、地址、国家等。

**Reconspider > > 8
MAC 地址查找(例如:08:00:69:02:01:FC) > >**

*   **iphone map**

如果使用准确的协调器连接所有提供的 ip 位置，此选项为您提供了提供的 ip 或单个 ip 的热图。

**recon spider>>9

1)追踪单个 IP
2)追踪多个 IP
选项> >**

*   **激流**

此选项允许您收集种子下载历史的历史。

**搜索>>10
IP 地址(例如:192.168.1.1) > >**

*   **用户名**

此选项允许您从 Instagram、Twitter、脸书等社交媒体收集所提供用户名的帐户信息。

**再蜘蛛> > 11

1。脸书
2。推特
3。insta gram
用户名>**

*   **IP2PROXY**

此选项允许您识别 IP 地址是否使用任何类型的 VPN /代理来隐藏其身份。

**搜索>>12
IP 地址(例如:192.168.1.1) > >**

*   **邮件泄露**

此选项允许您从给定的域中识别所有被破坏的邮件 ID。

**Reconspider > > 13
域(如:intercom.io) > >**

*   **更新**

此选项允许您检查更新。如果有新版本可用，ReconSpider 将下载更新并将其合并到当前目录中，而不会覆盖其他文件。

**搜索引擎> > 99
检查更新..**

*   **退出**

此选项允许您从 ReconSpider 框架退出到当前操作系统的终端。

**ReconSpider > > 0
再见，再见..**

[**Download**](https://github.com/bhavsec/reconspider)**