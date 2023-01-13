# nDPI:开源深度包检测软件工具包

> 原文：<https://kalilinuxtutorials.com/ndpi-packet-inspection-toolkit/>

nDPI 是一个用于深度数据包检测的开源 LGPLv3 库。基于 OpenDPI，它包括了 ntop 扩展。我们试图将它们放入 OpenDPI 源码树，但是没有人回复邮件，所以我们决定创建自己的源码树。

**也读作:** B [incat:集成 IDA 的二进制代码静态分析器](https://kalilinuxtutorials.com/bincat-binary-code-static-analyser/)

**如何编译 nDPI**

为了编译这个库做什么

*   ./autonom . sh
*   。/配置
*   制造

要运行测试，还需要:

*   光盘测试；。/do.sh

请注意，编译的先决条件包括:

*   GNU 工具(autogen，automake，autoconf，libtool)
*   GNU C 编译器(gcc)

**如何添加新的协议解析器**

详细介绍添加新协议的整个过程:

1.  将新协议及其唯一 ID 添加到:src/include/ndpi _ protocol _ ids . h
2.  在 src/lib/protocols/中创建一个新协议
3.  要在整个流的持续时间内保留的变量(作为状态变量)需要放在:src/include/ndpi _ typedefs . h in ndpi _ flow _ tcp _ struct(仅适用于 TCP)、ndpi_flow_udp_struct(仅适用于 udp)或 ndpi_flow_struct(适用于两者)中。
4.  在 src/include/ndpi_protocols.h 中为新协议的搜索功能添加一个新条目
5.  从 src/include/ndpi_define.h 中选择(不做任何更改)一个选择位掩码
6.  在 src/lib/ndpi_main.c 中的 ndpi _ set _ protocol _ detection _ bitmask 2 中添加一个新条目
7.  在 src/lib/ndpi_main.c 中的 ndpi_init_protocol_defaults 中设置协议默认端口
8.  ./autonom . sh
9.  制造
10.  进行检查

**如何使用 nDPI 阻止选定的流量**

您可以使用 nDPI 通过将其嵌入到应用程序中来选择性地阻止选定的互联网流量(请记住，nDPI 只是一个库)。恩托普恩和 T2【n】探测器森托都能做到这一点。

**创建源文件焦油球**

如果您想要分发 nDPI 的源 tar 文件，请执行以下操作:

*   制作区域

要确保 tar 文件包含所有必需的文件，并在发行版上运行测试，请执行以下操作:

*   进行远程检查

**免责声明**

虽然我们尽最大努力检测网络协议，但我们不能保证我们的软件在协议检测中没有错误并且 100%准确。请确保您尊重用户的隐私，并且您有适当的授权来监听、捕获和检查网络流量。

[**Download**](https://github.com/ntop/nDPI)