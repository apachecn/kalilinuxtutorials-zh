# 蓝牙低能耗瑞士军刀

> 原文：<https://kalilinuxtutorials.com/btlejack-bluetooth-low-energy-swiss-army-knife/>

[![Btlejack : Bluetooth Low Energy Swiss-Army Knife](img/7f1ac1fb9fd443d2273501a3a34068e1.png "Btlejack : Bluetooth Low Energy Swiss-Army Knife")](https://1.bp.blogspot.com/-5MkFgFLwHOY/XXTD3hScdyI/AAAAAAAACY8/8X1TRElyxoQaWotbyPBml-Uu1Odu0RGpgCLcBGAs/s1600/Hacker.png)

**Btlejack** 提供一切你需要的嗅探，干扰和劫持蓝牙低能耗设备。它依靠一个或多个 [BBC Micro:Bit](http://microbit.org/) 。

运行专用固件的设备。您可能还想使用一个 [Adafruit 的 Bluefruit LE 嗅探器](https://www.adafruit.com/product/2269)或一个 [nRF51822 评估套件](https://www.waveshare.com/wiki/BLE400)，因为我们增加了对这些设备的支持。

此工具的当前版本(2.0)支持 BLE 4.x 和 5 . x。BLE 5 . x 支持有限，因为它仅支持 1Mbps 未编码 PHY，不支持频道映射更新。

**要求**

你需要一个基于 UNIX 的系统(例如 Raspberry Pi)。如果您使用 BBC Micro:Bit，您将需要一到三个 Micro:Bit 设备(推荐三个设备)以及每个设备一个空闲的 USB 端口。

Micro:Bit 的功耗相当低，因此您可以使用一个 USB 端口和一个无源集线器为三个推荐单元供电。

如果你在电脑上同时连接 3 个 microbits，Btlejack 将能够嗅探每个广告频道，并有更多的机会捕获连接请求。

**也可阅读-[Telegra cs harp C2:C #编写的命令和控制](https://kalilinuxtutorials.com/telegra-csharp-c2/)**

**如何安装？**

首先，用 Pip 安装`btlejack` Python3 客户端软件:

**$ sudo pip3 安装 btlejack**

然后，用 USB 电缆将您的 Micro:Bit 设备连接到您的计算机，安装相关的大容量存储设备(安装点必须包含 **MICROBIT** ，并发出以下命令:

**$ btlejack -i**

这将对连接到您的计算机的每个 Micro:Bit 设备进行编程，并使它们准备好与 Btlejack 一起使用。它将使用当前客户端软件的正确固件版本，因此强烈建议您在每次更新 Btlejack 时执行此固件安装程序。

如果您使用的是 *Bluefruit LE sniffer* 或 *nRF51822 评估套件*，那么请使用外部 SWD 编程器用[该固件](https://github.com/virtualabs/btlejack-firmware/raw/master/dist/btlejack-firmware-ble400.hex)刷新您的设备。

保持设备连接，一切就绪！

**注意**:这只适用于 posix 兼容系统。

**如何使用 Btlejack？**

使用 Btlejack 相当容易。Btlejack 可以:

*   使用各种设备
*   嗅探现有的 BLE 连接
*   嗅嗅新 BLE 的联系
*   堵塞现有的 BLE 连接
*   劫持现有的 BLE 连接
*   将捕获的数据包导出为各种 PCAP 格式

**指定要使用的设备**

Btlejack 通常会尝试自动检测和使用连接的兼容设备(目前仅 Micro:Bit ),但由于固件可以被黑客攻击或修改，以与其他基于 nRF51822 的板一起工作，因此它提供了一个特定的选项来允许与这些设备兼容。

`-d`选项允许您使用 Btlejack 指定一个或多个设备。请注意，此选项将禁用设备的自动检测，您应该根据需要添加尽可能多的设备:

**$ btlejack-d/dev/tty ACM 0-d/dev/tty ACM 2-s**

**嗅探现有连接**

首先，使用`btlejack`找到到目标的现有连接:

$ btlejack -s
BtleJack 版本 1.1

【I】枚举现有连接…
[–54 dBm]0x CD 91d 517 | pkts:1
[–46 dBm]0x CD 91d 517 | pkts:2

第一个值(以 dBm 为单位)显示信号的功率，该值越大，探测到的连接越好。

第二个值(十六进制)是相关的访问地址，这是一个 32 位值，用于标识两个蓝牙低功耗兼容设备之间的链路。

最后一个值是使用该访问地址看到的数据包数量。该值越高，使用相应访问地址的可能性越大。

然后，使用-f 选项跟踪特定的连接:

btle jack-f 0xdda4845e
btle jack 版本 1.1

【I】检测到嗅探器:
>嗅探器#0: fw 版本 1.1

【I】与连接 0x DDA 4845 e 同步…
CRCInit:0x2a 035 e
通道图= 0x 1 ffffffff
跳间隔= 39
跳增量= 15
正在捕获数据包…
LL 数据:02 07 03 00 04 00 03 00
LL 数据:00 08 04 00 04 00 00 05a 69 70
LL 数据:02 07 03 00 04 00 00 03 00
LL 数据:08 04 00 04 00 05a 69 70

如果您正在使用 1 个以上的 microbit，Btlejack 将并行执行一些嗅探操作，以加速连接参数恢复！

**嗅探新连接**

btlejack 支持的-c 选项允许您指定目标 BD 地址，或者您可能希望使用 any 来捕获任何新创建的连接。

$ btlejack -c any
BtleJack 版本 1.1
[i]检测到的嗅探器:
嗅探器#0:版本 1.1
嗅探器#1:版本 1.1
LL 数据:05 22 df B4 6f 95 C5 55 c00a F6 99 23 40 1d 7b 2f 0a 9a F4 93 01 12 00 27 00 00 d0 07 ff ff ff 1f 0b【T5[I] 从 55:c5:95:6f:b4:df 到 40:23:99:F6:0a:c0
|–访问地址:0x 0a 2 f 7 B1 d
|–CRC 初始值:0x 93 f 49 a
|–跳间隔:39
|–跳增量:11
|–信道映射:1 fffffffff
|–超时:20000 ms
LL 数据:03 09

或者您可能还想指定目标 BD 地址:

**$ btle jack-c 03:E1:F0:00:11:22**

**堵塞连接**

一旦一个连接被它的*访问地址*识别，你可以通过使用`-j`选项提供 jam 它:

**$ btlejack-f0x 129 f 3244**

**劫持 BLE 连线**

Btlejack 也能够劫持一个现有的连接，使用`-t`选项来这样做。一旦被劫持，Btlejack 会给你一个提示，让你与被劫持的设备进行交互。

首先，劫持一个现有的连接:

$ btle jack-f 0x 9 c 68 FD 30-t-m 0x 1 fffffffff
btle jack 版本 1.1
[i]使用缓存参数(创建于 2018-08-11 01:48:24)
[i]检测到嗅探器:
嗅探器#0: fw 版本 1.1
[i]与连接 0x 9 c 68 FD 30…
CRCInit:0x81f 733

然后使用以下命令与设备进行交互:–discover:执行服务和特征枚举，将为您提供有关服务和特征的所有信息–write:将数据写入特定值句柄–read:从特定值句柄读取数据–ll:发送原始链路层数据包(针对 ninjas)

**发现命令**

discover 命令将发送和接收蓝牙 LE 数据包，并检索所有服务 uuid 和参数，以及特征 uuid 和参数:

btle jack > discover
start:0001 end:0005
start:0014 end:001 a
start:0028 end:ffff
发现的服务:
服务 UUID: 1801
特性 UUID: 2a05
| handle: 0002
|属性:indicate (20)
\值 handle: 0003
服务 UUID: 1800
特性 UUID: 2a04 值句柄:0016
特征 UUID: 2a01
|句柄:0017
|属性:读(02)
\值句柄:0018
服务 UUID: 1824
特征 UUID: 2abc
|句柄:0029
|属性:写指示(28)
\值句柄:002a

读命令

`read`命令接受单个参数，即与您想要读取的特性相对应的值句柄:

**btlejack >读取 0x16
读取>4c 47 20 77 65 62 4f 53 20 54 56**

**W***成年礼 T5**命令***

`write`命令接受三个参数:

**btlejack >写<值句柄>数据格式> <数据>**

支持的数据格式:

*   `**hex**`:十六进制数据(即“414261”)
*   `**str**`:文本字符串，可以用双引号括起来

**ll 命令**

最后一个命令允许您以十六进制形式发送蓝牙低能耗链路层 PDU，如第 6 卷 B 部分第 2.4 章所述。

**PCAP 文件导出**

Btlejack 的一个有趣的特性是可以将捕获的数据导出到 PCAP 文件中。

Btlejack 支持以下 DLT 格式:

*   DLT _ 蓝牙 _ 乐 _LL_WITH_PHDR(同款)
*   DLT _ 北欧 _BLE(北欧‘嗅探器’用的那个)
*   DLT _ 蓝牙 _ 乐 _LL(最新版本的 Wireshark 支持)

可以使用-o 选项指定输出文件，而使用-x 选项指定输出格式。有效的格式值为:ll_phdr、nordic 或 pcap(默认值)。

**$ btle jack-f 0x AC 56 BC 12-x nordic-o capture . nordic . pcap**

当嗅探加密连接时，`ll_phdr`导出类型很有用，因为它也受[裂纹](https://github.com/mikeryan/crackle)的支持。因此，如果你想嗅探和打破加密连接，这是一条路要走。

您可能还需要通过使用-s 选项来告诉 crackle 使用特定的破解策略:

**$ crackle -i some.pcap -s 1**

**连接缓存**

Btlejack 使用一个*连接缓存*来存储一些与连接相关的值，以便稍微加快速度。这种连接缓存可能会导致一些问题，尤其是在访问地址之前已经出现的情况下。

可以使用`-z`选项刷新该缓存:

**$ btlejack -z**

**用 Wireshark 倾倒直播包**

Btlejack 2.0 引入了一个新的 *-w* 选项，允许您指定一个 FIFO 路径(存在或不存在)，以便执行数据包实时分析:

**$ btlejack-c any-w/tmp/blepipe**

你甚至可以同时使用 FIFO 和输出文件:

**$ btlejack-c any-w/tmp/blepipe-o blepackets . pcap**

**在树莓派上使用 btlejack 的提示**

如果您之前已经启用了**USB 虚拟以太网** (RNDIS)，例如通过 USB 设置 Raspberry Pi Zero W，您需要再次禁用它(即从 boot/config.txt 中删除`dtoverlay=dwc2`，从 boot/cmdline.txt 中删除`modules-load=dwc2,g_ether`，然后再删除`sudo reboot`，因为这将干扰嗅探器的 USB 连接。

**蓝牙乐 5 & 5.1 支持**

该版本支持蓝牙低能耗版本 5 和 5.1，特别是版本 5 (CSA #2)中引入的新的*频道选择算法*。然而，由于使用的硬件不支持从版本 5 添加的两个新的 PHY，它将只能使用 **1Mbps 未编码的 PHY** 来嗅探、阻塞甚至劫持连接。

还请注意，Btlejack 中包含的 CSA #2 的当前实现暂时不支持频道映射更新。

**嗅探新 BLE 5 号的连接**

Btlejack 会自动检测所使用的通道选择算法，因此您不必担心，只需像往常一样捕获数据包。

**嗅探现有的 BLE 5 连接**

嗅探现有的 BLE 5 连接(使用 1Mbps 未编码的 PHY，只有这个 PHY)并不困难。首先，您必须通过使用 *-5* 选项来指定您想要将 BLE 5 连接作为目标。请注意，没有办法判断现有的连接是使用 CSA #2 还是 CSA #1，所以您必须尝试这两种技术，直到其中一种工作为止。

**$ btlejack -f 0x11223344 -5**

Btlejack 随后将恢复所使用的频道映射，然后恢复跳跃间隔值:

$ btlejack -f 0x11223344 -5
[i]与连接 0x11223344 同步…
CRCInit:0x 40 d64f
通道映射= 0x1fffffffff
跳间隔= 160

然后，它将尝试恢复此连接 PRNG 计数器值:

$ btlejack -f 0x11223344 -5
[i]与连接 0x11223344 同步…
【CRCInit:0x 40 d64 f
【通道映射= 0x1fffffffff
【跳间隔= 160
cs a2 PRNG 计数器= 5137
【I】同步，数据包捕获进行中…

一旦完成，Btlejack 就与这个连接同步，并将照常处理数据包。

**堵塞现有的 BLE 5 连接**

这里没有什么新东西，除了您必须使用 *-5* 选项指定您正在攻击的是 BLE 5 连接。

请注意，您还可以通过分别使用 *-m* 和 *-p* 标志来指定要使用的信道映射和跳跃间隔值，从而优化这种攻击。这两者都必须提供，除非行不通。

**劫持现有的 BLE 5 号连接**

我没有设法在这个时候劫持 BLE 5 连接，因为这次攻击是时间敏感的。我的 BLE 5 设备使用的延迟为 0，因此不允许任何延迟，导致这次攻击失败。

当我得到一些合法的 BLE 5 设备时，我会改进它。

[**Download**](https://github.com/virtualabs/btlejack)