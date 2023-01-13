# 出口评估:用于测试出口数据检测能力的工具

> 原文：<https://kalilinuxtutorials.com/egress-assess-data-detection/>

出口评估是一种用于测试出口数据检测能力的工具。要进行安装，请运行附带的安装脚本，或执行以下操作:

*   安装 pyftpdlib
*   生成一个服务器证书，并将其存储为与 Egress-assesse 相同级别的“server.pem”。这可以通过以下命令完成:

**OpenSSL req-new-x509-keyout server . PEM-out server . PEM-days 365-nodes**

**也读: [Kaboom:自动化渗透测试的脚本](https://kalilinuxtutorials.com/kaboom-penetration-test/)**

**用途**

博客帖子可在此处获得:

*   [https://www . christophertruncer . com/egress-assesse-testing-egress-data-detection-capabilities/](https://www.christophertruncer.com/egress-assess-testing-egress-data-detection-capabilities/)
*   [https://www . christophertruncer . com/egress-assesse-action-via-powershell/](https://www.christophertruncer.com/egress-assess-action-via-powershell/)

出口评估的典型用例是在两个位置复制该工具。一个位置将充当服务器，另一个位置将充当客户端。出口评估可以通过 FTP、HTTP 和 HTTPS 发送数据。

要通过 ftp 提取数据，首先要启动 Egress-assesse 的 FTP 服务器，方法是选择“–服务器 FTP”并提供用户名和密码以供使用:

**。/Egress-assesse . py–服务器 FTP–用户名 testuser–密码 pass123**

现在，要让客户机连接并向 ftp 服务器发送数据，您可以运行…

。/Egress-assesse . py–客户端 FTP–用户名 testuser–密码 pass 123–IP 192 . 168 . 63 . 149–数据类型 ssn

此外，您可以通过运行…来设置 Egress-assesse 作为 web 服务器。

。/Egress-assesse . py–服务器 https

然后，要向 FTP 服务器发送数据，特别是发送 15 兆的信用卡数据，运行以下命令…

。/Egress-assesse . py–客户端 https–数据大小 15–IP 192 . 168 . 63 . 149–数据类型 cc

[**Download**](https://github.com/FortyNorthSecurity/Egress-Assess)