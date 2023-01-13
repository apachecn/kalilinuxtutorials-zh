# 针对 Linux、Windows 和 Android 的五大 DDoS 攻击工具

> 原文：<https://kalilinuxtutorials.com/ddos-linux-windows-android/>

DDOS 或分布式拒绝服务攻击是 DOS 攻击的最强版本。在这种情况下，许多计算机被用来以分布式方式定位同一服务器。

其中拒绝服务攻击是最危险的网络攻击之一。它试图减少、限制或阻止合法用户访问资源。

这是通过用虚假请求淹没服务器的请求队列，从而使其资源过载来实现的。DOS 攻击也能永久破坏网站。DOS 攻击有两种方式。要么使服务器崩溃，要么使服务泛滥。

在这种情况下，阻止单个或几个 IP 地址不起作用，因为它涉及一个僵尸网络来执行 DOS 攻击。互联网上有许多工具可以淹没服务器并进行攻击。这里我们列举其中的几个

我们网站上的文章仅用于教育/信息目的。作者不对任何非法活动负责。我们不提倡任何恶意活动。

**又读:** [**泄密者:用庄丹**T5 找到打开的数据库](https://kalilinuxtutorials.com/leaklooker-open-databases-shodan/)

### **五大 DDoS 攻击工具**

**低轨道离子炮(LOIC)**

是一款用 C#编写的开源网络压力测试和 DOS 攻击软件。该工具通过在目标上发送 UDP、TCP 或 HTTP 来执行 DOS 攻击，意图破坏其服务

主要用于小型服务器的 DOS 攻击。它也可以在 Linux、Windows 和 Android 上使用。

[**Click Here To Download**](https://sourceforge.net/projects/loic/)

**慢动作**

这是 DDOS 攻击最有效的工具。它的工作原理是打开数千个到目标 web 服务器的连接，并长时间保持这些连接。

这是通过发送部分 HTTP 请求来实现的，它们都不会被完成。它只需要很少的带宽就可以到达网络服务器，而且没有任何副作用。

[**Click Here To Download**](https://pypi.org/project/Slowloris/)

**HOIC(高轨道离子佳能)**

高轨道离子炮或 HOIC 是为了取代低轨道离子炮(LOIC)工具而开发的。它的工作原理是用垃圾 HTTP、get 和 POST 请求淹没目标 web 服务器。

它可以一次同时打开多达 256 个攻击会话。这有助于通过发送连续的垃圾请求来关闭目标系统，从而使合法请求无法得到处理。

HOIC 是一个流行的工具，可以免费下载。这也适用于 Windows、Mac 和 Linux 平台。

[**Click Here To Download**](https://sourceforge.net/projects/highorbitioncannon/)

**R-U-Dead-Yet**

R-U-Dead-Yet 也称为 RUDY，是另一种 DOS 攻击工具，它通过 HTTP POST 方法提交一个长格式字段。

该工具检测目标网站中嵌入的 web 表单，然后发送一个合法的 HTTP POST 请求，该请求带有一个很长的“content-length”头字段。

之后，它将一次发送一个字节大小的数据包形式的信息。

[**Click Here To Download**](https://sourceforge.net/projects/r-u-dead-yet/)

**幽门**

 **幽门是一个可脚本化的工具，用于测试服务器中的漏洞。它可以通过使用 SOCKS 代理和 SSL 连接来执行 DOS 攻击。

它还可以针对各种协议，如 HTTP，FTP，IMAP，SMTP，Telnet。它也可以在 Windows、MAC 和 LINUX 上使用。

[**Click Here To Download**](https://sourceforge.net/projects/pyloris/)**