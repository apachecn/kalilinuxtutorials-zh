# Trommel:筛选嵌入式设备文件以识别潜在的易受攻击的指示器

> 原文：<https://kalilinuxtutorials.com/trommel-embedded-vulnerable-indicators/>

TROMMEL 筛选嵌入式设备文件，以识别潜在的易受攻击的指示器。它确定了与以下方面有关的指标:

*   安全外壳(SSH)密钥文件
*   安全套接字层(SSL)密钥文件
*   互联网协议(IP)地址
*   统一资源定位器(URL)
*   电子邮件地址
*   外壳脚本
*   web 服务器二进制文件
*   配置文件
*   数据库文件
*   特定的二进制文件(即 Dropbear、BusyBox 等。)
*   共享对象库文件
*   web 应用程序脚本变量，以及
*   Android 应用程序包(APK)文件权限。

它还集成了 [vFeed](https://vfeed.io/) ，允许对已确定的指标进行进一步深入的脆弱性分析，以丰富输出。

**还看:**[Linux、Windows & Android](https://kalilinuxtutorials.com/ddos-linux-windows-android/) 前 5 名 DDoS 攻击工具

**用途**

$ Drummond . py 帮助

根据给定的目录将 TROMMEL 结果输出到文件中。默认情况下，仅搜索纯文本文件。

$ trommel . py-p/directory-o output _ file

根据给定的目录将 TROMMEL 结果输出到文件中。搜索二进制和纯文本文件。

$ trommel . py-p/directory-o output _ file-b

**注释**

*   旨在帮助研究人员在固件分析过程中发现潜在的漏洞
*   网络维护者也可以受益于评估其网络上的设备或他们计划添加到其网络中的设备
*   设备可以包括物联网(网络摄像头)、智能设备(灯泡、插头、开关、电视、冰箱、咖啡机等。))、SCADA/ICS、路由器，实际上是任何具有嵌入式闪存芯片的设备，该芯片在启动时启动操作系统。
*   TROMMEL 已经在 Kali Linux x86_64 上使用 Python3 进行了测试。

[**Download**](https://github.com/CERTCC/trommel)

**鸣谢:凯尔·奥米拉**