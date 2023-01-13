# KaliTorify:用于 Kali Linux 操作系统的透明代理

> 原文：<https://kalilinuxtutorials.com/kalitorify-transparent-proxy/>

[![KaliTorify : Transparent Proxy Through Tor For Kali Linux OS](img/92191d508a6f0b39fee1614c6b492dae.png "KaliTorify : Transparent Proxy Through Tor For Kali Linux OS")](https://1.bp.blogspot.com/-MoIXnj4hXeo/XQPvpfkBW6I/AAAAAAAAA1o/mslHp3omtDQCPeENLHigHhyXxKy1-bXeQCLcBGAs/s1600/Kali.png)

**Kalitorify** 是一个用于 [Kali Linux](https://www.kali.org/) 的 shell 脚本，它使用 [iptables](https://www.netfilter.org/projects/iptables/index.html) 设置通过 Tor 网络创建一个**透明代理，该程序还允许您执行各种检查，如检查 Tor 出口节点(即当您处于 Tor 代理下时您的公共 IP)，或者检查 Tor 是否已正确配置服务和网络设置。**

简单地说，使用 kalitorify，您可以通过 Tor 网络重定向 Kali Linux 操作系统的所有流量。

**也读作:[RecScanSec–侦察扫描仪安全](https://kalilinuxtutorials.com/recscansec-reconnaisance-scanner-security/)**

**什么是通过 Tor 的透明代理？**

透明代理是位于用户和内容提供商之间中间系统。

当用户向 web 服务器发出请求时，透明代理拦截该请求以执行各种动作，包括缓存、重定向和认证。

![](img/d99daa9a121f2c9553adc6f2fefafafb.png)

通过 Tor 的透明代理意味着每个网络应用程序都将通过 Tor 进行 TCP 连接；任何应用程序都无法通过直接连接来泄露您的 IP 地址。

在 Tor 项目 wiki 中，你可以找到关于什么是**“透明代理通过 Tor”**以及相关设置的解释。**如果你想安全地使用加里托里法，请阅读它。**

**安装**

**安装依赖:**

**sudo apt 更新& & sudo apt 完全升级-y
sudo apt 安装 tor -y**

**安装加里波第&重启:**

**git 克隆 https://github.com/brainfucksec/kalitorify
CD kalitorify/
sudo make install
sudo 重启**

* * *

**用法**

**选项**

**-t，–tor**

**通过 tor 启动透明代理**

**-c，–clearnet**

重置 iptables 并返回 clearnet 导航

**-s，–状态**

**检查程序和服务的状态**

**-i，–IP info**

**显示公共 IP**

**-r，–重启**

重启 tor 服务并更改 IP

**安全**

**kalitorify 是独立于 Tor anonimity 软件制作的，Tor 项目不对其质量、适用性或任何其他方面做出保证，**请阅读这些文档，了解如何安全使用 Tor 网络:

[Tor 一般常见问题解答](https://www.torproject.org/docs/faq.html.en)

[世卫组织请勿推荐](https://www.whonix.org/wiki/DoNot)

kalitorify 在 Tor 上提供透明的代理管理，但不提供 100%匿名。

关于透明托管:使用 iptables 透明托管系统提供了相对强大的泄漏保护，但它不能替代虚拟化托管应用程序，如 Whonix 或 TorVM。应用程序仍然可以学习你的电脑的主机名，MAC 地址，序列号，时区等。拥有根权限的用户可以完全禁用防火墙。换句话说，iptables 的透明化可以防止误配置软件的意外连接和 DNS 泄漏，但不足以防止恶意软件或具有严重安全漏洞的软件。

为此，您至少应该更改主机名和 MAC 地址:

[在 Debian 上设置主机名](https://debian-handbook.info/browse/stable/sect.hostname-name-service.html)

[在 Linux 上更改 MAC 地址](https://en.wikibooks.org/wiki/Changing_Your_MAC_Address/Linux)

**检查泄漏:**

启动 kalitorify 后，您可以使用 [tcpdump](https://www.tcpdump.org/) 来检查 Tor 之外是否有任何互联网活动:

首先，获取您的网络接口:

**ip -o 地址**
或
**tcpdump -D**

我们假设它是`eth0`。

接下来你需要识别 tor 的守卫 IP，你可以通过 Tor 控制器使用`**ss**` **、** `**netstat**` **或者** `**GETINFO entry-guards**`来识别守卫 IP。

带`ss`的例子:

【t0-NTP \ grep $(cat/var/run/tor/tor . PID)】t1

有了接口和保护 IP，我们现在可以使用`tcpdump`来检查可能的非 tor 泄漏。更换 IP。TO.TOR.GUARD 用你从`ss`输出得到的 IP。

**tcpdump -n -f -p -i eth0 不是 arp 也不是主机 IP。TO.TOR.GUARD**

除了头两行，您不应该看到任何输出。你可以移除`and **not host IP**`来看看它是什么样子。

[**Download**](https://github.com/brainfucksec/kalitorify)