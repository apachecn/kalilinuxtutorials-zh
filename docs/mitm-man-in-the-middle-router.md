# MITM:中间人路由器

> 原文：<https://kalilinuxtutorials.com/mitm-man-in-the-middle-router/>

将任何 linux PC 变成一个开放 Wi-Fi，安静地组织 mitm 或中间人所有 http 活动。保持在 Docker 容器内运行，利用 hostapd、dnsmasq 和 mitmproxy 创建一个名为“open”的开放式蜜罐远程系统。对于包含的乐趣，将系统名称更改为“xfinitywifi ”,以自动连接任何曾经与这些系统关联的个人……它们都结束了。

```
# clone the repo
git clone https://github.com/brannondorsey/mitm-router
cd mitm-router

# build the image this step can be omitted if you prefer to pull 
# the image from the docker hub repository
docker build . -t brannondorsey/mitm-router
```

运行以下程序，分别用您的无线设备和连接互联网的以太网/无线设备替换`AP_IFACE`和`INTERNET_IFACE`。你可以通过运行`ifconfig`来查看你的网络设备的名称。

**也读 [WiFi 密码解密器软件恢复无线密码](http://kalilinuxtutorials.com/wifi-password-decryptor/)**

```
# run the container
docker run -it --net host --privileged \
-e AP_IFACE="wlan0" \
-e INTERNET_IFACE="eth0" \
-e SSID="Public" \
-v "$(pwd)/data:/root/data" \
brannondorsey/mitm-router
```

如果一切顺利，您应该会看到如下内容:

```
Current MAC:   a5:ae:f9:a4:b7:e3 (TP-LINK TECHNOLOGIES CO.,LTD.)
Permanent MAC: a5:ae:f9:a4:b7:e3 (TP-LINK TECHNOLOGIES CO.,LTD.)
New MAC:       00:d2:6b:d5:fe:bd (PHOTRON USA)
[ ok ] Starting system message bus: dbus.
[ ok ] Starting DNS forwarder and DHCP server: dnsmasq.
[ ok ] Starting advanced IEEE 802.11 management: hostapd.
Proxy server listening at http://0.0.0.0:1337 
```

`mitm-router`透明地捕获发送到`10.0.0.1:80`路由器的所有`HTTP`流量。它不会**而不是**拦截 HTTPS 流量(端口`443`，因为这样做会提醒用户可能发生了中间人攻击。以`https://`开头的 URL 之间的流量不会被捕获。

文件夹`**mitm-router/data/**`与 docker 容器共享，因此我们可以查看它放在主机上的捕获文件。默认情况下，你会在 `**mitm-router/data/http-traffic.cap**`中找到 **`mitmdump`** 抓图文件。

您还可以随时将您的`INTERNET_IFACE`连接到手机上运行的主机上😉

## **配置中间人** 

下面列出了支持的环境变量及其默认值:

```
# wireless device name that will be used for the Access Point
AP_IFACE="wlan0"

# device name that is used for the router's internal internet connection
# packets from AP_IFACE will be forwarded to this device
INTERNET_IFACE="eth0"

# wireless network name
SSID="Public"

# optional WPA2 password; if left empty network will be public
PASSWORD=""

# optional randomization of AP_IFACE MAC address
# can be set to a specific value like "XX:XX:XX:XX:XX:XX"
# or "unchanged" to leave the device MAC alone
MAC="random"

# tcpdump output file location inside the container
CAPTURE_FILE="/root/data/http-traffic.cap"

# optional mitmproxy filter
# see http://docs.mitmproxy.org/en/stable/features/filters.html
FILTER=""
```

该接入点运行在 Docker 内部进行隔离，确保接入点中任何可能被利用的漏洞都不会允许对手访问您的计算机或家庭网络。也就是说，需要注意一些警告:

*   **–网络主机**与 docker 容器共享来自主机的所有网络接口和 **iptables** 条目。假设易受攻击的 docker 容器拥有对这些设备的超级用户访问权限。
*   在**–特权**模式下运行给予 docker 容器扩展的权限
*   您的主机(运行 docker 的那台)**将**作为一个连接的客户端在“公共”网络上可访问。因此，请使用防火墙(linux 上的 ufw)来阻止所有端口上的传入流量，以便“公共”网络上的计算机无法访问您机器上公开的服务。
*   蜜罐网络上的所有流量都将从您家庭网络的网关流出。如果有人在“公共”网络上进行非法活动，你将被追究责任，你的 ISP 可能会取消你的服务。

为了增加安全性，我更喜欢在专用计算机上运行这个 docker 容器，比如 Raspberry Pi。

[![](img/a51de913dc60eee505c4a68651ee8e4d.png)](https://github.com/brannondorsey/mitm-router)