# gTunnel:用 Golang 编写的健壮的调优解决方案

> 原文：<https://kalilinuxtutorials.com/gtunnel/>

[![gTunnel : A Robust Tunelling Solution Written In Golang](img/39bd6a8156686749a30cdd1f4c840f04.png "gTunnel : A Robust Tunelling Solution Written In Golang")](https://1.bp.blogspot.com/-RgelDXamu7I/XzBN9pZmzvI/AAAAAAAAHUE/1YSSHm0IIJ0eB4ljccNIVt1eTViJXjE1gCLcBGAsYHQ/s728/h92%25281%2529.png)

gTunnel 是用 golang 和 gRPC 构建的 TCP 隧道套件。gTunnel 可以管理多个正向和反向隧道，这些隧道都通过一个 TCP/HTTP2 连接承载。

我想学习一门新的语言，所以我选择了 go 和 gRPC。客户端可执行文件已经在 windows 和 linux 上进行了测试。

**依赖关系**

gTunnel 已经用 docker 版本 19.03.6 测试过了，但是任何版本的 Docker 都可以。

**如何使用？**

start_server.sh 脚本将构建一个 docker 映像，并在没有暴露端口的情况下启动它。如果您计划使用前向隧道，请确保映射这些端口或更改 docker 网络。

**。/start_server.sh**

这将最终为您提供以下提示:

首先要做的是生成一个在远程系统上运行的客户机。对于名为“win-client”的 windows 客户端

**>>>config client win 443 win-client**

对于名为 lclient 的 linux 客户机

**> > >配置 linux 客户端 172 . 17 . 0 . 1 443 lcclient**

这将在“已配置”目录中输出一个已配置的可执行文件，相对于。/start_server.sh 在远程系统上运行可执行文件后，会通知您客户端正在连接。

**>>>config client Linux 127 . 0 . 0 . 1 443 测试
>>>2020/03/20 22:01:47 端点连接:id:测试
> > >**

要使用新连接的客户端，请键入 use 和客户端的名称。支持制表符结束。

**> > >使用测试
(测试)> > >**

提示将会改变，以指示您当前使用的端点。从这里，您可以添加或删除隧道。格式是

**添加隧道(本地|远程)监听端口目的地 IP 目的地端口**

例如，要在端口 4444 上打开一个到 ip 10.10.1.5 的本地隧道，并将其命名为“smbtun ”,命令如下:

**添加隧道本地 4444 10.10.1.5 445 smbtun**

同样，要打开远程系统端口 666 上的一个端口，并将所有流量转发到本地网络端口 443 上的 192.168.1.10，命令如下:

**addtunnel remote 666 192.168.1.10 443**

注意，名称是可选的，如果没有提供，将给出随机字符作为名称。要列出所有活动隧道，请使用“listtunnels”命令。

**(测试)> > > listtunnels
隧道 ID: smbtun
隧道 ID: dVck5Zba**

要删除隧道，请使用“deltunnel”命令:

**(测试)> > > deltunnel smbtun
删除隧道:smbtun**

要在目标上启动 socks 代理服务器，请使用 socks 命令。以下命令将在运行 gClient 的主机上的端口 1080 上启动一个 socks 服务器。通常，您需要在 gTunnel 提示符下创建一个隧道来使用 socks 服务器。

**袜子 1080
添加隧道本地 1080 127.0.0.1 1080**

要返回并使用另一个远程系统，请使用 back 命令:

**【测试】> > >回
> > >**

请注意提示是如何变化的，以表明它不再与特定的客户端一起工作。要断开客户机与服务器的连接，您可以在使用客户机时发出“disconnect”命令，或者在主菜单中提供端点 id。

**(测试)> > >断开
2020/03/20 22:14:52 断开测试
(测试)> > > 2020/03/20 22:14:52 端点断开:测试
> > >**

或者

**> > >断开测试
2020/03/20 22:16:00 断开测试
>>>2020/03/20 22:16:00 端点断开:测试
> > >**

要退出服务器，请运行 exit 命令:

**> > >退出**

请注意，这将删除 docker 容器，但是任何 tls 生成的证书和配置的可执行文件都将位于 tls/和 configured/目录中。

**待办事项**

*   反向隧道支护
*   多隧道支持
*   最好打印出对隧道的支持。应该是。
*   建立了多少个连接和端口等。
*   添加 REST API 并实现 web UI
*   动态 socks 代理支持。
*   客户端和服务器之间的身份验证
*   带有预配置隧道的输入服务器配置文件

**已知问题**

*   Internet Explorer 导致客户端锁定反向隧道
*   启动服务器脚本应该重用构建的映像，而不是每次都创建一个新映像。

[**Download**](https://github.com/hotnops/gtunnel)