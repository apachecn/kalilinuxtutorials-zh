# TCP preplay–适用于 UNIX 和 Windows 的 Pcap 编辑和重放工具

> 原文：<https://kalilinuxtutorials.com/tcpreplay-unix-windows/>

**Tcpreplay** 是一套适用于 UNIX 操作系统的 GPLv3 授权实用程序，用于编辑和重放以前由 tcpdump 和 Ethereal/Wireshark 等工具捕获的网络流量。

它允许您将流量分类为客户端或服务器，重写第 2 层、第 3 层和第 4 层数据包，并最终通过交换机、路由器、防火墙、NIDS 和 IPS 等其他设备将流量回放到网络上。

它支持单网卡和双网卡模式，用于测试嗅探和串联设备。

它还被许多防火墙、IDS、IPS、NetFlow 和其他网络供应商、企业、大学、实验室和开源项目所使用。

如果您的组织使用 Tcpreplay，请让我们知道您是谁以及您使用它的目的，以便我可以继续添加有用的功能。

Tcpreplay 设计用于网络硬件，通常不会渗透到第 2 层以下。

从版本 4.0 开始，Tcpreplay 得到了增强，以解决测试和调整 IP 流/网络流硬件的复杂性。增强功能包括:

*   支持 [netmap](http://info.iet.unipi.it/~luigi/netmap/) 修改后的网络驱动程序，实现 10GigE 线速性能
*   提高回放速度的准确性
*   提高结果报告的准确性
*   流量统计，包括每秒流量(fps)
*   流分析，用于分析和微调流到期超时
*   每秒几十万个流量(取决于 pcap 文件中的流量大小)

**也可以理解为:**N[ova hot——渗透测试人员的 Webshell 框架](https://kalilinuxtutorials.com/novahot-penetration-testers/)

## Tcpreplay 安装

#### 【Unix 用户的简单指南

您将需要编译源代码，但是首先您必须确保您已经安装了编译工具和必备软件。例如，在基本的 Ubuntu 或 Debian 系统上，您可能需要执行以下操作:

**sudo apt-get install build-essential libpcap-dev**

接下来解压缩 tarball，转到根目录，然后执行以下操作:

**。/configure
make
sudo make install**

您可以选择运行测试，以确保您的安装功能完全正常:

**sudo make 测试**

#### **视频教程**

[https://www.youtube.com/embed/5iK-0MiHZmI?feature=oembed&enablejsapi=1](https://www.youtube.com/embed/5iK-0MiHZmI?feature=oembed&enablejsapi=1)

#### **网络地图视频教程**

[https://www.youtube.com/embed/hswh90iIw9s?feature=oembed&enablejsapi=1](https://www.youtube.com/embed/hswh90iIw9s?feature=oembed&enablejsapi=1)

### Windows 说明

考虑 Windows 对 Tcpreplay 的支持是试验性的——如果你愿意的话，是测试质量。我们强烈建议您阅读关于如何获得 Tcpreplay 支持的[页面。](http://tcpreplay.appneta.com/wiki/support.html)

也就是说，你需要 [Cygwin](http://www.cygwin.com/) 来编译/运行 tcpreplay。你还需要安装[Winpcap](http://www.winpcap.org)——Windows 的 libpcap 端口。不管出于什么原因，将 Winpcap 文件安装在 Cygwin 根目录(/Wpdpack)中似乎很重要。

确保安装了[驱动和 DLL](http://www.winpcap.org/install/default.htm) 文件以及[开发者包](http://www.winpcap.org/devel.htm)。然后当你跑的时候。/configure，您将需要使用`**--with-libpcap**`标志指定 Winpcap 的位置，但是使用全部小写:`**./configure** **--with-libpcap=/wpdpack**`。

注意:我们已经得到通知，古勒 Cygwin 包被打破。这严重破坏了 GNU Autogen 的某些部分——特别是那些允许你通过 GitHub 构建 Tcpreplay 的部分。因此，我强烈建议抓一个 tarball 释放。

[**Download**](https://github.com/appneta/tcpreplay)

**鸣谢:亚伦·特纳、亚赞·暹罗&弗雷德·克拉森(4.0 版本)**