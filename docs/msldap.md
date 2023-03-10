# Msldap:用于审计 MS AD 的 ldap 库

> 原文：<https://kalilinuxtutorials.com/msldap/>

[![Msldap : LDAP Library For Auditing MS AD](img/87a84e58898440fe76ca91052ff4438b.png "Msldap : LDAP Library For Auditing MS AD")](https://1.bp.blogspot.com/-RTD3Dhxmd-U/YLTi41G5IDI/AAAAAAAAJQo/GQTn68DWgD0YSVY0xBjcN2KHDf5XfPZtgCLcBGAsYHQ/s640/msldap_2.gif)

Msldap 是一个用于 MS AD 的(ldap)轻量级目录访问协议库的工具。

**特性**

*   附带一个内置的控制台 LDAP 客户端
*   所有参数都可以通过一个方便的 URL 来控制(见下文)
*   支持 NTLM 和 KERBEROS 的集成 windows 身份验证(SSPI)
*   支持通道绑定(适用于 ntlm 和 kerberos，不适用于 SSPI)
*   支持加密(适用于 NTLM/KERBEROS/SSPI)
*   支持 LDAPS (TODO:实际验证证书)
*   支持 SOCKS5 代理，不需要额外的代理
*   最小占地面积
*   大量预建的查询用于方便的信息轮询
*   易于集成到您的项目中
*   没有测试套件

**安装**

走 GIT

**python3 setup.py 安装**

运筹学

**pip 安装 msldap**

**先决条件**

*   `**winsspi**`模块。仅适用于 windows。这支持基于 SSPI 的认证。
*   `**asn1crypto**`模块。一些 LDAP 查询包含要在 ASN1 传输 XD 之上发送的 ASN1 结构
*   `**asysocks**`模块。支持 socks 代理。
*   `**aiocmd**`对于交互式客户端
*   `**asciitree**`用于在交互式客户端中绘制漂亮的树

**用途**

请注意，这是一个库，并不打算用作命令行程序。
注意到这一点，该项目打包了一个全功能的 LDAP 交互式客户端。当用`**setup.py install**`安装`**msldap**`模块时，一个名为`**msldap**`的新二进制文件将会出现(令人震惊的命名惯例)

**LDAP 连接 URL**

版本 0.2.0 中的主要变化是将不同的连接选项统一为一个字符串，而不需要额外的命令行开关。
新的连接字符串由以下方式组成:
`**<protocol>+<auth_method>://<domain>\<username>:<password>@<ip>:<port>/?<param>=<value>&<param>=<value>&...**`
详细举例说明:

**+://:@://？=
设置 ldap 协议支持以下值:
–LDAP
–ldaps
如果要执行明文身份验证，则可以省略(在这种情况下，默认为 ntlm-password)，否则:
–NTLM-password
–NTLM-nt
–Kerberos-password(必须使用 dc 选项参数)
–Kerberos-RC4/Kerberos-nt(必须使用 dc 选项参数)
–Kerberos-AES(DC 选项)
–sspi-Kerberos(仅限 windows！)
–匿名
–普通
–简单
–西西里(与 ntlm-nt 格式相同，但使用西西里认证)
:
可选。指定所有查询的根树
可以是:
–time out:以秒为单位的连接超时
–proxy type:目前仅支持 socks5 代理
–proxy host:代理服务器的 IP 或主机名
–proxy port:代理服务器的端口
–proxy time out:代理连接的 ecodns 超时
–DC:域控制器的 Ip 地址， 必须用于 kerberos 认证
示例:
ldap://10.10.10.2(匿名绑定)
ldaps://test.corp(匿名绑定)
LDAP+sspi-NTLM://TEST . corp
LDAP+sspi-Kerberos://TEST . corp
LDAP://TEST \ victim:@ 10 . 10 . 10 . 2(默认为 SASL GSSAPI NTLM)
LDAP+SIMPLE time out = 99&proxy type = socks 5&proxy host = 127 . 0 . 0 . 1&proxy port = 1080&proxy time out = 44**

[**Download**](https://github.com/skelsec/msldap)