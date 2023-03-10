# Rathole:一种轻量级、稳定、高性能的 NAT 穿越反向代理

> 原文：<https://kalilinuxtutorials.com/rathole/>

[![](img/b3c928e7a54a44e31bfa887daf922852.png)](https://blogger.googleusercontent.com/img/a/AVvXsEjDvrtR5hj1fYOuhfiKZqi8xoDy71PkwKzUp0b84o838UYKSshdZYJWJlxeyn6rHvRdR6IjQWuJERUtTSqqWp-9S4q2duTAFIdzLqxN3Vp7BdVlQxF9bwYQOQ0lh7suVGUlWUZv0DOyoMxXhlmy9bYdXKrMnlSjnG1L4JXp4P9EqsWU3vU_8YUcVcQt=s728)

**Rathole** 与 frp 和 ngrok 一样，可以通过具有公共 IP 的服务器，帮助将 NAT 后的设备上的服务暴露给互联网。

## 特性

*   **高性能**可以实现比 frp 高得多的吞吐量，并且在处理大量连接时更加稳定。参见基准测试
*   **低资源消耗**消耗的内存比同类工具少得多。参见基准测试。该二进制文件可以**小到大约 500 千磅**，以适应设备的限制，比如路由器这样的嵌入式设备。
*   **安全**服务的令牌是强制性的，并且是基于服务的。服务器和客户端负责自己的配置。通过可选的噪声协议，可以轻松配置加密。无需创建自签名证书！也支持 TLS。
*   **热重装**可以通过热重装配置文件来动态添加或删除服务。HTTP API 是 WIP。

## 快速入门

一个全动力的`**rathole**`可以从发布页面获得。或者为其他平台从源代码**构建并最小化二进制代码**。Docker 图像也是可用的。

**`rathole`** 的用法和玻璃钢很像。如果你有后者的经验，那么配置对你来说是非常容易的。唯一的区别是服务的配置分为客户端和服务器端，并且令牌是必需的。

要使用`**rathole**`，你需要一个有公共 IP 的服务器，和一个在 NAT 后面的设备，在那里一些服务需要暴露给互联网。

假设您在家里的 NAT 后面有一个 NAS，并希望将其 ssh 服务公开给互联网:

1.  在具有公共 IP 的服务器上

用以下内容创建 **`server.toml`** ，并根据自己的需要进行调整。

**server.toml
【服务器】
bind _ addr = " 0 . 0 . 0 . 0:2333 " #`2333`指定 rathole 监听客户端的端口
【server . services . my _ nas _ ssh】
Token = " use _ a _ secret _ that _ only _ you _ know " #令牌，用于对服务的客户端进行身份验证。更改为任意值。
bind _ addr = " 0 . 0 . 0 . 0:5202 " #`5202`指定将`my_nas_ssh`暴露给互联网**的端口

然后运行:

**。/rathole server.toml**

2.  在 NAT 后面的主机上(您的 NAS)

使用以下内容创建`**client.toml**`，并根据您的需要进行调整。

# 客户，toml

**【客户端】
remote _ addr = " my server . com:2333 " #服务器的地址。端口必须与`server.bind_addr`** 中的端口相同

**【client . services . my _ nas _ ssh】
token = " use _ a _ secret _ that _ only _ you _ know " #必须与服务器相同才能通过验证
local_addr = "127.0.0.1:22" #需要转发的服务的地址**

3.  现在，客户端将尝试在端口`**2333**`上连接到服务器`m**yserver.com**`，任何去往`**myserver.com:5202**`的流量都将被转发到客户端的端口`**22**`。

因此，您可以通过 ssh 连接到您的 NAS。

要在 Linux 上作为后台服务运行`**rathole**`,请查看 systemd 示例。

## 配置

`**rathole**`可以根据配置文件的内容，自动确定在服务器模式或客户端模式下运行，前提是`**[server]**`和`**[client]**`块中只有一个存在，如快速入门中的示例。

但是`**[client]**`和`[**server]**`块也可以放在一个文件中。然后在服务器端运行`**rathole --server config.toml**`，在客户端运行`**rathole --client config.toml**`，明确告诉`**rathole**`运行模式。

在阅读完整的配置规范之前，建议浏览一下配置示例，对配置格式有所了解。

有关加密和`**transport**`块的更多细节，请参见传输。

这是完整的配置规格

**【客户端】
remote _ addr = " example . com:2333 " #必要。服务器的地址
default _ token = " default _ token _ if _ not _ specify " #可选。服务的默认令牌，如果它们没有定义自己的令牌
heartbeat_timeout = 40 #可选。设置为 0 可禁用应用层心跳测试。该值必须大于`server.heartbeat_interval`。默认值:40 秒
[client.transport] #整个块是可选的。指定使用哪种传输方式
type = "tcp" #可选。可能的值:["tcp "，" tls "，" noise"]。默认:" TCP "
[client . transport . TCP]#可选。也影响`noise`和`tls`proxy = " socks 5://user:passwd @ 127 . 0 . 0 . 1:1080 " #可选。用于连接到服务器的代理。`http`和`socks5`是支持的。nodelay = false #可选。确定是否启用 TCP_NODELAY(如果适用),以改善延迟但降低带宽。默认值:false
keepalive_secs = 20 #可选。如果适用，在`tcp(7)`中指定`tcp_keepalive_time`。默认值:20 秒
keepalive_interval = 8 #可选。如果适用，在`tcp(7)`中指定`tcp_keepalive_intvl`。默认:8 秒
[client.transport.tls] #如果`type`是" TLS "
trusted _ root = " ca . PEM " #必需。签署服务器证书的 CA 的证书
hostname = "example.com" #可选。客户端用来验证证书的主机名。如果没有设置，回退到`client.remote_addr`
【client . transport . Noise】# Noise 协议。更多解释见`docs/transport.md`
pattern = " Noise _ NK _ 25519 _ ChaChaPoly _ Blake 2s " #可选。默认值如图
local _ private _ key = " key _ encoded _ in _ base64 " # Optional
remote _ public _ key = " key _ encoded _ in _ base64 " # Optional
[client . services . service 1]#需要转发的服务。名称`service1`可以任意更改，只要与服务器配置中的名称相同
type = "tcp" #可选。需要转发的协议。可能的值:["tcp "，" udp"]。默认:" tcp"
token = "whatever" #如果`client.default_token`未设置
local _ addr = " 127 . 0 . 0 . 1:1081 " #必需。需要转发的服务的地址
nodelay = false #可选。确定是否为数据传输启用 TCP_NODELAY(如果适用),以改善延迟但降低带宽。默认:false
【client . services . service 2】#可以定义多个服务
local _ addr = " 127 . 0 . 0 . 1:1082 "
【服务器】
bind_addr = "0.0.0.0:2333" #必要。服务器监听客户端的地址。通常只有端口需要改变。
default _ token = " default _ token _ if _ not _ specify " #可选
heartbeat_interval = 30 #可选。两次应用层心跳之间间隔。设置为 0 将禁用发送心跳。默认:30 秒
【server . transport】#同`[client.transport]`
type = " TCP "
【server . transport . TCP】#同客户端
nodelay = false
keepalive _ secs = 20
keepalive _ interval = 8
【server . transport . TLS】#必要时`type`为" TLS "
pkcs12 = " identify . pfx " #必要时。服务器证书的 pkcs12 文件和私钥
pkcs12 _ password = " password " #必需。pkcs12 文件的密码
[server . transport . Noise]# Same as`[client.transport.noise]`
pattern = " Noise _ NK _ 25519 _ chacha poly _ Blake 2s "
local _ private _ key = " key _ encoded _ in _ base64 "
remote _ public _ key = " key _ encoded _ in _ base64 "
【server . services . service 1】#服务名必须与客户端的名称一致
type = "tcp" #同客户端`[client.services.X.type] token = "whatever" # Necessary if`server . default _ token ` not set
bind _ addr = " 0 . 0 . 0 . 0:8081 " #必需。服务的地址公开在。通常只有端口需要改变。nodelay = false #可选。同客户端
【server . services . service 2】
bind _ addr = " 0 . 0 . 0 . 1:8082 "**

### 记录

`**rathole**`和很多其他 Rust 程序一样，使用环境变量来控制日志级别。`**info**`、**、**、**、`error`、`debug`、`trace`、**皆可。

**RUST _ LOG =错误。/rathole config.toml**

## 基准

rathole 的延迟与 frp 相似，但可以处理更多的连接，提供更大的带宽，使用更少的内存。

有关更多详细信息，请参见单独的页面基准。

**但是，不要从这里就认为`rathole`可以神奇地让你转发的服务比以前快好几倍。**基准测试是在本地回环上完成的，表示任务受 cpu 限制时的性能。如果网络不是瓶颈，人们可以获得相当大的改善。不幸的是，对于许多用户来说，情况并非如此。在这种情况下，主要好处是降低资源消耗，而带宽和延迟可能不会明显改善。

## 发展状况

正在积极开发中。大量功能即将推出:

*   TLS 支持
*   UDP 支持
*   热重装
*   用于配置的 HTTP APIs

[Download](https://github.com/rapiz1/rathole)