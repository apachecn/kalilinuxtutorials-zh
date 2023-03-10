# 使 Tor 网络成为你的默认网关的脚本

> 原文：<https://kalilinuxtutorials.com/nipe-script-tor-default-gateway/>

Nipe 是一个让 Tor Network 成为你默认网关的脚本。Nipe 是一个用于 Linux 的脚本，它调整 iptables 来处理 Tor 上的所有活动。问题是 Tor 只支持 TCP，而不支持 UDP。因此，像“dns 查询”这样的大多数 UDP 应用程序都将失败。如果 Linux 框架是为 IPv6 设计的，这个脚本同样也有一个难题。更重要的是，Linux 自然是 IPv6 的基础。万一你附近的系统或 ISP 支持 IPv6，那么它就被授权了。具体来说，该脚本并不通过 Tor 转移 IPv6 TCP，因此您这样被发现是微不足道的。

**另请参阅[SQLMAP-来自易受攻击 Web 表单的数据库&用户的枚举](https://kalilinuxtutorials.com/sqlmap2/)**

## **Nipe 如何工作？**

Tor 使用户能够匿名上网、聊天和发送即时消息，并被各种各样的人用于合法和非法目的。例如，Tor 已经被犯罪企业、
黑客组织和执法机构用于不同的目的，有时是同时使用。

Nipe 是一个让 Tor Network 成为你默认网关的脚本。

这个 Perl 脚本使您能够将所有流量从您的
计算机直接路由到 Tor 网络，通过它您可以匿名地在互联网上冲浪
,而不必担心被跟踪或追溯。

#### 下载并安装:

```
git clone https://github.com/GouveaHeitor/nipe
cd nipe
cpan install Switch JSON LWP::UserAgent
```

#### 命令:

```
COMMAND          FUNCTION
install          Install dependencies
start            Start routing
stop             Stop routing
restart          Restart the Nipe process
status           See status` `Examples:` `perl nipe.pl install
perl nipe.pl start
perl nipe.pl stop
perl nipe.pl restart
perl nipe.pl status
```

**[+] AUTOR: 海托尔 gouvaêa**
**[+]SITE:https://heitorgouvea . me**
**[+]EMAIL:hi @ heitorgouvea . me**
**[+]GITHUB:https://github.com/GouveaHeitor**
**[+]电报: @GouveaHeitor【电子邮件**

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/GouveaHeitor/nipe)