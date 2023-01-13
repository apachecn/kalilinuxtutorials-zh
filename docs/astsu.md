# Astsu:一个网络扫描工具

> 原文：<https://kalilinuxtutorials.com/astsu/>

[![Astsu : A Network Scanner Tool](img/4079e34298b3db15ba80cd187636c64a.png "Astsu : A Network Scanner Tool")](https://1.bp.blogspot.com/-qZkISs7p--E/XuE8xW1XFoI/AAAAAAAAGl4/8KLfMCqUbKgRttb1_73AV5SBWaBGlgNFwCLcBGAsYHQ/s1600/astsu%25281%2529.png)

Astsu 是一个网络扫描工具，使用 scapy 在 Python 3 中开发。

它是如何工作的？

*   **扫描公共端口:**在定义的端口上发送一个 TCP Syn 包到目的地，如果端口是开放的，使用 nmap 扫描检查端口上运行的服务并打印所有找到的端口。
*   **发现网络中的主机:**使用路由器的 ip 作为基础来映射所有可能的 IP。然后，它向每个 IP 发送一个 ICMP 数据包，并等待响应，如果它收到保存在联机主机的 IP 数组中的任何响应，当它检查完所有主机后，打印所有联机主机。
*   **操作系统扫描:**向目的地发送 ICMP 数据包，并等待响应。然后，从目标响应中提取 TTL，并检查列表中可能的 OS，如果找到了，就打印出来。

**如何安装？**

克隆这个库 **git 克隆 https://github.com/ReddyyZ/astsu.git**

*   **安装 python 3。**
    *   **Linux**
        *   apt-get 安装 python3
        *   chmod +x *
        *   python3 -m pip 安装要求. txt
        *   python3 install.py
        *   搞定了。
    *   **窗户**
        *   Python 3，下载并安装
        *   python3 -m pip 安装要求. txt
        *   python3 install.py
        *   搞定了。

**自变量**

*   **-sC |扫描公共端口**
    *   -p |扫描中使用的协议
    *   -i |要使用的接口
    *   -t |每个请求的超时
    *   -st |使用隐形扫描方法(TCP)
*   **-sA |扫描所有端口**
    *   -p |扫描中使用的协议
    *   -i |要使用的接口
    *   -t |每个请求的超时
    *   -st |使用隐形扫描方法(TCP)
*   **-sP |扫描范围端口**
    *   -p |扫描中使用的协议
    *   -i |要使用的接口
    *   -t |每个请求的超时
    *   -st |使用隐形扫描方法(TCP)
*   **-sO |扫描目标的操作系统**
*   **-d |发现网络中的主机**
    *   -p |扫描中使用的协议
    *   -i |要使用的接口

**操作系统支持**

*   **Windows** ✔️
*   **Linux** ✔️
*   **麦克** ❓

[**Download**](https://github.com/ReddyyZ/astsu)