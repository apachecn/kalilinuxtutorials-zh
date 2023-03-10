# kemon——一个用于 macOS 内核监控的基于开源前后回调的框架

> 原文：<https://kalilinuxtutorials.com/kemon-macos-kernel-monitoring/>

Kemon 是一个开源的基于回调前后的框架，用于 macOS 内核监控。借助它的力量，我们可以轻松实现 LPC 通信监控、MAC 策略过滤、内核驱动防火墙等。一般来说，从攻击者的角度来看，这个框架可以帮助实现更强大的 Rootkit。从防御的角度来看，它可以帮助构建更细粒度的监控功能。我还通过这个框架实现了一个内核 fuzzer，帮我发现了很多漏洞，比如:CVE-2017-7155，CVE-2017-7163，CVE-2017-13883 等

**又读[social box——一个暴力攻击框架【脸书，Gmail，Instagram，Twitter】](https://kalilinuxtutorials.com/socialbox-bruteforce-attack/)**

## **支持的功能**

功能包括:

*   文件操作监控
*   流程创建监控
*   动态库和内核扩展监控
*   网络流量监控
*   强制访问控制(MAC)策略监控等。

此外，该项目还可以为任何 macOS 内核函数扩展基于回调的前后监控接口。

## **入门**

### **如何使用？** 

*   如果您没有有效的内核证书，请关闭 macOS 系统完整性保护(SIP)检查
*   使用命令“sudo chown-R root:wheel kemon . kext”来更改驱动程序的所有者
*   使用命令“sudo kextload kemon.kext”安装驱动程序
*   使用命令“sudo kextunload kemon.kext”卸载驱动程序

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/didi/kemon)