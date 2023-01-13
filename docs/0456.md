# DNS-Shell:DNS 通道上的交互式 Shell

> 原文：<https://kalilinuxtutorials.com/dns-shell/>

**DNS-Shell** 是一个通过 DNS 通道的交互式 Shell。该服务器基于 python，可以在任何安装了 Python 的操作系统上运行，有效负载是一个编码的 PowerShell 命令。

有效负载是在调用服务器脚本时生成的，它只是利用 nslookup 来执行查询，并向服务器查询新命令，然后服务器在端口 53 上侦听传入的通信，一旦在目标机器上执行有效负载，服务器将生成一个交互式 shell。

一旦建立了通道，有效负载将继续向服务器查询命令。如果输入了新命令，它将执行该命令并将结果返回给服务器。

**也可阅读—[谷歌让人工智能开发者可以轻松保护用户数据隐私](https://kalilinuxtutorials.com/google-makes-it-easy-for-ai-developers-to-keep-users-data-private/)**

**用途**

运行它相对简单

它支持两种操作模式直接模式和递归模式:

*   从我们的 DNS-shell [Github 页面](https://github.com/sensepost/DNS-Shell)执行 git 克隆
*   它的直接模式:sudo python DNS-shell . py-l-d[服务器 IP]
*   它的递归模式:sudo python DNS-shell . py-l-r[Domain]

[**Download**](https://github.com/sensepost/DNS-Shell)