# 间谍:Linux 的网络数据包和流量拦截器。欺骗 ARP 并窃听网络

> 原文：<https://kalilinuxtutorials.com/espionage/>

[![](img/ae590e3952fd492c71b6783dde4d40fa.png)](https://blogger.googleusercontent.com/img/a/AVvXsEg0w6cOtKDq8oYWAAv2N53qm1jmYIC47RvxENLbSQ2O8UWQr9muXVJhAkFDyN1N4TupwqJx2kDYU_-MME1KxPJLAFHgHsgf7GidgqFvNSqCZPwp22RK4rY2g3CufScqWgygbznsZrn1C8Dehrgetvv219VVtKyuRobWCkckM38UmA81dWadeOaYfqWW=s728)

**谍报**是一种网络数据包嗅探器，拦截通过接口传递的大量数据。该工具允许用户运行正常和详细的流量分析，显示实时流量，揭示数据包方向、协议、标志等。间谍活动也可以欺骗 ARP，因此目标发送的所有数据都会通过攻击者(MiTM)重定向。间谍支持 IPv4、TCP/UDP、ICMP 和 HTTP。间谍软件是用 Python 3.8 编写的，但它也支持 3.6 版本。这是该工具的第一个版本，所以如果你想帮助贡献和增加更多的间谍活动，请联系开发者。注意:这不是 Scapy 包装器，scapylib 只协助 HTTP 请求和 ARP。

## 安装

*   `**git clone https://www.github.com/MandConsultingGroup/Espionage.git**`
*   `**cd Espionage**`
*   `**sudo python3 -m pip install -r requirments.txt**`
*   `**sudo python3 espionage.py --help**`

## 用法

*   `**sudo python3 espionage.py --normal --iface wlan0 -f capture_output.pcap**`
    命令 1 将执行干净的数据包嗅探，并将输出保存到提供的 pcap 文件中。用你的网络接口替换掉`wlan0`。
*   `**sudo python3 espionage.py --verbose --iface wlan0 -f capture_output.pcap**`
    命令 2 将执行更详细(详细)的数据包嗅探，并将输出保存到提供的 pcap 文件中。
*   `**sudo python3 espionage.py --normal --iface wlan0**`
    命令 3 仍然会执行干净的数据包嗅探，但是不会将数据保存到 pcap 文件中。建议保存嗅探。
*   `**sudo python3 espionage.py --verbose --httpraw --iface wlan0**`
    命令 4 将执行详细的数据包嗅探，并且还将以字节显示原始 http/tcp 数据包数据。
*   `**sudo python3 espionage.py --target <target-ip-address> --iface wlan0**`
    命令 5 将 ARP 欺骗目标 ip 地址，所有发送的数据将被路由回攻击者的机器(您/localhost)。
*   `**sudo python3 espionage.py --iface wlan0 --onlyhttp**`
    命令 6 将只显示利用 HTTP 协议在端口 80 上嗅探到的数据包。
*   `**sudo python3 espionage.py --iface wlan0 --onlyhttpsecure**`
    命令 7 将只显示利用 HTTPS(安全)协议在端口 443 上探测到的数据包。
*   `**sudo python3 espionage.py --iface wlan0 --urlonly**`
    命令 8 只会嗅探并返回 victum 访问过的嗅探到的 URL。(与 sslstrip 配合使用效果最佳)。

*   按 Ctrl+C 停止数据包拦截，并将输出写入文件。

## 菜单

**用法:sp 谍. py[-h][–version][-n][-v][-URL][-o][-OHS][-HR][-f FILENAME]-I IFACE
[-t TARGET]
可选参数:
-h，–帮助显示此帮助信息并退出
–version 返回数据包嗅探器版本。
-n，–normal 执行更干净的拦截，不那么复杂。
-v，–verbose(推荐)执行更深入的数据包拦截/嗅探。
-url，–url only 仅使用 http/https 嗅探访问过的 URL。
-o，–only http 只嗅探 tcp/http 数据，返回访问过的 URL。
-ohs，–only http secure
只嗅探 https 数据，(端口 443)。
-hr，–http raw 显示端口 80 上接收或发送的原始数据包数据(字节顺序)。
(推荐)数据输出的参数(。pcap):
-f FILENAME，–FILENAME FILENAME
存储输出的文件名(make 扩展名)。pcap’)。
(必选)执行所需参数:
-i IFACE，–I IFACE
指定网络接口(即。wlan0、eth0、wlan1 等。)
(ARP 欺骗)使用 ARP 欺骗实用程序所需的参数:
-t TARGET，–TARGET TARGET**