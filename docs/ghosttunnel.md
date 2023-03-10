# ghost tunnel–可在隔离环境中使用的后门传输方法

> 原文：<https://kalilinuxtutorials.com/ghosttunnel/>

**GhostTunnel** 是一种隐蔽的后门传输方式，可以在隔离环境下使用。它可以通过 HID 设备攻击目标，只需要释放有效载荷代理，然后在有效载荷释放后可以移除 HID 设备。

GhostTunnel 使用 802.11 探测请求帧和信标帧进行通信，不需要建立 wifi 连接。确切地说，它通过在信标和探测请求中嵌入数据来进行通信。我们发布了用 c/c++实现的 GhostTunnel 服务器和 windows 代理。

代理不需要提升权限，它使用系统 wifi api 发送探测请求并接收信标。例如在 windows 上，使用本地 WiFi API。所以你可以在其他平台上实现相应的代理。服务器运行在 linux 上，您需要一个或两个支持监控模式和数据包注入的 usb wifi 卡来运行它。

**也可阅读[Getsploit v 0 . 2 . 2–搜索和下载漏洞利用的命令行实用程序](https://kalilinuxtutorials.com/getsploit-searching-downloading-exploits/)**

## **幽灵隧道的优势**

1.  隐蔽性。
2.  不干扰目标的现有连接状态和通信。
3.  可以绕过防火墙。
4.  可用于攻击严格隔离的网络。
5.  通信信道不依赖于目标的现有网络连接。
6.  允许多达 256 个客户端
7.  有效范围可达 50 米
8.  跨平台支持。
9.  可以用来攻击任何带有无线通信模块的设备，我们在 Window 7 到 Windows 10 以及 OSX 上测试了这种攻击。

## **如何使用** **？**

*   服务器只需要一个或两个支持数据包注入和监控模式的无线网卡，如 TP-LINK TL-WN722N、Alfa AWUS036ACH。用法:

```
 **`./ghosttunnel [interface]
 ./ghosttunnel [interface1] [interface2]

 COMMANDS:
 	sessions = list all clients
 	use = select a client to operate, use [clientID]
 	exit = exit current operation
 	wget = download a file from a client, wget [filepath]
 	quit = quit ghost tunnel
 	help = show this usage help
```

*   客户端将有效负载释放到目标系统(仅发布 windows 客户端)并执行它。

## **实施**

*   Shell 命令创建远程 shell。
*   下载文件文件最大大小限制为 10M，一次只能下载一个文件。
*   您可以根据需要添加其他功能。

## **大楼**

### **服务器要求**

```
apt-get install pkg-config libnl-3-dev libnl-genl-3-dev
```

### **编译**

```
server:
	cd src
	make
windows client:
	Microsoft Visual Studio 2015
```

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/360PegasusTeam/GhostTunnel) **信用** ** : Aircrack-ng，MDK4，hostapd & Kismet**