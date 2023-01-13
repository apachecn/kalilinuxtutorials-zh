# UDP-Hunter:适用于涵盖 IPv4 和 IPv6 协议的各种 UDP 服务的网络评估工具

> 原文：<https://kalilinuxtutorials.com/udp-hunter/>

[![](img/81361778a3433098a8984a12e96ddedf.png)](https://blogger.googleusercontent.com/img/a/AVvXsEjsNzT6FGzQ9kou1NHo0ajwrC6-rc-3SMxDbidzQCgXJ5G4EpTYEC3sWY4UPb7JbrLIZ-MMscsNNZgfnecYSD7q2v1PaPF01PC39TW8h_ynGbxwySGTe_c-7W0S9Z36B7iKWtZ0la581xw8FbA2f6s1eeo2p48tcH9uampH92JafwnI-qd1RbaL4JQa=s746)

UDP-Hunter 是一个 UDP 扫描一直是一项缓慢而痛苦的工作，如果你在 UDP 上添加 IPv6，工具的选择会非常有限。UDP Hunter 是一个基于 python 的开源网络评估工具，专注于 UDP 服务扫描。使用 UDP Hunter，我们专注于为 IPv6 和 IPv4 主机提供广为人知的 UDP 协议审计。截至目前，UDP Hunter 支持 19 种不同的服务探测。该工具允许您对大型网络进行批量扫描，以及对特定端口进行目标主机扫描等。一旦发现一个开放的服务，UDP Hunter 会更进一步，甚至会指导您如何利用发现的服务。UDP Hunter 以简洁的文本格式提供报告，然而，对更多格式的支持正在进行中。

**UDP Hunter 是如何工作的？**

当向 UDP Hunter 提供任何 IP 范围时，它会创建一个 IP 列表。它还支持将被解析的域名和将被添加到列表中的 IP。一旦 UDP Hunter 在内部创建了列表，它将向所有列出的 IP 发送 UDP 探测。如果主机正在运行 UDP 服务，它会做出响应。UDP Hunter 主要是嗅探网络，特别是 UDP 流量，然后读取所有到达目标主机的 UDP 数据包。将报告运行 UDP Hunter 后收到的所有 UDP 探测器。但是，有一个选项(通过设置–noise = false)可以忽略不相关的 UDP 数据包，只观察来自目标列表中提到的主机和服务/端口的感兴趣的 UDP 流量。创建 UDP Hunter 的想法最初是受 udp-proto-scanner 的启发。我衷心感谢波特卡利斯实验室，也感谢阿南特和苏米特·西达尔特(Sid)在 UDP 亨特工作时提供的宝贵意见。

**支持的 UDP 探针**

从今天起，我们在默认端口上支持以下 UDP 服务探测:

*   ike–500 端口
*   RPC/RPC check–111 端口
*   ntp / NTPRequest – 123 port
*   SNMP-public/SNMP v3 get request–161 端口
*   ms-SQL/ms-SQL-slam–1434 端口
*   正确-6502 个连接埠
*   TFTP–69 端口
*   DB2–523 端口
*   Citrix–1604 端口
*   回声-7 端口
*   chargen–19 端口
*   systat–11 端口
*   白天/时间–13 端口
*   DNS status request/DNS version bindreq–53 端口
*   NBTStat–137 端口
*   xdmcp – 177 port
*   网络支持–5405 端口
*   mdns-zeroconf – 5353 port
*   GTP v1–2123 端口

设置

**要求**

*   Python 3.x
*   Python 模块——在“requirements.txt”文件中也提到了
    *   netaddr
    *   彩色光
    *   抱怨吗
    *   ifaddr
    *   日期时间

这将有助于您进行初始设置:

安装所有需要的模块:pip3 install -r requirements.txt

**所需配置文件**

*   udp . txt–该文件包含 UDP 探测器
*   UDP help . txt–该文件包含工具列表、每个 UDP 探测器或服务的建议

您也可以使用命令行参数来更改配置文件:

“–配置文件”和“–探测帮助”

通过运行以下命令验证配置:

python udp-hunter.py

注意:它应该显示以下帮助细节，如果这抛出任何错误检查您的配置或与我联系任何工具特定的错误。

**功能/选项**

UDP Hunter v0.1beta 具有以下特性:

**强制选项**

*   –主机–单一主机–必需的或
*   –File–IPS 的文件–必填

**Optional**

*   –输出–输出文件–必需
*   –探测器–探测器名称或“全部”(默认:所有探测器)(可选)
    *   探测列表–ike、rpc、ntp、snmp-public、ms-sql、ms-sql-slam、netop、tftp、db2、citrix、echo、chargen、systat、daytime、time、RPCCheck、DNSStatusRequest、DNSVersionBindReq、NBTStat、NTPRequest、SNMPv3GetRequest、xdmcp、net-support、mdns-zeroconf、gtpv1
*   –端口–端口列表或“全部”(默认:所有端口)(可选)
*   –重试次数–发送到每台主机的数据包数量。默认 2(可选)
*   –噪音–过滤未列出 IP 的输出(可选)
*   –verbose–verbosity，也会显示嗅探器输出—请保持此项为真，默认为真。这将有助于我们分析输出。
*   –超时–超时 1.0、2.0 分钟(可选)
*   –lhost 6–为 listner 接口提供 IPv6
*   –lhost 4–提供 listner 接口的 IPv4
*   –config file–配置文件位置–默认为同一目录中的“udp.txt”
*   –probe Help–帮助文件位置–默认为同一目录中的“udphelp.txt”

**用法**

用法:python UDP-hunter . py–file = input file . txt–output = output file . txt[可选参数]用法:python UDP-hunter . py–file = input file . txt–output = output file . txt[–probes = NTPRequest，SNMP v3 getreques][–ports = 123，161，53][–retries = 3][–noise = true][–verbose = false][–time out = 1.0][–config file]

[**Download**](https://github.com/NotSoSecure/udp-hunter)