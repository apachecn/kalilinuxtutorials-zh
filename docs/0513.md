# Pyrit:著名的 WPA 预计算破解程序，从 Google 移植而来

> 原文：<https://kalilinuxtutorials.com/pyrit-wpa-precomputed-cracker-google/>

Pyrit 允许你在一个空间-时间权衡中创建预先计算的 WPA/WPA2-PSK 认证阶段的大规模数据库。

通过 ATI-Stream、Nvidia CUDA 和 OpenCL 使用多核 CPU 和其他平台的计算能力，这是目前针对世界上最常用的安全协议之一的最强大的攻击。

WPA/WPA2-PSK 是 IEEE 802.11 WPA/WPA2 的子集，它通过为每个参与方分配相同的预共享密钥，跳过了复杂的密钥分发和客户端验证任务。

**又念——[insta anane:多线程 Instagram 蛮力器](https://kalilinuxtutorials.com/instainsane-instagram-brute-forcer/)**

该主密钥源自管理用户必须在例如他的膝上型电脑和接入点上预先配置的密码。当笔记本电脑创建到接入点的连接时，会从主密钥中导出一个新的会话密钥来加密和验证后续流量。

使用单个主密钥而不是每个用户密钥的“捷径”简化了家庭和小型办公室使用的 WPA/WPA2 保护网络的部署，代价是使协议容易受到针对其密钥协商阶段的暴力攻击；它允许最终泄露保护网络的密码。

这个漏洞被认为是灾难性的，因为该协议允许预先计算大部分密钥派生，使得简单的暴力攻击对攻击者更有吸引力。要了解更多背景信息，请参见该项目的博客(已过时)上的这篇文章。

作者不鼓励或支持使用 Pyrit 侵犯人们的通信隐私。

这里讨论的技术的探索和实现把激励作为它们自己的目的；这在开放开发、严格基于源代码的分发和“版权所有”许可中都有记载。

Pyrit 是自由软件——自由就是自由。每个人都可以在 GNU 通用公共许可证 v3+下检查、复制或修改它并共享衍生作品。

它可以在各种平台上编译和执行，包括 FreeBSD、MacOS X 和 Linux 操作系统以及 x86、alpha、arm、hppa、mips、powerpc、s390 和 sparc 处理器。

通过蛮力攻击 WPA/WPA2 归结为尽快计算成对主密钥。

每一个成对的主密钥都“相当于”通过 PBKDF2-HMAC-SHA1 推送的 1 兆字节的数据。反过来，每秒计算 10.000 PMKs 相当于在一秒钟内用 SHA1 散列 9.8 千兆字节的数据。

以下是多个计算节点如何通过 Pyrit 提供的各种方式访问单个存储服务器的示例:

*   单一存储(例如 MySQL 服务器)
*   一个本地网络，可以直接访问存储服务器，并在不同级别上提供四个计算节点，其中只有一个节点实际访问存储服务器本身。
*   另一个不受信任的网络可以通过 Pyrit 的 RPC 接口访问存储，并提供三个计算节点，其中两个实际上访问 RPC 接口。

**最新消息**

*   修复了#479 和#481
*   Pyrit CUDA 现在在 OSX 用工具包 7.5 编译
*   在配置文件中添加了 use_CUDA 和 use_OpenCL
*   改进的核心列表和管理
*   当设置为值< = 0 时，limit_ncpus 现在禁用所有 CPU
*   由于 yannayl，改进了 CCMP 数据包识别

有关更好的描述，请参见 CHANGELOG 文件。

**如何使用**

Pyrit 在 Linux、MacOS X 和 BSD 上编译并运行良好。我不关心 Windows 如果你不用复制一半 GNU 就能让 Pyrit 工作，请给我写封短信(读:补丁)

在 wiki 中可以找到在您的系统上安装 Pyrit 的指南。还有一个[教程](https://github.com/JPaulMora/Pyrit/wiki/Usage)和一个[参考手册](https://github.com/JPaulMora/Pyrit/wiki/ReferenceManual)供命令行客户端使用。

**如何参与**

如果你对把 Pyrit 移植到新的硬件平台感兴趣，你可能想读一下这个 wiki 条目。您应该[提交问题](https://github.com/JPaulMora/Pyrit/issues)的投稿或错误报告。

[**Download**](https://github.com/JPaulMora/Pyrit)