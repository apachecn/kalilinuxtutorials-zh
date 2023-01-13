# 比奇:eBPF 游乐场

> 原文：<https://kalilinuxtutorials.com/peetch/>

[![](img/f905dcfd51491ef5f09a9d6c5544b5fa.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgIw_UrY01UOQImtEy8bNJyBq1jPMXq3w_9BklG1vQbmRzsnuMSyWuQlARzDY7VTh-fLtMh_0qyx4TSAihLO_EscyiYtEB2hefdhMNztqBE78YK3F-DI_vlO6IRlLxeTyeqiigNDZydpRS4YS4lforN8jLvLd5BCbMzcqd5asFvoljog52YZRM_R6fr/s728/download%20(1).png)

`**peetch**`是一组工具，旨在试验 eBPF 的不同方面，以绕过 TLS 协议保护。

目前，peetch 包括两个子命令。第一个称为`**dump**`的目的是通过将关于源进程的信息与每个数据包相关联来嗅探网络流量。第二个名为`**tls**`允许使用 OpenSSL 识别进程来提取密钥。

结合使用这两个命令，可以解密以 PCAPng 格式记录的 TLS 交换。

## 安装

`**peetch**`依赖于几个依赖项，包括 bcc 和 Scapy 的非合并修改。使用以下命令可以轻松构建 Docker 映像，以便轻松测试`**peetch**`:

**码头工建造-t 夸克 slab/peech。**

## 命令遍历

以下示例假设您使用以下命令输入 Docker 映像并在其中启动示例:

**docker run–privileged–network host–mount type = bind，source=/sys，target =/sys–mount type = bind，source=/proc，target =/proc–RM-it quarkslab/peetch**

### `**dump**`

此子命令使您能够使用 eBPF TC 分类器来嗅探数据包，并使用以下命令检索相应的 PID 和进程名称:

**peetch dump
curl/1289291–Ether/IP/TCP 10 . 211 . 55 . 10:53052>208 . 97 . 177 . 124:https S/Padding
curl/1289291–Ether/IP/TCP 208 . 97 . 177 . 124:https>10 . 211 . 55 . 10:53052 SA/124**

请注意，出于演示目的，`**dump**`将仅捕获基于 IPv4 的 TCP 数据段。

为了方便起见，可以使用`**--write**`将捕获的数据包与进程信息一起存储到 PCAPng 中:

**peetch 转储–写入 peetch.pcapng
^C**

使用 Wireshark 或 Scapy 可以轻松操作该 PCAPng:

scapy

**l = rdpcap(“peetch . pcapg”)
l[0]
>>>
l[0]。
b ' curl/1289909**怎么说

### `**tls**`

这个子命令旨在识别使用 OpenSSl 的进程，并使它转储一些东西，如明文和机密。

默认情况下，`**peetch tls**`将只为每个进程显示一行，`**--directions**`参数使得显示交换消息成为可能:

**peech TLS—方向
<curl(1291078)208 . 97 . 177 . 124/443 TLS 1.2 ecdh-RSA-AES 128-GCM-sha 256**

c**URL(1291078)208.97.177.124/443 TL S1。-1 个 ECDHE-RSA-AES128-GCM-SHA256**

显示 OpenSSL 缓冲区内容是通过`**--content**`实现的。

内容
curl(1290608)208 . 97 . 177 . 124/443 TLS 1.2 ecdh-RSA-AES 128-GCM-sha 256 0000 47 54 20 F2 f20 48 54 54 50 F2 f31 2 e 31 0d 0 a get/http/1.1-什么 0010 48 6 f 73 74 3 至 20 77 77 77 2 和 70 65 72 64 75 2E 主机:www . lost . 0020 63 6 f 6 d0s 0 至 55 73 65 72 2D 41 67 65 6E 74 3A com-什么用户代理:0030 20 63 75 72 6 C2 f 37 2 e 36 38 2 e 30 0d 0 a 41 63 curl/7 . 68 . 0-什么 AC->curl(1290608)208 . 97 . 177 . 124/443 TLS 1。-1 ecdhe-RSA-AES 128-GCM-sha 256
0000 48 54 54 50 F2 f31 2 e 31 20 32 30 30 20 4 F4 b0d http/1.1200 确定。
0010 至 44 61 74 65 3 至 20 54 68 75 2C 20 31 39 20 4D。日期:格林尼治标准时间 18:16:01
00320 47 4d54 0d 0 至 53 65 72 76 65 72 72 3 至 20 41 70-什么服务器:Ap

`**--secrets**`参数将显示从内存中提取的 TLS 主密钥。以下示例利用`**--write**`来编写要讨论的主机密，以简化用 Scapy 解密 TLS 消息:

**(睡眠 5；curl https://www.perdu.com/?name=highly%20secret%20information–TLS-max 1.2-http 1.1)&
peetch TLS–write&
curl(1293232)208.97.177.124/443 TLS 1.2 ECDHE-RSA-AES 128-GCM-sha 256
peetch dump–write traffic . pcapng
C
将主秘密添加到 PCAPng 文件中
editcap–inject-secrets TLS，1293232-master _ secret . log traffic . PCAPng 消息
[]**

[**Download**](https://github.com/quarkslab/peetch)