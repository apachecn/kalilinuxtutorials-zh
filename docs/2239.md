# 碰撞:围棋中基于规则的隧道

> 原文：<https://kalilinuxtutorials.com/clash-2/>

[![](img/5994687bf5b94209b31840a346a12f30.png)](https://blogger.googleusercontent.com/img/a/AVvXsEjlNAwSyfX9PzzHkEzAeCmGYzK-HEDWwFyKjUQWbbwDWamyN0koz4yrbj1PeYJkKvMzORuQFCgjQDY4kyUZV6kL2hWfga4htsriEabhg_6VSDp0LZMDBCHXLbNOB_5Y6ISG8pY04quq4gXyObMjqbLg17oKLuoX16iJXEt4x-US-CBVM-AqbXoIZVgL=s728)

Clash 是一个工具，就像围棋中基于规则的隧道

**特性**

*   支持身份验证的本地 HTTP/HTTPS/SOCKS 服务器
*   VMess，Shadowsocks，特洛伊木马，Snell 协议支持远程连接
*   内置 DNS 服务器，旨在最小化 DNS 污染攻击影响，支持 DoH/DoT 上行和假 IP。
*   基于域、GEOIP、IPCIDR 或进程的规则将数据包转发到不同的节点
*   远程组允许用户实施强大的规则。支持自动回退、负载平衡或基于延迟自动选择节点
*   远程提供者，允许用户远程获取节点列表，而不是在配置中硬编码
*   Netfilter TCP 重定向。使用`**iptables**`在您的互联网网关上部署 Clash。
*   全面的 HTTP RESTful API 控制器

**高级功能**

*   macOS、Linux 和 Windows 上的 TUN 模式。文件
*   通过脚本匹配您的隧道
*   规则提供者

入门指南

**欢迎光临**

欢迎来到 Clash 核心项目(“Clash”)的官方维基页面。目前有两个版本的 Clash:

*   clash:dream acro/clash 发布的软件
*   Clash Premium:源代码封闭的预构建 Clash 二进制文件，支持 TUN 等(免费)

这个 wiki 将涵盖两个版本的 Clash。

该文档仍在工作中。在我们努力改进它并保持其准确性的同时，我们也推荐阅读 https://lancellc.gitbook.io/clash 的作品。

**入门**

你可以从 https://github.com/Dreamacro/clash/releases 获得预先构建的 Clash 二进制文件，也可以在本地构建。
Clash 需要 Golang 1.17 或更高版本。

**$去安装 github.com/Dreamacro/clash@latest**

二进制文件构建在＄GOPATH/bin 下

**$ clash -v**

现在，您可以进入本维基的下一章，我们将在其中介绍 Clash 的配置语法

**简介**

Clash 对配置文件使用 YAML， *YAML 不是标记语言*。YAML 被设计成易于被计算机读取、编写和解释，并且通常用于精确的配置文件。在本章中，我们将介绍 Clash 的常见功能以及如何使用和配置它们。

Clash 通过在本地端打开 HTTP、SOCKS5 或透明代理服务器来工作。当一个请求，比如说一个数据包，进来时，Clash *用 VMess、Shadowsocks、Snell、Trojan、SOCKS5 或 HTTP 协议将数据包路由*到不同的远程服务器(“节点”)。

**所有配置选项**

**Port of HTTP(S) proxy server on the local end
port: 7890
Port of SOCKS5 proxy server on the local end
socks-port: 7891
Transparent proxy server port for Linux and macOS (Redirect TCP and TProxy UDP)
redir-port: 7892
Transparent proxy server port for Linux (TProxy TCP and TProxy UDP)
tproxy-port: 7893
HTTP(S) and SOCKS4(A)/SOCKS5 server on the same port
mixed-port: 7890
authentication of local SOCKS5/HTTP(S) server
authentication:
“user1:pass1”
“user2:pass2”
Set to true to allow connections to the local-end server from
other LAN IP addresses
allow-lan: false
This is only applicable when `allow-lan` is `true`
‘*‘: bind all IP addresses 192.168.122.11: bind a single IPv4 address “[aaaa::a8aa:ff:fe09:57d8]”: bind a single IPv6 address bind-address: ‘*‘
Clash router working mode
rule: rule-based packet routing
global: all packets will be forwarded to a single endpoint
direct: directly forward the packets to the Internet
mode: rule
Clash by default prints logs to STDOUT
info / warning / error / debug / silent
log-level: info
When set to false, resolver won’t translate hostnames to IPv6 addresses
ipv6: false
RESTful web API listening address
external-controller: 127.0.0.1:9090
A relative path to the configuration directory or an absolute path to a
directory in which you put some static web resource. Clash core will then
serve it at `http://{{external-controller}}/ui`.
external-ui: folder
Secret for the RESTful API (optional)
Authenticate by spedifying HTTP header `Authorization: Bearer ${secret}`
ALWAYS set a secret if RESTful API is listening on 0.0.0.0
secret: “”
Outbound interface name
interface-name: en0
fwmark on Linux only
routing-mark: 6666
Static hosts for DNS server and connection establishment (like /etc/hosts)
Wildcard hostnames are supported (e.g. *.clash.dev, *.foo.*.example.com)
Non-wildcard domain names have a higher priority than wildcard domain names
e.g. foo.example.com > *.example.com > .example.com
P.S. +.foo.com equals to .foo.com and foo.com
hosts:
‘*.clash.dev’: 127.0.0.1 ‘.dev’: 127.0.0.1 ‘alpha.clash.dev’: ‘::1’ profile: Store the `select` results in $HOME/.config/clash/.cache set false If you don’t want this behavior when two different configurations have groups with the same name, the selected values are shared store-selected: false persistence fakeip store-fake-ip: true DNS server settings This section is optional. When not present, the DNS server will be disabled. dns: enable: false listen: 0.0.0.0:53 ipv6: false # when the false, response to AAAA questions will be empty These nameservers are used to resolve the DNS nameserver hostnames below. Specify IP addresses only default-nameserver: – 114.114.114.114 – 8.8.8.8 enhanced-mode: redir-host # or fake-ip fake-ip-range: 198.18.0.1/16 # Fake IP addresses pool CIDR use-hosts: true # lookup hosts and return IP record Hostnames in this list will not be resolved with fake IPs i.e. questions to these domain names will always be answered with their real IP addresses fake-ip-filter: – ‘*.lan’
– localhost.ptlogin2.qq.com
Supports UDP, TCP, DoT, DoH. You can specify the port to connect to.
All DNS questions are sent directly to the nameserver, without proxies
involved. Clash answers the DNS question with the first result gathered.
nameserver:
– 114.114.114.114 # default value
– 8.8.8.8 # default value
– tls://dns.rubyfish.cn:853 # DNS over TLS
– https://1.1.1.1/dns-query # DNS over HTTPS
– dhcp://en0 # dns from dhcp
When `fallback` is present, the DNS server will send concurrent requests
to the servers in this section along with servers in `nameservers`.
The answers from fallback servers are used when the GEOIP country
is not `CN`.
fallback:
– tcp://1.1.1.1
If IP addresses resolved with servers in `nameservers` are in the specified
subnets below, they are considered invalid and results from `fallback`
servers are used instead.
IP address resolved with servers in `nameserver` is used when
`fallback-filter.geoip` is true and when GEOIP of the IP address is `CN`.
If `fallback-filter.geoip` is false, results from `nameserver` nameservers
are always used if not match `fallback-filter.ipcidr`.
This is a countermeasure against DNS pollution attacks.
fallback-filter:
geoip: true
geoip-code: CN
ipcidr:
– 240.0.0.0/4
domain:
– ‘+.google.com’
– ‘+.facebook.com’
– ‘+.youtube.com’
Lookup domains via specific nameservers
nameserver-policy:
‘www.baidu.com’: ‘114.114.114.114’
‘+.internal.crop.com’: ‘10.0.0.1’
proxies:
Shadowsocks
The supported ciphers (encryption methods):
aes-128-gcm aes-192-gcm aes-256-gcm
aes-128-cfb aes-192-cfb aes-256-cfb
aes-128-ctr aes-192-ctr aes-256-ctr
rc4-md5 chacha20-ietf xchacha20
chacha20-ietf-poly1305 xchacha20-ietf-poly1305
name: “ss1”
type: ss
server: server
port: 443
cipher: chacha20-ietf-poly1305
password: “password”
# udp: true
name: “ss2”
type: ss
server: server
port: 443
cipher: chacha20-ietf-poly1305
password: “password”
plugin: obfs
plugin-opts:
mode: tls # or http
# host: bing.com
name: “ss3”
type: ss
server: server
port: 443
cipher: chacha20-ietf-poly1305
password: “password”
plugin: v2ray-plugin
plugin-opts:
mode: websocket # no QUIC now
# tls: true # wss
# skip-cert-verify: true
# host: bing.com
# path: “/”
# mux: true
# headers:
# custom: value
vmess
cipher support auto/aes-128-gcm/chacha20-poly1305/none
name: “vmess”
type: vmess
server: server
port: 443
uuid: uuid
alterId: 32
cipher: auto
udp: true
tls: true
# skip-cert-verify: true
# servername: example.com # priority over wss host
# network: ws
# ws-opts:
# path: /path
# headers:
# Host: v2ray.com
# max-early-data: 2048
# early-data-header-name: Sec-WebSocket-Protocol
name: “vmess-h2”
type: vmess
server: server
port: 443
uuid: uuid
alterId: 32
cipher: auto
network: h2
tls: true
h2-opts:
host:
– http.example.com
– http-alt.example.com
path: /
name: “vmess-http”
type: vmess
server: server
port: 443
uuid: uuid
alterId: 32
cipher: auto
# udp: true
# network: http
# http-opts:
# # method: “GET”
# # path:
# # – ‘/’
# # – ‘/video’
# # headers:
# # Connection:
# # – keep-alive
name: vmess-grpc
server: server
port: 443
type: vmess
uuid: uuid
alterId: 32
cipher: auto
network: grpc
tls: true
servername: example.com
# skip-cert-verify: true
grpc-opts:
grpc-service-name: “example”
socks5
name: “socks”
type: socks5
server: server
port: 443
# username: username
# password: password
# tls: true
# skip-cert-verify: true
# udp: true
http
name: “http”
type: http
server: server
port: 443
# username: username
# password: password
# tls: true # https
# skip-cert-verify: true
# sni: custom.com
Snell
# Beware that there’s currently no UDP support yet
name: “snell”
type: snell
server: server
port: 44046
psk: yourpsk
# version: 2
# obfs-opts:
# mode: http # or tls
# host: bing.com
Trojan
name: “trojan”
type: trojan
server: server
port: 443
password: yourpsk
# udp: true
# sni: example.com # aka server name
# alpn:
# – h2
# – http/1.1
# skip-cert-verify: true
name: trojan-grpc
server: server
port: 443
type: trojan
password: “example”
network: grpc
sni: example.com
# skip-cert-verify: true
udp: true
grpc-opts:
grpc-service-name: “example”
name: trojan-ws
server: server
port: 443
type: trojan
password: “example”
network: ws
sni: example.com
# skip-cert-verify: true
udp: true
# ws-opts:
# path: /path
# headers:
# Host: example.com
ShadowsocksR
# The supported ciphers (encryption methods): all stream ciphers in ss
# The supported obfses:
# plain http_simple http_post
# random_head tls1.2_ticket_auth tls1.2_ticket_fastauth
# The supported supported protocols:
# origin auth_sha1_v4 auth_aes128_md5
# auth_aes128_sha1 auth_chain_a auth_chain_b
name: “ssr”
type: ssr
server: server
port: 443
cipher: chacha20-ietf
password: “password”
obfs: tls1.2_ticket_auth
protocol: auth_sha1_v4
# obfs-param: domain.tld
# protocol-param: “#”
# udp: true
proxy-groups:
# relay chains the proxies. proxies shall not contain a relay. No UDP support.
# Traffic: clash <-> http <-> vmess <-> ss1 <-> ss2 <-> Internet
name: “relay”
type: relay
proxies:
– http
– vmess
– ss1
– ss2
url-test select which proxy will be used by benchmarking speed to a URL.
name: “auto”
type: url-test
proxies:
– ss1
– ss2
– vmess1
# tolerance: 150
# lazy: true
url: ‘http://www.gstatic.com/generate_204’
interval: 300
fallback selects an available policy by priority. The availability is tested by accessing an URL, just like an auto url-test group.
name: “fallback-auto”
type: fallback
proxies:
– ss1
– ss2
– vmess1
url: ‘http://www.gstatic.com/generate_204’
interval: 300
load-balance: The request of the same eTLD+1 will be dial to the same proxy.
name: “load-balance”
type: load-balance
proxies:
– ss1
– ss2
– vmess1
url: ‘http://www.gstatic.com/generate_204’
interval: 300
# strategy: consistent-hashing # or round-robin
select is used for selecting proxy or proxy group
you can use RESTful API to switch proxy is recommended for use in GUI.
name: Proxy
type: select
# disable-udp: true
proxies:
– ss1
– ss2
– vmess1
– auto
direct to another infacename
name: en1
type: select
interface-name: en1
proxies:
– DIRECT
name: UseProvider
type: select
use:
– provider1
proxies:
– Proxy
– DIRECT
proxy-providers:
provider1:
type: http
url: “url”
interval: 3600
path: ./provider1.yaml
health-check:
enable: true
interval: 600
# lazy: true
url: http://www.gstatic.com/generate_204
test:
type: file
path: /test.yaml
health-check:
enable: true
interval: 36000
url: http://www.gstatic.com/generate_204
rules:
DOMAIN-SUFFIX,google.com,auto
DOMAIN-KEYWORD,google,auto
DOMAIN,google.com,auto
DOMAIN-SUFFIX,ad.com,REJECT
SRC-IP-CIDR,192.168.1.201/32,DIRECT
optional param “no-resolve” for IP rules (GEOIP, IP-CIDR, IP-CIDR6)
IP-CIDR,127.0.0.0/8,DIRECT
GEOIP,CN,DIRECT
DST-PORT,80,DIRECT
SRC-PORT,7777,DIRECT
RULE-SET,apple,REJECT # Premium only
MATCH,auto**

**指定配置目录**

如果没有另外指定，默认情况下，Clash 在`**$HOME/.config/clash/config.yaml**`读取配置文件。如果不存在，碰撞将生成默认设置。

您可以使用命令行选项`**-d**`来指定一个配置目录:

**$ clash -d . #当前目录
$ clash -d /etc/clash**

您可以使用命令行选项`-f`来指定配置:

**$ clash -f ./config.yaml #当前目录
$ clash-f/etc/clash/config . yam**l

**语法**

*   IPv6 地址应该用`**[**`和`**]**`包装。例如:`**[aaaa::a8aa:ff:fe09:57d8]**`。
*   通配符。请注意，任何包含这些字符的域名都应该用单引号`**'**`括起来。
    *   `*****`:单级通配符。`***.google.com**`匹配`**www.google.com**`但不匹配`**foo.bar.google.com**`。使用`***.*.*.google.com**`是可能的。
    *   `**+**`:多级通配符。`**+.google.com**`匹配`**google.com**`、`**www.google.com**`和`**foo.bar.google.com**`。这和`**DOMAIN-SUFFIX**`的工作原理一模一样。

**DNS**

Clash 附带的 DNS 服务器旨在最大限度地减少 DNS 污染攻击的影响，并提高网络性能。它有两种工作模式:`**redir-host**`和`**fake-ip**`。两者最大的区别在于 IP 地址是如何解析的，连接是如何建立的。

**雷迪尔-主持人**

这更像是代理工作的传统方式。在此模式下，根据`dns.nameserver`、`dns.fallback`和`dns.fallback-filter`中的设置，目的地 FQDN 以几种不同的方式解析。Clash DNS 模块收到的第一个结果将被发送回客户端。然后，客户端可以通过 Clash 建立到所述 IP 地址的连接。

**假 ip**

“假 IP”地址的概念源自 RFC 3089:

“假 IP”地址被用作查找相应“FQDN”信息的密钥。

当一个 DNS 请求被发送到 DNS 服务器时，Clash 在假 IP 地址池中分配一个空闲的*假 IP 地址*，这是一个映射表，管理 FQDN 和“假 IP”地址之间的映射。请注意，假 IP 地址池中的 IP 地址不应用于真实通信。池的默认 CIDR 是保留的 IPv4 地址空间`198.18.0.1/16`，可以在`**dns.fake-ip-range**`中更改。

然后，Clash 将查找 FQDN 并检查 IP 地址的 GEOIP，这仅仅是为了规则(如 GEOIP)。当对所述“假 IP”地址的请求被发送到 Clash 时，Clash 通过 SOCKS5、Shadowsocks(或其他协议)服务器建立到与“假 IP”链接的 FQDN 的连接。

**代理团体**

代理组是可以利用 Clash 的一些特殊功能来管理和利用的代理组。

*   `**relay**`:发送到该代理组的请求将依次通过指定的代理服务器进行中继。目前对此没有 UDP 支持。指定的代理服务器不应包含另一个中继。
*   `**url-test**` : Clash 对列表中的每个代理服务器进行基准测试，通过这些服务器定期向指定的 URL 发送 HTTP HEAD 请求。可以设置最大容许值、基准测试间隔和目标 URL。
*   `**fallback**` : Clash 使用与`**url-test**`相同的机制定期测试列表中服务器的可用性。将使用第一台可用的服务器。
*   `**load-balance**`:对同一个 eTLD+1 的请求将使用同一个代理拨号。
*   【Clash 启动时默认使用第一台服务器。用户可以选择使用 RESTful API 的服务器。在这种模式下，您可以在配置中硬编码服务器或使用代理提供程序。

**代理提供商**

代理提供程序使用户能够动态加载代理服务器列表，而不是将它们硬编码在配置文件中。代理提供者目前有两个来源来加载服务器列表:

*   `**http**` : Clash 在启动时从指定的 URL 加载服务器列表。如果设置了`**interval**`选项，Clash 会定期从远程获取服务器列表。
*   `**file**` : Clash 在启动时从文件系统上的指定位置加载服务器列表。

健康检查在两种模式下都可用，其工作方式与代理组中的`**fallback**`完全一样。服务器列表文件的配置格式在主配置文件中也完全相同:

#**config . YAML
proxy-providers:
provider 1:
type:http
URL:" URL "
interval:3600
path:。/provider1.yaml
健康检查:
enable: true
间隔:600
# lazy:true
URL:http://www.gstatic.com/generate_204
测试:
类型:文件
路径:/test.yaml
健康检查:
enable: true
间隔:36000**
URL:http://www.gstatic.com/generate_204

test.yaml
代理:

*   # **名称:" ss1"
    类型:ss
    服务器:服务器
    端口:443
    密码:chacha20-ietf-poly1305
    密码:" password"
    名称:" ss2"
    类型:ss
    服务器:服务器
    端口:443
    密码:chachacha 20-IETF-poly 1305
    密码:" password"
    插件:obfs
    插件-opt**

**规则**

可用关键字:

*   **`DOMAIN` : `DOMAIN,www.google.com,policy`** 航线只有`**www.google.com**`到 **`policy`。**
*   **`DOMAIN-SUFFIX` : `DOMAIN-SUFFIX,youtube.com,policy`** 路由任何以`**youtube.com**`结尾的 FQDN，例如`**www.youtube.com**`或`**foo.bar.youtube.com**`到`**policy**`。这类似于通配符 **`+`。**
*   **`DOMAIN-KEYWORD` : `DOMAIN-KEYWORD,google,policy`** 路由任何包含`**google**`的 FQDN，例如`**www.google.com**`或`**googleapis.com**`到`**policy**`。
*   **`GEOIP` : `GEOIP,CN,policy`** 将任何到中国 IP 地址的请求路由到`**policy**`。
*   **`IP-CIDR` : `IP-CIDR,127.0.0.0/8,DIRECT`** 将任何到`**127.0.0.0/8**`的数据包路由到`**DIRECT**`策略。
*   `**IP-CIDR6**` : `**IP-CIDR6,2620:0:2d0:200::7/32,policy**`将任何到`**2620:0:2d0:200::7/32**`的数据包路由到`**policy**`。
*   **`SRC-IP-CIDR` : `SRC-IP-CIDR,192.168.1.201/32,DIRECT`** 将任何数据包**从** `**192.168.1.201/32**`路由到`**DIRECT**`策略。
*   **`SRC-PORT` : `SRC-PORT,80,policy`** 将任何数据包**从**端口 80 路由到`**policy**`。
*   `D` **`ST-PORT` : `DST-PORT,80,policy`** 路由任何数据包**到**端口 80 到`**policy**`。
*   **`PROCESS-NAME` : `PROCESS-NAME,nc,DIRECT`** 将流程`**nc**`路由到`**DIRECT**`。(支持 macOS、Linux、FreeBSD 和 Windows)
*   **`MATCH` : `MATCH,policy`** 将剩余的数据包路由到`**policy**`。这条规则是**必选**。

还有两个额外的特殊政策:

*   `**DIRECT**`:直接连接到目标，不涉及任何代理
*   `**REJECT**`:包的黑洞。Clash 不会处理此策略的任何 I/O。

策略可以是 **`DIRECT`、`REJECT`** ，也可以是代理组或代理服务器。

**无解析**

`**no-resolve**`是 **`GEOIP`、`IP-CIDR`或`IP-CIDR6`** 规则的附加选项。将`**,no-resolve**`添加到这些规则中以启用。默认情况下，遇到 IP 规则时，Clash 会将域名转换为 IP 地址。当遇到具有 FQDN 目标的数据包时，Clash 会跳过启用此选项的 IP 规则。

**开发者**

没有以下不可思议的开发人员，就不会有冲突:

*   Dreamacro
*   Beyondkmp
*   Comzyh
*   戴蒙德
*   机器人
*   Kr328

[**Download**](https://github.com/Dreamacro/clash)