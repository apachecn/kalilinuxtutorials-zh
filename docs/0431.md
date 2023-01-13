# Ntopng:基于 Web 的流量和安全网络流量监控

> 原文：<https://kalilinuxtutorials.com/ntopng-traffic-monitoring/>

Ntopng 是一个基于 web 的网络流量监控应用程序，由 GPLv3 发布。它是 1998 年编写的原始 ntop 的新版本，现在在性能、可用性和特性方面进行了改进。

如果你更喜欢使用预建的包而不是源代码，请前往[http://packages.ntop.org](http://packages.ntop.org)

我们为以下平台构建二进制包:

*   Ubuntu Linux 服务器 x64
*   CentOS/RedHat Linux x64
*   Windows x64
*   RaspberryPI/BeagleBoard ARM(基于 Ubuntu Linux)
*   普适网络边缘路由器(MIPS)

ntopng 有三个版本，分别是社区版、专业版和企业版。ntopng 自动切换到这三个版本中的一个，这取决于许可证的存在。

**也读-[Wordlistctl:获取、安装&从网站搜索 Wordlist 档案&Torrent Peers](https://kalilinuxtutorials.com/wordlistctl-websites-torrent-peers/)**

这三个版本的功能和比较可在[https://www.ntop.org/products/traffic-analysis/ntop/](https://www.ntop.org/products/traffic-analysis/ntop/)获得。

社区不需要任何许可证。专业版和企业版需要许可证。

许可证是基于服务器的，并根据 EULA(最终用户许可协议)发布。每个许可证都是永久性的(即不会过期)，并且允许在购买/许可证颁发后的一年内安装更新。

这意味着在 2018 年 1 月 1 日生成的许可证将能够激活软件的新版本，直到 2019 年 1 月 1 日。

如果您想在该日期后安装软件版本的新版本，您需要续订维护或避免进一步更新软件。

对于基于源代码的 ntopng，您可以参考 GPL-v3 许可证。

ntopng 许可证是使用您在[https://shop.ntop.org/](https://shop.ntop.org/)购买许可证时提供的订单 Id 和电子邮件生成的。

**主要特点**

*   根据许多标准对网络流量进行分类，包括 IP 地址、端口、L7 协议、吞吐量、自治系统(ASs)
*   显示实时网络流量和活动主机
*   为包括吞吐量和应用协议在内的多项网络指标生成长期报告
*   最大流量生成者(发送者/接收者)、最大流量生成者、最大 L7 应用
*   监控并报告实时吞吐量、网络和应用延迟、往返时间(RTT)、TCP 统计数据(重新传输、无序数据包、数据包丢失)以及传输的字节和数据包
*   在磁盘上存储持久的流量统计数据，以便将来进行探索和事后分析
*   在地理图中地理定位和覆盖主机
*   利用 [nDPI](https://www.ntop.org/products/ndpi/) 、ntop 深度数据包检测(DPI)技术发现应用协议(脸书、YouTube、BitTorrent 等)
*   通过利用由[谷歌](http://en.wikipedia.org/wiki/Google_Safe_Browsing)和 [HTTP 黑名单](http://www.projecthoneypot.org/httpbl.php)提供的表征服务来表征 HTTP 流量。
*   分析 IP 流量，并根据来源/目的地进行分类。
*   报告按协议类型排序的 IP 协议使用情况
*   产生 HTML5/AJAX 网络流量统计。
*   完全支持 IPv4 和 IPv6
*   全面的第 2 层支持(包括 ARP 统计)
*   GTP/希腊失谐
*   支持 [MySQL](https://www.ntop.org/ntopng/exploring-historical-data-using-ntopng-part-2/) 、 [ElasticSearch](https://www.ntop.org/ntopng/exploring-your-traffic-using-ntopng-with-elasticsearchkibana/) 和 [LogStash](https://www.ntop.org/ntopng/filling-the-pipe-exporting-ntopng-flows-to-logstash/) 导出监控数据
*   导出到 MySQL 的监控数据的交互式历史探索
*   警报引擎捕获异常和可疑的主机
*   [SNMP](https://www.ntop.org/ntopng/monitoring-network-devices-with-ntopng-and-snmp/) v1/v2c 支持并持续监控 SNMP 设备。

[**Download**](https://github.com/ntop/ntopng)