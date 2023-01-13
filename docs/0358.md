# 马尔孔-2019 年恶意软件通信分析器

> 原文：<https://kalilinuxtutorials.com/malcom-malware-communications-analyzer/>

马尔孔是一种工具，旨在使用网络流量的图形表示来分析系统的网络通信，并将它们与已知的恶意软件来源进行交叉引用。

这在分析某些恶意软件物种如何试图与外界通信时很方便。该工具可以在以下方面为您提供帮助:

*   检测中央命令和控制(C&C)服务器
*   了解对等网络
*   观察 DNS 快速流动基础设施
*   快速确定网络工件是否“已知有害”

该工具的目的是通过提供源自给定主机或网络的人类可读版本的网络流量，使恶意软件分析和英特尔收集*更快*。更快地将网络流量信息转化为可操作的情报。

**又读:** [Evilginx2:独立中间人攻击框架](https://kalilinuxtutorials.com/evilginx2-man-in-the-middle-attack/)

## **马尔孔安装**

它是用 python 写的。如果您有必要的库，您应该能够在任何平台上运行它。我强烈推荐使用 python 虚拟环境(virtualenv ),以免搞乱您的系统库。

以下测试是在 Ubuntu server 14.04 LTS 版上进行的:

**安装 git、python 和 libevent libs、mongodb、redis 和其他依赖项**

**$ sudo apt-get install build-essential git python-dev libevent-dev mongob libxml 2-dev libxslt-dev zlib 1g-dev redis 服务器 libffi-dev libssl-dev python-virtualenv**

**克隆 Git 回购:**

克隆 https://github.com/tomchop/malcom.git·马尔科

**创建并激活您的 virtualenv:**

**$ CD malcom
$ virtualenv env-malcom
$ source env-malcom/bin/activate**

**获取并安装 scapy:**

**$ cd..
$ wget http://www . sec dev . org/projects/scapy/files/scapy-latest . tar . gz
$ tar xvzf scapy-latest.tar.gz
$ CD scapy-2 . 1 . 0
$ python setup . py 安装**

**还是从你的 virtualenv，从 requirements.txt 文件安装必要的 python 包:**

**$ cd../malcom
$ pip install-r requirements . txt**

为了让 IP 地理定位工作，你需要下载 Maxmind 数据库并将文件解压到**malcom/马尔孔/auxiliary/geoIP** 目录。你可以从以下链接获得 Maxmind 的免费(因此或多或少准确)数据库:【http://dev.maxmind.com/geoip/geoip2/geolite2/[:](http://dev.maxmind.com/geoip/geoip2/geolite2/)

**$ cd 马尔孔/辅助/geoIP
$ wget http://geolite . maxmind . com/download/geoIP/database/geolite 2-city . MMDB . gz
$ gunzip-d GeoLite2-City.mmdb.gz
$ mv geolite 2-city . MMDB geoIP 2-city . MMDB**

使用**从工具目录启动网络服务器。/malcom.py** 。检查**。/malcom . py**–监听接口和端口的帮助。

首先，您可以将 **malcom.conf.example** 文件复制到 **malcom.conf** 并运行**。/malcom.py -c malcom.conf.**

## 技术规格

它大部分是用 Python 从头开始写的。它使用以下框架工作:

*   一个轻量级的 python web 框架
*   一个 NoSQL 数据库。它通过 [pymongo](http://api.mongodb.org/python/current/) 与 python 接口
*   [redis](https://github.com/tomchop/malcom/blob/master/redis.io)–高级内存键值存储
*   [d3js](http://d3js.org/)——一个 JavaScript 库，可以生成令人敬畏的力导向图(【https://github.com/mbostock/d3/wiki/Gallery】T2)
*   引导程序(bootstrap)——一个 CSS 框架，它将最终杀死 webdesign，但使它非常容易地快速“网络化”只能通过命令提示符工作的应用程序。

## 放弃

这个工具是我在空闲时间编写的。像我们每天下载和使用的大量工具一样，我们不建议在数据稳定性和可靠性是必须的生产环境中使用它。

*   它可能被破坏，存在安全漏洞(在不受控制环境中以 root 用户身份运行它可能不是一个好主意)，或者根本不工作。
*   它是用 python 写的，所以不要指望它会超快或轻松处理海量数据。
*   我不是程序员，所以不要期望在任何地方都能看到漂亮的 pythonic 代码。或者很多评论。

它处于发展的早期阶段。

[**Download**](https://github.com/tomchop/malcom#installation)

**信用:托马斯·乔皮蒂亚**