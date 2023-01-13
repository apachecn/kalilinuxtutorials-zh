# DNSPeep:监视你的计算机正在进行的 DNS 查询

> 原文：<https://kalilinuxtutorials.com/dnspeep/>

[![DNSPeep : Spy On The DNS Queries Your Computer Is Making](img/c5074a71b9702cadb7abc317726b7b87.png "DNSPeep : Spy On The DNS Queries Your Computer Is Making")](https://1.bp.blogspot.com/-oQPyd1WFlFc/YIiEdLeQV6I/AAAAAAAAI3w/VNOWlXmHPiU9V5iB0lISfmsm3nZ9xSBpQCLcBGAsYHQ/s728/Dnspeep%25281%2529.png)

**DNSPeep** 让你监视你的计算机正在进行的 DNS 查询。

以下是一些输出示例:

$ sudo dnspeep
查询名称服务器 IP 响应
A incoming.telemetry.mozilla.org 192 . 168 . 1 . 1 CNAME:telemetry-incoming.r53-2.services.mozilla.com，CNAME:pipeline-incoming-prod-elb-149169523 . us-west-2 . elb . Amazon AWS . com，A:52.39.144.189，A:54.191.136.131，A:34.215.151.143，A:54.149.208.57，A:44.226.235.191，A:52.10.174.113，A: 35.160.138.173，A: 44.238.190

**如何安装？**

您可以使用下面的不同方法安装 dnspeep。

**安装二进制版本**

1.  从[GitHub 发布页面](https://github.com/jvns/dnspeep/releases)下载`**dnspeep**`的最新版本
2.  打开它
3.  将`**dnspeep**`二进制文件放在您的路径中(例如在`**/usr/local/bin**`中)

**编译&从源码安装**

1.  从[的 GitHub 发布页面](https://github.com/jvns/dnspeep/releases)下载`**dnspeep**`的最新源代码发布，或者 git 克隆这个库。
2.  打开它
3.  运行`**cargo build --release**`
4.  在那里切换到“目标/发布”目录。
5.  把`**dnspeep**`二进制放到你的路径中(例如在 **`/usr/local/bin`** )

**从 Linux 软件包管理器安装**

*   如果您使用的是 Arch Linux，那么您可以从 [AUR](https://aur.archlinux.org/) 安装 dnspeep。

它是如何工作的？

它使用`**libpcap**`来捕获端口 53 上的数据包，然后匹配 DNS 请求和响应数据包，以便它可以在同一行上显示请求和响应。

它还跟踪在 1 秒内没有得到响应的 DNS 查询，并打印出响应 **`<no response>`。**

**限制**

*   仅支持由`**dns_parser**`箱支持的 DNS 查询类型([这里有一个列表](https://docs.rs/dns-parser/0.8.0/dns_parser/))
*   不支持 TCP DNS 查询，仅支持 UDP
*   它不能显示 HTTPS DNS 查询(因为它需要 MITM HTTPS 连接)

[**Download**](https://github.com/jvns/dnspeep)