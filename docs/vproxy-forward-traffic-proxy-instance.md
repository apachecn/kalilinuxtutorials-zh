# v Proxy–将 HTTP/S 流量转发到代理实例

> 原文：<https://kalilinuxtutorials.com/vproxy-forward-traffic-proxy-instance/>

Vproxy 工具用于将 HTTP/S 流量转发到代理实例。移动设备中的 WIFI 代理选项不会让您使用最喜欢的代理程序捕获所有 HTTP/S 流量？使用此工具解决此问题并捕获整个 HTTP/S 流量。

## **Vproxy 系统要求**

*   **Linux**
*   **Python 2.x**

**也可理解为 [Win-PortFwd : Powershell 脚本使用本地 Netsh 客户端](https://kalilinuxtutorials.com/win-portfwd/)** 设置 Windows 端口转发

## **先决条件**

```
pip install termcolor
```

## **用途**

*   在 localip 上设置 VPN 服务器，并将从设备发送的流量重定向到代理实例
*   在 localip 上设置 VPN 服务器并监控来自设备的流量
*   在 localip 上设置 VPN 服务器，并将发送到 192.168.1.0/24 的流量重定向到代理实例

```
$sudo python vproxy.py -ip [LOCALIP] -port [PORTLIST] -proxy [PROXYHOST:PROXYPORT] -mode Redirect
```

```
$sudo python vproxy.py -ip [LOCALIP]  -port [PORTLIST] -mode Monitor
```

```
$sudo python vproxy.py -ip [LOCALIP] -port [PORTLIST] -proxy [PROXYHOST:PROXYPORT] -int 192.168.1.0/24 -mode Redirect
```

## **限制**

证书锁定

## **配置虚拟专用网视频**

### ios

[https://www.youtube.com/embed/TC-xJ9rCTXU?feature=oembed](https://www.youtube.com/embed/TC-xJ9rCTXU?feature=oembed)

### **安卓**

[https://www.youtube.com/embed/bFeJZKX4O3A?feature=oembed](https://www.youtube.com/embed/bFeJZKX4O3A?feature=oembed)

[![https://github.com/Nekmo/dirhunt](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/B4rD4k/Vproxy)