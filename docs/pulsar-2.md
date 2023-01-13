# Pulsar:数据渗透和隐蔽通信工具

> 原文：<https://kalilinuxtutorials.com/pulsar-2/>

[![](img/bd8b185fbc860c35c7c0e4fe9dc51cfa.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhaLbljyIlkfDxiAXq6AKvBhNO0DwIMr7IClCQz7okOo07KC4ccOMf3S9JnGykXzYor9H3uF_L9t10I6Cs4uyd8mMMAGJLlUCYDQjk9ZserBJk2J7KV41JVY0xu-sPBdpixvdE4L1tw8Rts1tDToxSR_TOdlcS6Y4vvqi-tCSChQPdB-RC6do_odf4t/s728/Data%20Exfiltration%20(2).png)

Pulsar 是一款用于数据渗透和隐蔽通信的工具，使您能够通过不同的协议创建安全的数据传输、奇怪的聊天或网络隧道，例如，您可以从 tcp 连接接收数据，并通过 DNS 数据包将其重新发送到真实的目的地

## 设置 Pulsar

首先，从存储库中获取代码，并使用以下命令编译它:

**$ CD pulsar
$ export GOPATH = $(shell pwd)
$ go 获取 golang.org/x/net/icmp
$ go build-o bin/pulsar src/main . go**

或者运行:

**$ make**

## 连接器

连接器是通向外部世界的简单通道，通过连接器，您可以从不同的源读取和写入数据。

*   控制台:
    *   默认输入/输出连接器，从标准输入读取数据并写入标准输出
*   传输控制协议（Transmission Control Protocol）
    *   通过 tcp 连接读写数据

**tcp:127.0.0.1:9000**

用户数据报协议(User Datagram Protocol)

*   通过 udp 包读写数据

**udp:127.0.0.1:9000**

网间控制报文协议(Internet Control Messages Protocol)

*   通过 icmp 数据包读写数据

**icmp:127.0.0.1(连接端口明显没用)**

您可以使用 option-in 来选择输入连接器，使用 option-out 来选择输出连接器:

**–in TCP:127 . 0 . 0 . 1:9000
–out DNS:fk DNS . lol:2 . 3 . 4 . 5:8989**

## 经理人

一个处理程序允许你改变传输中的数据，你可以任意组合处理程序。

*   存根:
    *   默认，什么都不做，通过
*   Base32
    *   Base32 编码器/解码器

**–处理器 base32**

您可以使用–decode 选项在解码模式下使用所有的处理程序

**–处理 base64，base32，base64，密码:密钥–解码**

# 例子

在下面的例子中，Pulsar 将用于在 DNS 协议上创建一个安全的双向隧道，数据将从 TCP 连接(简单的 nc 客户端)中读取，并通过隧道加密重新发送。

**【NC 127 . 0 . 0 . 1 9000】<–TCP->【脉冲星】<–DNS->【脉冲星】<–TCP->【NC-l 127 . 0 . 0 . 1-p 9900】**

**$。/pulsar–in TCP:127 . 0 . 0 . 1:9000–out DNS:test . org @ 192 . 168 . 1 . 199:8989–duplex–plain–handlers 的密码:supersekretkey！!'
$ 127 . 0 . 0 . 1 9000**

[**Download**](https://github.com/jacopodl/Pulsar)