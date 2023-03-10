# 斗篷:一种规避审查的工具，以避免被专制国家的对手发现

> 原文：<https://kalilinuxtutorials.com/cloak/>

[![](img/30d1008637c83a9da39e597c77d581d8.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhct6zK-ZqTevs_Jy-Tds6YEuE7Ab8tKHExLqdbvjY7GFNnN3jk2i1X5D7R5NkcIEBcIYqJ8rD9ho-hMby_VrGalTyI5VFaX_CE4rND_eM1inVWZtXgxvFY7RHu5BDBs4WGPSlq2w3CyO1cz5Wz54lThJRgGcpknAwk-wRLJrkMp-QkLSwUcRv3CUOL/s728/logo%20(1).png)

斗篷是一种可插拔的传输工具，它增强了 OpenVPN 等传统代理工具，以逃避复杂的审查和数据歧视。

斗篷不是一个独立的代理程序。相反，它的工作原理是将代理流量伪装成正常的 web 浏览活动。与传统工具相比，传统工具具有非常明显的流量指纹，可以通过简单的过滤规则来阻止，因此很难精确地锁定目标，并且几乎没有误报。这增加了审查行动的附带损害，因为试图屏蔽斗篷也可能损害审查国依赖的服务。

对于任何第三方观察者来说，运行斗篷服务器的主机与一个无辜的 web 服务器是无法区分的。既可以被动地观察进出服务器的流量，也可以主动探测伪装服务器的行为。这是通过使用一系列加密隐写术技术实现的。

斗篷可以与任何通过 TCP 或 UDP 传输流量的代理程序结合使用，如 Shadowsocks、OpenVPN 和 Tor。多个代理服务器可以在同一个服务器主机上运行，而斗篷服务器将充当反向代理，将客户端与其所需的代理端桥接起来。

斗篷通过多个底层 TCP 连接多路传输流量，减少了线路头阻塞并消除了 TCP 握手开销。这也使得流量模式更接近真实网站。

斗篷提供多用户支持，允许多个客户端在同一个端口(默认为 443)上连接到代理服务器。它还提供流量管理功能，如使用信用和带宽控制。这允许代理服务器为多个用户服务，即使底层代理软件不是为多个用户设计的

斗篷还支持通过中间 CDN 服务器(如 Amazon Cloudfront)的隧道。这种服务被广泛使用，试图干扰它们的流量会给审查者带来很高的附带损害。

## 建设

**git 克隆 https://github.com/cbeuw/Cloak
CD 斗篷
去拿。/…
制造**

## 配置

配置文件的例子可以在`**example_config**`文件夹下找到。

### 服务器

`**RedirAdd**r`是传入流量不是来自斗篷客户端时的重定向地址。理想情况下，它应该被设置为审查机构允许的主要网站(例如`**www.bing.com**`)

**`BindAddr`** 是斗篷将绑定并监听的地址列表(例如`**[":443",":80"]**`监听所有接口上的端口 443 和 80)

`**ProxyBook**`是一个对象，其键是客户端使用的 ProxyMethod 的名称(区分大小写)。它的值是一个数组，第一个元素是协议，第二个元素是上游代理服务器的一个`**IP:PORT**`字符串，斗篷将把流量转发到这个服务器。

示例:

**{
" proxy book ":{
" shadow socks ":[
" TCP "，
"localhost:51443"
，
"openvpn": [
"tcp "，
" localhost:12345 "
]
}
}**

是用 base64 编码的静态 curve25519 Diffie-Hellman 私钥。

`**BypassUID**`是没有任何带宽或信用限额限制的授权 uid 列表

`**AdminUID**`是 base64 中 admin 用户的 UID。如果您只将用户添加到`**BypassUID**`中，您可以将其留空。

`**DatabasePath**`是`**userinfo.d**b`的路径，用于存储用户使用信息和限制。如果文件不存在，斗篷将自动创建文件。如果您只向`**BypassUID**`添加用户，您可以将其留空。如果`**AdminUID**`不是有效的 UID 或者为空，这个字段也没有任何作用。

`**KeepAlive**`是告诉操作系统在无活动后，向上游代理服务器发送 TCP KeepAlive 探测之前等待的秒数。零或负值禁用它。默认值为 0(禁用)。

### 客户

你的 UID 是 base64 吗？

**`Transport`** 可以是`**direct**`也可以是`**CDN**`。如果服务器主机希望您直接连接到它，请使用`direct`。如果使用 CDN，使用 **`CDN`。**

是 base64 中的静态 curve25519 公钥，由服务器管理员给出。

`**ProxyMethod**`是您正在使用的代理方法的名称。这必须与服务器的`**ProxyBook**`中的一个条目完全匹配。

`**EncryptionMethod**`是您希望斗篷使用的加密算法的名称。选项有 **`plain`、`aes-256-gcm`** (与 **`aes-gcm`同义)、`aes-128-gcm`** 、`**chacha20-poly1305**`。注意:斗篷不是为了提供传输安全。加密的目的是隐藏代理协议的指纹，并使有效载荷具有统计随机性。**如果您确定您的底层代理工具已经提供了加密和认证(通过 AEAD 或类似的技术)，那么您只能将其保留为`plain`。**

`**ServerName**`是你想让你的 ISP 或防火墙*认为*你正在访问的域名。理想情况下，它应该与服务器配置中的`**RedirAddr**`相匹配，这是审查机构允许的一个主要网站，但这不是必须的。

`**AlternativeNames**`是一个数组，与`**ServerName**`一起使用，为每个新连接在不同的服务器名之间移动。**如果 CDN 提供商禁止域名转发并拒绝替代域名，这可能会与`CDN`传输模式**冲突。

示例:

**{
"ServerName": "bing.com "，
" alternative names ":[" cloud flare . com "，" github.com"]
}**

`**CDNOriginHost**`是`**CDN**`模式下*源*服务器(即运行斗篷的服务器)的域名。这只在 **`Transport`** 设置为`**CDN**`时有效。如果未设置，它将默认为通过命令行参数(在独立模式下)或由 Shadowsocks(在插件模式下)提供的远程主机名。在与 CDN 服务器建立 TLS 会话后，该域名将用于 HTTP 请求中，请求 CDN 服务器与该主机建立 WebSocket 连接。

`**NumConn**`是您想要使用的底层 TCP 连接的数量。默认值 4 应该适合大多数人。设置太高会影响性能。将其设置为 0 将禁用连接多路复用，每个 TCP 连接将产生一个单独的短期会话，该会话将在终止后关闭。这使得它的行为类似于 GoQuiet。这可能对连接不稳定的人有用。

`**BrowserSig**`是您希望**显示**正在使用的浏览器。这与你实际使用的浏览器无关。目前支持`**chrome**`和`**firefox**`。

`**KeepAlive**`是告诉操作系统在无活动后，向斗篷服务器发送 TCP KeepAlive 探测之前等待的秒数。零或负值禁用它。默认值为 0(禁用)。警告:启用它可能会使您的服务器作为代理更容易被检测到，但它会使斗篷客户端更快地检测到互联网中断。

`**StreamTimeout**`是等待来自代理程序的传入连接发送任何数据的秒数，在此之后，连接将被斗篷关闭。在 TCP 连接建立后，斗篷不会强制 TCP 连接超时。

## 设置

### 服务器

*   至少安装一个底层代理服务器(例如 OpenVPN、Shadowsocks)。
*   下载最新版本或克隆并构建这个 repo。
*   运行`**ck-server -key**`。**公钥**应该给用户，**私钥**应该保密。
*   (如果您只想添加不受限制的用户，请跳过)运行 **`ck-server -uid`。**新的 UID 将被用作`A**dminUID**`。
*   将 example_config/ckserver.json 复制到所需位置。将`**PrivateKey**`更改为您刚刚获得的私钥；将 **`AdminUID`** 更改为您刚刚获得的 UID。
*   配置底层代理服务器，使它们都在本地主机上侦听。相应地在配置文件中编辑`**ProxyBook**`
*   配置代理程序。运行`**sudo ck-server -c <path to ckserver.json>**`。ck-server 需要 root 权限，因为它绑定到一个编号较低的端口(443)。或者，您可以遵循 https://superuser.com/a/892391 来避免不必要地授予 ck-server root 权限。

#### 添加用户

无限制用户

运行`**ck-server -uid**`并将 UID 添加到`c**kserver.json**`中的`**BypassUID**`字段

##### 受带宽和信用控制的用户

*   首先确保您已经在 **`ckserver.json`、**中生成并设置了`**AdminUID**`，以及一个到`**DatabasePath**`中的`**userinfo.db**`的路径(如果这个文件还不存在的话，斗篷会为您创建这个文件)。
*   在您的客户端上，运行`**ck-client -s <IP of the server> -l <A local port> -a <AdminUID> -c <path-to-ckclient.json>**`进入管理模式
*   访问 https://cbeuw.github.io/Cloak-panel(注意:这是一个纯 js 静态站点，没有后端，所有输入到该站点的数据都在您的浏览器和您指定的斗篷 API 端点之间进行处理。或者，你可以在 https://github.com/cbeuw/Cloak-panel 下载回购协议，并在浏览器中打开`**index.html**`。不需要网络服务器)。
*   输入 **`127.0.0.1:<the port you entered in step 1>`** 作为 API 基，点击`**List**`。
*   您可以通过点击`+`面板添加更多用户

注意:用户数据库是持久的，因为它在磁盘中。每次启动 ck-server 时，您不需要再次添加用户。

### 客户

**安卓客户端在此可用:https://github.com/cbeuw/Cloak-android**

*   安装与服务器相应的底层代理客户端。
*   下载最新版本或克隆并构建这个 repo。
*   从服务器管理员处获取公钥和您的 UID
*   将`**example_config/ckclient.json**`复制到您选择的位置。输入你获得的`**UID**`和`**PublicKey**`。将`ProxyMethod`设置为与服务器端`**ProxyBook**`中的相应条目完全匹配
*   配置代理程序。运行`**ck-client -c <path to ckclient.json> -s <ip of your server>**`

[**Download**](https://github.com/cbeuw/Cloak)