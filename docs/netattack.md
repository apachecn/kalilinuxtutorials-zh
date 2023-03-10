# 网络攻击–扫描和攻击无线网络

> 原文：<https://kalilinuxtutorials.com/netattack/>

NETATTACK 或 netattack.py 是一个 python 脚本，使您能够检查您的本地 WiFi 网络并执行取消身份验证攻击。这个脚本的生存能力和能力非常依赖于你的无线网卡。

## **网攻 2 发布**

```
https://github.com/chrizator/netattack2/
```

#### **也读作[WMD——大规模杀伤性武器](http://kalilinuxtutorials.com/wmd-weapon-mass-destruction/)**

## **用法**

#### **扫描 WIFI 网络**

```
python netattack.py -scan -mon 
```

此示例将执行 WiFi 网络扫描。BSSID、ESSID 和信道将在表格中列出。

```
-scan | --scan 
```

当您想要进行扫描时，必须调用此参数。这是主要命令之一。它正在搜索路由器发送的信标帧，以通知其存在。

```
-mon | --monitor 
```

通过调用这个参数，脚本自动检测您的无线网卡，并将其置于监控模式，以捕获正在进行的流量。如果您知道无线网卡的名称，并且它已经在监控模式下工作，您可以拨打

```
-i 
```

这个可以用来代替`-mon`。

#### **解除认证攻击**

```
python netattack.py -deauth -b AB:CD:EF:GH:IJ:KL -u 12:34:56:78:91:23 -c 4 -mon 
```

该命令显然会执行取消身份验证攻击。

```
-deauth | --deauth 
```

该参数是扫描的主要参数。如果你想对某个目标进行远程攻击，呼叫是必要的。

```
-b | --bssid 
```

使用`-b`选择 AP 的 MAC 地址(BSSID)。`-deauth`参数需要一个或多个 BSSID

```
-u | --client 
```

如果不想攻击整个网络，而是单个用户/客户端/设备，可以用`-u`来做到这一点。没有必要。

```
-c | --channel 
```

通过添加此参数，您的解除身份验证攻击将在进入的通道上执行。强烈建议使用`-c`，因为如果使用了错误的通道，攻击将会失败。AP 的信道可以通过做 WiFi 扫描来看(`-scan`)。如果你不添加`-c`，攻击将发生在当前频道。

`-mon`或`-i`也是这次攻击的目标。

#### **对每个人的去认证攻击**

```
python netattack.py -deauthall -i [IFACE] 
```

当调用这个命令时，脚本会自动搜索您所在区域的 AP。搜索之后，它开始攻击所有找到的接入点。`-deauthall`参数只需要一个接口就可以工作。注意:如果你想让所有这些攻击尽可能高效，请看下面的“高级”部分。

## **要求**

*   Python 2.5+(不是 Python 3+)
*   模块:
    *   scapy
    *   抱怨吗
    *   [计]系统复制命令（system 的简写）
    *   操作系统（Operating System）
    *   穿线
    *   记录
*   iw(配置)
*   OFC LINUX

## **免责声明和许可**

本软件的所有者和生产者不对本软件造成的任何损害或任何违法行为负责。

[![](img/a51de913dc60eee505c4a68651ee8e4d.png)](https://github.com/chrizator/netattack)