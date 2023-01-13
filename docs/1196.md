# SSF:安全插座漏斗网络工具

> 原文：<https://kalilinuxtutorials.com/ssf-secure-socket-funneling/>

[![SSF : Secure Socket Funneling Network Tool](img/6aabd3cc75f0bb75f30a9d5fba808232.png "SSF : Secure Socket Funneling Network Tool")](https://1.bp.blogspot.com/-dy1VBWvSPww/XllexvQ6DbI/AAAAAAAAFK4/_r1lVEMnMdQhSVjRzg2PSgAKi1NnnbBVQCLcBGAsYHQ/s1600/Secure%2BSocket%2BFunneling-svg%25281%2529.png)

**安全套接字漏斗(SSF)** 是一个网络工具和工具包。它提供了简单有效的方法，通过一个安全的 TLS 隧道将数据从多个套接字(TCP 或 UDP)转发到远程计算机。

它是跨平台的(Windows，Linux，OSX ),作为独立的可执行文件。

**特性**

*   本地和远程 TCP 端口转发
*   本地和远程 UDP 端口转发
*   本地和远程 SOCKS 服务器
*   通过套接字的本地和远程外壳
*   存档原件
*   本地中继协议
*   最强密码套件的 TLS 连接

**如何使用？**

**命令行**

**客户端**

用法:`**ssf[.exe] [options] server_address**`

选项:

*   `**-v verbose_level**`:Verbosity:critical | error | warning | info | debug | trace(默认值:info)
*   `**-q**`:安静模式。不要打印日志
*   `**-p port**`:远程端口(默认:8011)
*   `**-c config_file_path**`:指定配置文件。如果未设置，则从当前工作目录加载“config.json”
*   `**-m attempts**`:停止前最大不成功连接尝试次数(默认值:1)
*   `**-t delay**`:尝试重新连接前等待的时间，以秒为单位(默认值:60)
*   **`-n`** :如果连接中断，不要尝试重新连接客户端
*   `**-g**`:允许网关端口。允许客户端将服务的本地套接字绑定到特定地址，而不是“本地主机”
*   `**-S**`:显示微服务状态(开/关)

服务选项:

*   `**-D [[bind_address]:]port**`:在本地端的`**[[bind_address]:]port**`上可访问的服务器上运行 SOCKS 代理
*   `**-F [[bind_address]:]port**`:在本地主机上运行一个 SOCKS 代理，可以从`**[[bind_address]:]port**`上的服务器访问
*   `**-X [[bind_address]:]port**`:将服务器 shell I/O 转发到本地指定端口。每个连接都会创建一个新的 shell 进程
*   `**-Y [[bind_address]:]port**`:将本地 shell I/O 转发到服务器上的指定端口
*   **`-L [[bind_address]:]port:host:hostport`** :将本地主机上`**[[bind_address]:]port**`的 TCP 连接转发到服务器上的`**host:hostport**`
*   `**-R [[bind_address]:]port:host:hostport**`:将到服务器上`**[[bind_address]:]port**`的 TCP 连接转发到本地的`**host:hostport**`
*   `**-U [[bind_address]:]port:host:hostport**`:将 **`[[bind_address]:]port`上的本地 UDP 流量转发到服务器上的`host:hostport`**
*   `**-V [[bind_address]:]port:host:hostport**`:将服务器上`**[[bind_address]:]port**`的 UDP 流量转发到本地的`**host:hostport**`

**服务器**

用法:`**ssfd[.exe] [options]**`

**选项:**

1.  **`-v verbose_level` :** 详细程度:严重|错误|警告|信息|调试|跟踪(默认:信息)
2.  **`-q` :** 安静模式。不要打印日志
3.  **`-c config_file_path` :** 指定配置文件。如果未设置，则从当前工作目录加载“config.json”
4.  **`-p port` :** 本地端口(默认:8011)
5.  **`-R` :** 服务器只会中继连接
6.  **`-l host` :** 设置服务器绑定地址
7.  **`-g` :** 允许网关端口。允许客户端将服务的本地套接字绑定到特定地址，而不是“本地主机”
8.  **`-S` :** 显示微服务状态(开/关)

*   **复制**

必须在客户端和服务器配置文件上启用复制功能:

{
"ssf": {
"服务":{
"复制":{ "启用":真}
}
}
}

**用法:** `**ssfcp[.exe] [options] [host@]/absolute/path/file [[host@]/absolute/path/file]**`

**选项:**

*   `**-v verbose_level**`:Verbosity:critical | error | warning | info | debug | trace(默认值:info)
*   `**-q**`:安静模式。不要打印日志
*   `**-c config_file_path**`:指定配置文件。如果未设置，则从当前工作目录加载“config.json”
*   `**-p port**`:远程端口(默认:8011)
*   `**-t**`:使用标准输入作为输入
*   `**--resume**`:如果目标文件存在，尝试恢复文件传输
*   `**--check-integrity**`:传输结束时检查文件完整性
*   `**-r**`:递归复制文件
*   `**--max-transfers arg**`:最大并行传输数(默认为 1)

**也读作-[Dnssearch:一个子域枚举工具](https://kalilinuxtutorials.com/dnssearch/)**

**例题**

**客户端**

客户端将在端口 9000 上运行 SOCKS 代理，并将连接请求传输到服务器 **192.168.0.1:8000**

**ssf -D 9000 -c 配置. json -p 8000 192.168.0.1**

*   **服务器**

服务器将被绑定到所有网络接口上的端口 **8011**

**ssfd**

服务器将被绑定到 **192.168.0.1:9000**

ssfd -p 9000 -l 192

*   **将本地文件复制到远程文件系统**

ssfcp [-c 配置文件] [-p 端口]path/to/file host @ absolute/path/directory _ destination
ssfcp[-c 配置文件] [-p 端口]path/to/file * host @ absolute/path/directory _ destination
ssfcp[-c 配置文件] [-p 端口]-r path/to/dir host @ absolute/path/directory _ destination

*   **从标准输入到远程文件系统的管道文件**

data_in_stdin | ssfcp [-c 配置文件] [-p 端口] -t 主机@路径/到/目的地/文件目的地

*   **将远程文件复制到本地文件系统:**

ssfcp [-c 配置文件] [-p 端口]远程主机@路径/到/文件绝对/路径/目录目的地

ssfcp [-c 配置文件] [-p 端口]远程主机@路径/到/文件*绝对/路径/目录目的地

ssfcp [-c 配置文件] [-p 端口] -r 远程主机@路径/到/目录绝对/路径/目录目的地

**配置文件**

{
"ssf": {
"arguments ":"，
"circuit": []，
"http_proxy": {
"host ":"，
"port ":"，
"user_agent ":"，
" credentials ":{
" username ":"，
"password ":"，
"domain ":"，
"reuse_ntlm": true，
" reuse _ neg "。/certs/trusted/ca.crt "，
"cert_path ":"。/certs/certificate.crt "，
"key_path ":"。/certs/private.key "，
"key_password ":" "，
"dh_path ":"。/certs/dh4096.pem "、
" cipher _ alg ":" DHE-RSA-AES 256-GCM-sha 384 "
}、
"服务":{
"数据报 _ 转发器":{ "启用":true }、
"数据报 _ 侦听器":{
"启用":true、
"网关 _ 端口":false
}、
"流 _ 转发器":{ "启用":enable

**自变量**

| 配置密钥 | 描述 |
| --- | --- |
| 争论 | 使用配置参数代替给定的 CLI 参数(除了`-c`) |

**`arguments`** 键允许用户在配置文件中自定义命令行参数。此功能是保存不同客户端连接配置文件的便捷方式。

给定以下配置文件`**conf.json**`:

{
" SSF ":{
" arguments ":" 10 . 0 . 0 . 1-p 443-D 9000-L 11000:localhost:12000-v debug "
}
}

SSF 将提取给定的参数，并用它们替换初始参数(除了`**-c**`)。

例如，`**ssf -c conf.json**`将等同于 **`ssf 10.0.0.1 -p 443 -D 9000 -L 11000:localhost:12000 -v debug` :**

*   连接到 **`10.0.0.1:443` ( `10.0.0.1 -p 443` )**
*   启动 SOCKS 服务(`**-D 9000**`)
*   启动 TCP 端口转发服务(`**-L 11000:localhost:12000**`)
*   将详细级别设置为调试(`**-v debug**`)

**电路**

| 配置密钥 | 描述 |
| --- | --- |
| 电路 | 用于建立与远程服务器连接的中继链服务器 |

该电路是一个 JSON 数组，包含用于建立连接的反弹服务器和端口。它们列举如下:

{
"ssf": {
"电路":[
{ "主机":"服务器 1 "，"端口":"端口 1 "，
{ "主机":"服务器 2 "，"端口":"端口 2 "，
{ "主机":"服务器 3 "，"端口":"端口 3 " }
]
}
}

此配置将创建以下连接链:

**客户端- >服务器 1:端口 1 - >服务器 2:端口 2 - >服务器 3:端口 3 - >目标**

**代理**

SSF 通过以下方式支持连接:

*   使用`CONNECT` HTTP 方法的 HTTP 代理
*   SOCKS 代理(v4 或 v5)

**HTTP 代理**

| 配置密钥 | 描述 |
| --- | --- |
| http _ 代理服务器.主机 | HTTP 代理主机 |
| http_proxy.port | HTTP 代理端口 |
| http_proxy.user_agent | HTTP 连接请求中的用户代理标头值 |
| http_proxy.credentials .用户名 | 代理用户名凭据(所有平台:基本或摘要，Windows: NTLM 和协商，如果重用=假) |
| http_proxy.credentials .密码 | 代理密码凭据(所有平台:基本或摘要，Windows: NTLM 和协商，如果重用=假) |
| http_proxy.credentials.domain | 用户域(仅限 Windows 上的 NTLM 和协商授权) |
| http _ proxy . credentials . reuse _ NTLM | 重新使用当前计算机用户凭据通过代理 NTLM 身份验证(SSO)进行身份验证 |
| http _ proxy . credentials . reuse _ kerb | 重新使用当前计算机用户凭据(Kerberos 票证)通过代理协商身份验证(SSO)进行身份验证 |

支持的身份验证方案:

*   基础
*   摘要
*   NTLM(仅限 Windows)
*   与 Kerberos 协商(重用计算机用户凭据)

**SOCKS 代理**

| 配置密钥 | 描述 |
| --- | --- |
| socks_proxy .版本 | 袜子版本(4 或 5) |
| socks_proxy .主机 | SOCKS 代理主机 |
| socks_proxy.port | SOCKS 代理端口 |

不支持身份验证方案。

**TLS**

##### 使用外部文件

| 配置密钥 | 描述 |
| --- | --- |
| tls.ca 证书路径 | CA 证书文件的相对或绝对文件路径 |
| tls .证书路径 | 实例证书文件的相对或绝对文件路径 |
| tls.key_path | 私钥文件的相对或绝对文件路径 |
| tls.key_password | 密钥密码 |
| tls.dh_path | Diffie-Hellman 文件的相对或绝对文件路径(仅限服务器) |
| tls .密码 _ 算法 | 密码算法 |

使用默认选项时，以下文件和文件夹应该位于客户端或服务器的工作目录中:

*   **T2`./certs/dh4096.pem`**
*   **T2`./certs/certificate.crt`**
*   **T2`./certs/private.key`**
*   **T2`./certs/trusted/ca.crt`**

其中:

*   **dh4096.pem** 包含 Diffie-Hellman 参数([生成 dh 参数](https://github.com/securesocketfunneling/ssf#generating-diffie-hellman-parameters))
*   **certificate.crt** 和 **private.key** 是 SSF 服务器或客户端的证书和私钥([生成证书](https://github.com/securesocketfunneling/ssf#generating-a-certificate-signed-with-the-ca-and-its-private-key)
*   **ca.crt** 是 SSF 服务器或客户端信任的证书的串联列表([生成 CA](https://github.com/securesocketfunneling/ssf#generating-a-self-signed-certification-authority-ca)

如果您希望这些文件位于不同的路径，可以通过 TLS 路径键对它们进行自定义:

{
" SSF ":{
" TLS ":{
" ca _ cert _ path ":"。/certs/trusted/ca.crt "，
"cert_path ":"。/certs/certificate.crt "，
"key_path ":"。/certs/private.key "、
"key_password ":"、
"dh_path ":"。/certs/dh4096.pem "，
" cipher _ alg ":" DHE-RSA-AES 256-GCM-sha 384 "
}
}
}

**仅使用配置文件**

| 配置密钥 | 描述 |
| --- | --- |
| tls.ca 证书缓冲区 | PEM 格式的 CA 证书文件内容(数据和 PEM 页眉/页脚之间的⚠️ `\n`) |
| tls.cert _ buffer | PEM 格式的实例证书文件内容(数据和 PEM 页眉/页脚之间的⚠️ `\n`) |
| tls.key _ 缓冲区 | PEM 格式的私钥文件内容(数据和 PEM 页眉/页脚之间的⚠️ `\n`) |
| tls.key_password | 密钥密码 |
| tls.dh_buffer | PEM 格式的 Diffie-Hellman 参数文件内容(数据和 PEM 页眉/页脚之间的⚠️ `\n`,仅服务器) |
| tls .密码 _ 算法 | 密码算法 |

您可以使用**、`tls.cert_buffer`、`tls.key_buffer`、**和`**tls.dh_buffer**`键将 TLS 参数直接集成到配置文件中。

{
" SSF ":{
" TLS ":{
" ca _ cert _ buffer ":"——开始证书——\ n……\ n——结束证书—",
" cert _ buffer ":"——开始证书——\ n……\ n——结束证书—“，
" KEY _ buffer ":"——开始 RSA 私钥———\ n……\ n——结束 RSA 私钥—”,
" KEY _ KEY _ 1

证书、私钥和 DH 参数必须采用 PEM 格式。数据和 PEM 页眉/页脚之间的⚠️ `\n`是必需的。

**微服务**

| 配置密钥 | 描述 |
| --- | --- |
| 服务。*.使能够 | 启用/禁用微服务 |
| 服务。*.网关 _ 端口 | 启用/禁用网关端口 |
| services.shell.path | 用于创建外壳的二进制路径 |
| services.shell.args | 用于创建 shell 的二进制参数 |

SSF 的功能是使用微服务(TCP 转发、远程 SOCKS 等)构建的

共有 7 种微服务:

*   流转发器
*   流 _ 监听器
*   数据报 _ 转发器
*   数据报 _ 监听器
*   复制
*   袜子
*   壳

每个特征是至少一个客户端微服务和一个服务器端微服务的组合。

下表总结了每个功能的组装方式:

| ssf 特征 | 微服务客户端 | 微服务服务器端 |
| --- | --- | --- |
| `-L` : TCP 转发 | 流 _ 监听器 | 流转发器 |
| `-R`:远程 TCP 转发 | 流转发器 | 流 _ 监听器 |
| `-U` : UDP 转发 | 数据报 _ 监听器 | 数据报 _ 转发器 |
| `-V`:远程 UDP 转发 | 数据报 _ 转发器 | 数据报 _ 监听器 |
| `-D`:袜子 | 流 _ 监听器 | 袜子 |
| `-F`:遥控袜子 | 袜子 | 流 _ 监听器 |
| `-X`:外壳 | 流 _ 监听器 | 壳 |
| `-Y`:远程外壳 | 壳 | 流 _ 监听器 |

这种架构使得构建远程特性变得更加容易:它们使用相同的微服务，但是在相反的一侧。

`ssf`和`ssfd`带有预启用的微服务。以下是默认的微服务配置:

{
" SSF ":{
" services ":{
" datagram _ forwarder ":{ " enable ":true }、
" datagram _ listener ":{ " enable ":true }、
" stream _ forwarder ":{ " enable ":true }、
" stream _ listener ":{ " enable ":true }、
"socks": { "enable": true }、
"copy": { "enable": false }、
"shell": { "enable": false } 【T

要启用或禁用微服务，将`enable`键设置为`true`或`false`。

尝试使用需要禁用微服务的功能将导致错误消息。

**如何为 TLS 连接生成证书**

**手动**

*   **生成 Diffie-Hellman 参数**

OpenSSL DH param 4096-out form PEM-out DH 4096 . PEM

*   **生成自签名认证机构(CA)**

首先，创建一个名为 *extfile.txt* 的文件，其中包含以下几行:

[v3 _ req _ p]
basic constraints = CA:FALSE
key usage =不可否认，数字签名，密钥加密

然后，生成一个自签名证书(CA) *ca.crt* 及其私钥 *ca.key* :

OpenSSL req-x509-nodes-new key RSA:4096-key out ca . key-out ca . CRT-days 3650

*   **生成私钥和证书(用 CA 签名)**

生成私钥 private.key 和证书签名请求 certificate.csr:

OpenSSL req-new key RSA:4096-nodes-key out private . key-out certificate . CSR

通过用 CA (ca.crt，ca.key)签署 CSR 来生成证书(certificate.pem):

OpenSSL x509-extfile extfile . txt-extensions v3 _ req _ p-req-sha1-days 3650-CA CA . CRT-CAkey CA . key-cacreate serial-in certif

[**Download**](https://github.com/securesocketfunneling/ssf)