# Jarm:主动传输层安全(TLS)服务器指纹工具

> 原文：<https://kalilinuxtutorials.com/jarm/>

[![SMTPTester : Small Python3 Tool To Check Common Vulnerabilities In SMTP Servers](img/650febbb49702cc4b827b73bdd66425e.png "SMTPTester : Small Python3 Tool To Check Common Vulnerabilities In SMTP Servers")](https://1.bp.blogspot.com/-2dViqwTuBso/XaVTShad9FI/AAAAAAAAC7g/E5euH3VUfkUVPDNBz0vaxI0V037KUp8KQCLcBGAsYHQ/s1600/SMTPTester%2B%25281%2529.png)

**JARM** 是一款主动传输层安全(TLS)服务器指纹识别工具。

JARM 指纹可用于:

*   快速验证一个组中的所有服务器是否具有相同的 TLS 配置。
*   通过配置将互联网上不同的服务器分组，例如，识别服务器可能属于 Google vs. Salesforce vs. Apple。
*   确定默认应用程序或基础架构。
*   识别互联网上的恶意软件命令和控制基础设施以及其他恶意服务器。

JARM 支持已经或正在添加到:
security trails
Shodan
binary edge
risk IQ
Palo Alto Networks
Censys
360

**跑 JARM**

**python3 jarm.py [-h] [-i 输入] [-p 端口] [-v] [-V] [-o 输出] [-j] [-P 代理] [域/IP]**

示例:

`**% python3 jarm.py www.salesforce.com**`
**`Domain: www.salesforce.com`
`Resolved IP: 23.50.225.123`
`JARM: 2ad2ad0002ad2ad00042d42d00000069d641f34fe76acdc05c40262f8815e5`**

要在 Python 2 中使用它，您需要 ipaddress 模块:

`**pip install -r requirements.txt**`

**批量运行 JARM 大单速度**

`**./jarm.sh <list> <output_file>**`
例如:
`**% ./jarm.sh alexa500.txt jarm_alexa_500.csv**`

**示例输出**

| 领域 | JARM |
| --- | --- |
| salesforce.com | `**2ad2ad0002ad2ad00042d42d00000069d641f34fe76acdc05c40262f8815e5**` |
| force.com | `**2ad2ad0002ad2ad00042d42d00000069d641f34fe76acdc05c40262f8815e5**` |
| google.com | `**27d40d40d29d40d1dc42d43d00041d4689ee210389f4f6b4b5b1b93f92252d**` |
| youtube.com | `**27d40d40d29d40d1dc42d43d00041d4689ee210389f4f6b4b5b1b93f92252d**` |
| gmail.com | `**27d40d40d29d40d1dc42d43d00041d4689ee210389f4f6b4b5b1b93f92252d**` |
| facebook.com | `**27d27d27d29d27d1dc41d43d00041d741011a7be03d7498e0df05581db08a9**` |
| instagram.com | `**27d27d27d29d27d1dc41d43d00041d741011a7be03d7498e0df05581db08a9**` |
| oculus.com | `**29d29d20d29d29d21c41d43d00041d741011a7be03d7498e0df05581db08a9**` |

**JARM 如何工作**

在了解 JARM 如何工作之前，了解 TLS 如何工作是很重要的。TLS 和它的前身 SSL 被用于加密通信，既用于互联网浏览器等常见应用程序，以确保您的数据安全，也用于恶意软件，因此它可以隐藏在噪音中。为了启动 TLS 会话，客户端将在 TCP 三次握手之后发送 TLS 客户端问候消息。这个包及其生成方式取决于构建客户端应用程序时使用的包和方法。如果接受 TLS 连接，服务器将用 TLS 服务器 Hello 数据包进行响应。

TLS 服务器根据在 TLS 客户端 Hello 数据包中收到的详细信息来制定它们的服务器 Hello 数据包。为任何给定的客户机 Hello 制定服务器 Hello 的方式可以根据应用程序或服务器的构建方式而有所不同，包括:

*   操作系统
*   操作系统版本
*   使用的库
*   使用的那些库的版本
*   调用库的顺序
*   自定义配置

所有这些因素导致每个 TLS 服务器以独特的方式响应。这些因素的组合使得不同组织部署的服务器不太可能有相同的响应。

JARM 的工作方式是主动向目标 TLS 服务器发送 10 个 TLS 客户端 Hello 数据包，并捕获 TLS 服务器 Hello 响应的特定属性。然后，聚合的 TLS 服务器响应以特定的方式进行哈希处理，以生成 JARM 指纹。

这不是我们第一次与 TLS 指纹合作。2017 年，我们开发了 JA3/S，这是一种被动的 TLS 客户端/服务器指纹识别方法，现在可以在大多数网络安全工具上找到。但是 JA3/S 是被动的，通过监听网络流量来识别客户端和服务器，而 JARM 是一个主动的服务器指纹扫描器。你可以在这里找到更多关于 TLS 协商和 JA3/S 被动指纹的信息。

JARM 的 10 个 TLS 客户端 Hello 数据包是特制的，用于在 TLS 服务器中产生唯一的响应。JARM 以不同的顺序发送不同的 TLS 版本、密码和扩展名，以收集唯一的响应。服务器支持 TLS 1.3 吗？它会用 1.2 的密码协商 TLS 1.3 吗？如果我们从最弱到最强排列密码，它会选择哪个？这些都是不同寻常的问题，JARM 实际上是在要求服务员给出最独特的回答。然后，这 10 个响应被散列以产生 JARM 指纹。

JARM 指纹哈希是一种混合模糊哈希，它使用可逆和不可逆哈希算法的组合来产生 62 个字符的指纹。前 30 个字符由服务器为发送的 10 个客户端 hello 中的每一个选择的密码和 TLS 版本组成。“000”表示服务器拒绝与该客户端协商 hello。剩余的 32 个字符是服务器发送的累积扩展名的截断的 SHA256 哈希，忽略 x509 证书数据。当比较 JARM 指纹时，如果前 30 个字符相同，但后 32 个字符不同，这意味着服务器具有非常相似的配置，接受相同的版本和密码，尽管由于扩展名不同而不完全相同。

在收到每个 TLS 服务器 hello 消息后，JARM 用 FIN 优雅地关闭连接，以免让套接字保持打开。

值得注意的是，JARM 是一种高性能的指纹函数，不应被视为或与安全加密函数混淆。我们将 JARM 指纹设计成既是机器消耗品也是人类消耗品。这意味着它足够小，足以吸引眼球，分享和发推特，并为上下文细节提供足够的空间。

**JARM 如何被用来识别恶意服务器**

恶意软件命令和控制(C2)和恶意服务器由它们的创建者像任何其他服务器一样进行配置，然后部署到它们的机群中。因此，这些往往会产生独特的 JARM 指纹。以下是常见恶意软件和攻击性工具的示例，JARM 与 Alexa 排名前 100 万的网站重叠(截至 2020 年 10 月):

| 恶意服务器 C2 | JARM 指纹 | 与 Alexa Top 1M 重叠 |
| --- | --- | --- |
| 特技机器人 | `**22b22b09b22b22b22b22b22b22b22b352842cd5d6b0278445702035e06875c**` | Zero |
| 异步鼠 | `**1dd40d40d00040d1dc1dd40d1dd40d3df2d6a0c2caaa0dc59908f0d3602943**` | Zero |
| Metasploit | `**07d14d16d21d21d00042d43d000000aa99ce74e2c6d013c745aa52b5cc042d**` | Zero |
| 钴罢工 | `**07d14d16d21d21d07c42d41d00041d24a458a375eef0c576d23a7bab9a9fb1**` | Zero |
| 梅林·C2 | `**29d21b20d29d29d21c41d21b21b41d494e0df9532e75299f15ba73156cee38**` | Three hundred and three |

由于 Alexa Top 1M 网站几乎没有重叠，组织内的主机不太可能连接到具有这些 JARM 指纹的服务器。

[**Download**](https://github.com/salesforce/jarm)