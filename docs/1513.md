# Netenum:网络侦察工具，用于嗅探活动主机

> 原文：<https://kalilinuxtutorials.com/netenum/>

[![Netenum : Network Reconnaisance Tool That Sniffs For Active Hosts](img/5e33d9e728fbc9c9202bac0ad167cac7.png "Netenum : Network Reconnaisance Tool That Sniffs For Active Hosts")](https://1.bp.blogspot.com/-jbfziD5yawc/Xy-jCOq6xWI/AAAAAAAAHRc/3M8_asmlBGYOF8K9cbEGyyu0BNAe9G8VwCLcBGAsYHQ/s728/Netenum%25281%2529.png)

**Netenum** 被动监控网络上的 ARP 流量。它提取每个活动主机的基本数据，如 IP 地址、MAC 地址和制造商。这个工具的主要目的是在不产生太多噪音的情况下找到活跃的机器。

**特性**

*   提供有关网络的基本信息，如 ESSID 和当前信号强度。
*   找到的主机可以写入文件(接下来我们可以使用 Nmap 的`-iL <hosts_file>`选项来扫描检测到的主机)。
*   在 IP 地址旁边显示一个签名，表明该主机是本地网关:`(G)`。

**截图**

![](img/5314fd6574cba5e78db7e3d2a9cabea0.png)[**Download**](https://github.com/wintrmvte/Netenum#features)