# Stunner:测试和利用 STUN，TURN 和翻转 TCP 服务器的工具

> 原文：<https://kalilinuxtutorials.com/stunner/>

[![](img/51f67cdd39159e95b1c9a018cb1b3924.png)](https://1.bp.blogspot.com/-p33BS4dO5TA/YOVAj022AzI/AAAAAAAAJ5g/1MUPHEogapM4TL6fotueMZvu3zKQxHvhwCLcBGAsYHQ/s905/scour-demo.png)

**Stunner** 是一个测试和利用 STUN，TURN 和 TURN over TCP 服务器的工具。TURN 是一种主要用于视频会议和音频聊天(WebRTC)的协议。

如果您发现一个错误配置的服务器，您可以使用此工具打开一个本地 socks 代理，它通过 TURN 协议将所有流量中继到服务器后面的内部网络中。

我在 Cisco Expressway 的一次测试中开发了这个工具，该测试导致了一些漏洞:https://fire fart . at/post/multiple _ vulnerability _ Cisco _ Expressway/

要获得所需的用户名和密码，您需要使用带外方法获取它们，例如通过打嗝从 web 浏览器中嗅探连接请求。我在自述文件的底部添加了一个示例工作流，说明如何测试这样的服务器。

# 实施的 RFC

STUN: RFC 5389

转弯:RFC 5766

转向 TCP: RFC 6062

IPv6 的 TURN 扩展:RFC 6156

# 可用命令

## 信息

该命令将打印一些关于 stun 或 turn 服务器的信息，如支持的协议和属性，如使用的软件。

### 选项

**–debug，-d enable debug output(默认:false)
–turnserver value，-s value turn server 以 host:port
的格式连接到–tls 使用 TLS 进行连接(大多数测试为 false)(默认:false)
–超时值连接到 turn server 的超时(默认:1s)
–help，-h show help(默认:false)**

## 例子

**。/stunner info -s x.x.x.x:443**

## 距离扫描

此命令尝试几个私有和受限范围，以查看 TURN 服务器是否配置为允许连接到指定的 IP 地址。如果没有禁止特定的范围，您可以使用提供的其他命令进一步枚举该范围。如果一个 ip 是可到达的，这意味着 TURN 服务器将把流量转发到这个 IP。

### 选项

**–debug，-d enable debug output(默认值:false)
–turnserver 值，-s 值 turn server 要连接到的格式主机:端口
–tls 使用 TLS 进行连接(大多数测试中为 false)(默认值:false)
–协议值连接到 TURN 服务器时要使用的协议。支持的值:tcp 和 udp(默认:“UDP”)
–超时值连接到 turn 服务器的超时(默认:1s)
–用户名值，-u 值 turn 服务器的用户名
–密码值，-p 值 turn 服务器的密码
–help，-h 显示帮助(默认:false)**

### 例子

基于 TCP 的 TURN 连接(来自 TURN 服务器的连接):

**。/击晕器范围-扫描-s x.x.x.x:3478 -u 用户名-p 密码-协议 tcp**

基于 UDP 的 TURN 连接(来自 TURN 服务器的连接):

**。/击晕器范围-扫描-s x.x.x.x:3478 -u 用户名-p 密码-协议 udp**

## 袜子

对于支持 TCP 连接到后端服务器的 TURN 服务器来说，这是最有用的命令之一。它将启动一个没有身份验证的本地 socks5 服务器，并通过 TURN 协议中继所有 TCP 流量(目前不支持通过 socks 的 UDP)。如果服务器配置不当，它会将流量转发到内部地址，因此这可被用来访问内部系统并滥用服务器作为内部网络的代理。如果您选择通过 socks 进行 DNS 查找，它将使用您的本地名称服务器进行解析，因此最好使用私有 IPv4 和 IPv6 地址。请注意，此模块只能中继 TCP 流量。

### 选项

**–debug，-d enable debug output(默认值:false)
–turnserver 值，-s 值 turn server 要连接到的格式主机:端口
–tls 使用 TLS 进行连接(大多数测试中为 false)(默认值:false)
–协议值连接到 TURN 服务器时要使用的协议。支持的值:tcp 和 udp(默认:“UDP”)
–超时值连接到 turn 服务器的超时值(默认:1s)
–用户名值，-u 值 turn 服务器的用户名
–密码值，-p 值 turn 服务器的密码
–监听值，-l 值地址和监听端口(默认:“127 . 0 . 0 . 1:1080”)
–Drop-public，-x 丢弃对公共 IP 的请求。如果目标无法连接到互联网，而您的浏览器希望通过连接来检查 TLS 证书，这将非常方便。(默认:真)
–帮助，-h 显示帮助(默认:假)**

## 例子

**。/尤物袜子-s x.x.x.x:3478 -u 用户名-p 密码-x**

启动代理后，打开浏览器，将设置中的代理指向 ip 为 127.0.0.1:1080 的 socks5(确保不要设置绕过本地地址选项，因为我们希望到达远程本地地址)，并在浏览器中调用您选择的 IP。

例如:https://127.0.0.1、https://127.0.0.1:8443 或 https://[::1]:8443(这些将从本地接口调用被测 TURN 服务器上的端口)。

您还可以配置`**proxychains**`来使用这个代理(但是这会非常慢，因为每个请求都会导致多个请求来启用代理)。只需编辑`**/etc/proxychains.conf**`，在`**ProxyList**`下输入数值`**socks5 127.0.0.1 1080**`。

具有正确配置的代理链的此 socks5 代理上的 nmap 示例(请注意，必须执行 TCP syns，否则它不会使用 socks5 代理)

**sudo proxychains nmap -sT -p 80，443，8443 -sV 127.0.0.1**

## 运输毛额

这很可能不会产生任何有用的信息，但对于枚举服务器支持的所有可用传输(=到内部系统的协议)非常有用。这可能会显示一些自定义协议实现，但大多数情况下只会返回默认值。

### 选项

**–debug，-d enable debug output(默认值:false)
–turnserver 值，-s 值 turn server 要连接到的格式主机:端口
–tls 使用 TLS 进行连接(大多数测试中为 false)(默认值:false)
–协议值连接到 TURN 服务器时要使用的协议。支持的值:tcp 和 udp(默认:“UDP”)
–超时值连接到 turn 服务器的超时(默认:1s)
–用户名值，-u 值 turn 服务器的用户名
–密码值，-p 值 turn 服务器的密码
–help，-h 显示帮助(默认:false)**

**例子**

**。/stunner brute-transports-s x . x . x . x:3478-u 用户名-p 密码**

## 内存泄漏

这种攻击的工作方式如下:服务器把要发送给`**target**`(大多数情况下必须是高端口> 1024)的数据作为 TLV(类型长度值)。这种利用使用一个短值的大长度。如果服务器不检查 TLV 的边界，它可能会通过`**length**`向`**target**`发送一些内存。Cisco Expressway 被证实易受此攻击，但根据 Cisco 的说法，它只泄漏了当前会话的内存。

### 选项

**–debug，-d enable debug output(默认值:false)
–turnserver 值，-s 值 turn server 要连接到的格式主机:端口
–tls 使用 TLS 进行连接(大多数测试中为 false)(默认值:false)
–协议值连接到 TURN 服务器时要使用的协议。支持的值:tcp 和 udp(缺省值:“UDP”)
–超时值连接到 turn 服务器的超时值(缺省值:1s)
–用户名值，-u 值 turn 服务器的用户名
–密码值，-p 值 turn 服务器的密码
–目标值，-t 值主机:端口格式的内存泄漏目标。应该是你控制下的一个公共服务器
–Size value 要泄漏的缓冲区大小(默认值:35510)
–help，-h show help(默认值:false)**

### 例子

为了接收数据，我们需要在一个有公共 ip 的服务器上设置一个接收器。通常，防火墙被配置为只允许来自 TURN 服务器的高端口(> 1024)，因此在连接到互联网时，请确保使用像本例中的 8080 这样的高端口。

sudo NC-u-l-n-v-p 8080 | hex dump-C

然后在您的机器上执行以下语句，将公共 ip 添加到`**t**`参数中

如果可以的话，你应该会看到大量的内存进入，否则你只会看到短消息。

## udp 扫描程序

如果 TURN 服务器允许 UDP 连接到目标，此扫描器可用于扫描所有专用 ip 范围，并向它们发送 SNMP 和 DNS 请求。由于这将检查大量 IP，可能需要几天时间才能完成，因此请谨慎使用或通过参数指定较小的目标。您需要提供将被尝试的 SNMP 社区字符串和将在每个 IP 上解析的域名。例如，对于域名，您可以使用 burp collaborator。

**选项**

–**-debug、-d enable debug output(默认值:false)
–turnserver value、-s value turn server 要连接到的格式主机:端口
–tls 使用 TLS 进行连接(大多数测试为 false)(默认值:false)
–protocol value 连接到 TURN server 时要使用的协议。支持的值:tcp 和 udp(默认:“UDP”)
–超时值连接到 turn 服务器的超时(默认:1s)
–用户名值，-u 值 turn 服务器的用户名
–密码值，-p 值 turn 服务器的密码
–社区字符串值用于扫描的 SNMP 社区字符串(默认:“公共”)
–域值扫描期间在内部 DNS 服务器上解析的域名
–ip 值扫描单个 IP 而不是整个私有范围。如果留空，则扫描所有私有范围。接受单 IPs 或 CIDR 格式。(接受多个输入)
–帮助，-h 显示帮助(默认:假)**

# 示例工作流程

假设您发现了一个使用 WebRTC 的服务，并且想要测试它。

第一步是获得所需的数据。我建议在后台启动 Wireshark，然后通过 Burp 加入一个会议，收集所有 HTTP 和 Websocket 流量。接下来在你的打嗝历史中搜索一些与转身相关的关键词，如**`3478``password``credential`**和`**username**`(一定要检查这些关键词的 websocket 标签)。这可能会暴露 turn 服务器和协议(UDP 和 TCP 端点可能有不同的端口)以及用于连接的凭据。如果您在 burp 中找不到数据，请开始查看 wireshark 来识别流量。如果它在一个非标准端口上(除了 3478 之外的任何端口),在 Wireshark 中通过右击`**STUN**`来解码协议。这应该会向您显示用于连接的用户名，您可以使用此信息来搜索打嗝历史，甚至进一步搜索所需的数据。请注意，Wireshark 不能向您显示密码，因为密码用于散列一些包内容，所以它不能被逆转。

下一步是使用从 burp 获得的正确端口和协议向 turn 服务器发出`**info**`命令。

如果这行得通，下一步就是`**range-scan**`。如果这允许任何流量进入内部系统，您可以进一步利用这一点，但要注意 UDP 只有有限的使用案例。

如果允许 TCP 连接到内部系统，只需启动`**socks**`命令，通过浏览器访问允许的 IPs，并将 socks 代理设置为 127.0.0.1:1080。可以试用 127.0.0.1:443 等 IP 找管理接口。

[**Download**](https://github.com/firefart/stunne)