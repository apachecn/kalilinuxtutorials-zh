# 使用 Powershell 调用 SocksProxy : Socks 代理和反向 Socks 服务器

> 原文：<https://kalilinuxtutorials.com/invoke-socksproxy/>

[![Invoke SocksProxy : Socks Proxy & Reverse Socks Server Using Powershell](img/d5fc66c139bef3799762a93b19d1045b.png "Invoke SocksProxy : Socks Proxy & Reverse Socks Server Using Powershell")](https://1.bp.blogspot.com/-DEBLKNahjW4/YFgwZWwnkwI/AAAAAAAAIn0/jgsQIYLD-mEe9JfzEXZr7I8s4RycHQ6VgCLcBGAsYHQ/s728/Invoke-SocksProxy%25281%2529.png)

**Invoke SocksProxy** 是一个使用 powershell 创建本地或“反向”Socks 代理的工具。本地代理是一个简单的 Socks 4/5 代理。

反向代理通过启动可以通过系统代理的出站 SSL 连接来创建 tcp 隧道。然后，可以将该隧道用作远程主机上的 socks 代理，以连接到本地主机的网络。

**例题**

**本地**

*   **在端口 1080 上创建一个 Socks 4/5 代理:**

**导入-模块。\ Invoke-socks proxy . PS m1
Invoke-socks proxy-bind port 1080**

*   **将最大线程数从 200 增加到 400**

**导入-模块。\ Invoke-socks proxy . PS m1
Invoke-socks proxy-threads 400**

**反转**

**#远程主机:
#生成私钥和自签名证书**
OpenSSL req-x509-nodes-days 365-new key RSA:2048-keyut private . key-out cert . PEM

**#获取证书指纹进行验证:**
OpenSSL x509-in cert . PEM-noout-sha1-fingerprint | cut-d " = "-F2 | tr-d ":

/cert.pem。/private . key

**#本地主机:**
导入-模块。\ Invoke-socks proxy . PS m1
Invoke-reversesocksproy-remote port 443-remote host 192 . 168 . 49 . 130

**#穿越系统代理:**
Invoke-reversesocksproy-remote port 443-remote host 192 . 168 . 49 . 130-useSystemProxy

**#验证证书**
Invoke-reversesockspro

*   **在远程主机的端口 1080 上创建一个“反向”Socks 4/5 代理:**

系统代理技巧的功劳:[https://github . com/Arno 0x/powershell scripts/blob/master/Proxy tunnel . PS1](https://github.com/Arno0x/PowerShellScripts/blob/master/proxyTunnel.ps1)

**限制**

*   这只是 Socks 4 和 5 协议的一个子集:它不支持认证，不支持 UDP 或 bind 请求。
*   当 Socks 代理用完可用的线程时，在线程被释放之前，无法建立新的连接。
*   将来会实现新的功能。欢迎公关。

**免责声明**

这个项目是为安全研究人员和渗透测试人员设计的，只有得到系统所有者的批准才能使用。

[**Download**](https://github.com/p3nt4/Invoke-SocksProxy)