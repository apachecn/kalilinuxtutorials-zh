# PFQ:多核架构的功能网络框架

> 原文：<https://kalilinuxtutorials.com/pfq-functional-network-framework/>

PFQ 是一个为 Linux 操作系统设计的功能框架，旨在实现高效的数据包捕获/传输(10G、40G 及以上)、内核内功能处理、内核旁路和跨多组套接字/端点的数据包控制。

它针对多核架构以及配备多个硬件队列的网络设备进行了高度优化。

与任何网卡兼容，它提供了一个从源代码开始生成加速网络设备驱动程序的脚本。

PFQ 支持高性能网络应用程序的开发，它附带了一个定制版本的 libpcap，用于加速和并行化遗留应用程序。

此外，还包括一个为早期内核包处理设计的纯函数式语言:pfq-lang。

Pfq-Lang 受 Haskell 的启发，旨在定义运行在网络设备驱动程序之上的应用程序。通过 pfq-lang，可以构建高效的网桥、端口镜像、简单的防火墙、网络平衡器等等。

该框架包括 PFQ 内核模块的源代码、用于 C、C++11-14、Haskell 语言的用户空间库、加速的 pcap 库、pfq-lang 作为 eDSL 用于 C++/Haskell 的实现、实验性的 pfq-lang 编译器和一组诊断工具。

**也可阅读-[Vuls:漏洞扫描器，用于 Linux/FreeBSD，无代理，用 Go](https://kalilinuxtutorials.com/vuls-vulnerability-scanner/) 编写，**

**特性**

*   具有全无锁架构的数据路径。
*   预先分配的套接字缓冲池。
*   兼容过多的网络设备驱动程序。
*   10 千兆位链路(14.8 Mpps)上的 Rx 和 Tx 线速，使用英特尔 ixgbe *vanilla* 驱动程序进行测试。
*   内核线程对异步数据包传输的透明支持。
*   带有活动时间戳的传输。
*   支持多个多线程应用并发监控的套接字组。
*   通过随机化散列或确定性分类的按组分组导向。
*   每组贝克莱和 VLAN 过滤器。
*   C、C++11-14 和 Haskell 语言的用户空间库。
*   使用 **pfq-lang** 进行内核数据包处理的功能引擎。
*   用于 C++11-14 和 Haskell 语言的 pfq-lang eDLS。
*   **pfq-lang** 编译器用于解析和编译 pfq-lang 程序。
*   面向传统应用的加速 pcap 库(使用 [captop](https://github.com/awgn/captop) 进行线速测试)。
*   I/O 用户内核内存映射通信分配在大页面之上。
*   用于配置和并行化(pcap)传统应用的 pfqd 守护进程。
*   自动加速普通驱动程序的脚本。

[**Download**](https://github.com/pfq/PFQ)

**鸣谢:尼古拉·博内利**