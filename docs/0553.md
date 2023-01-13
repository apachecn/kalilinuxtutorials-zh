# Anevicon:一个基于 UDP 的高性能负载生成器

> 原文：<https://kalilinuxtutorials.com/anevicon/>

Anevicon 是一个高性能的流量生成器，设计得尽可能方便可靠。

它向服务器发送大量 UDP 数据包，从而模拟可能由您的最终用户或一群黑客发起的活动。

该工具还可以用作 bot 来构建僵尸网络，用于模拟 UDP 洪水攻击(但仅用于教育和测试目的)。

这是通过这个程序所依赖的 Anevicon 核心库实现的。

**特性**

*   **用铁锈写的。**你可以看到，Anevicon 完全是用 [Rust](https://www.rust-lang.org/) 编写的，这意味着它利用了高水平的安全性和裸机性能，通过零成本抽象实现。
*   **Linux 加速。Anevicon 不仅仅是为基于 Linux 的操作系统开发的。它使用 [sendmmsg](http://man7.org/linux/man-pages/man2/sendmmsg.2.html) 系统调用与内核交互，一次传输多条消息。**
*   **功能。**我试图实现尽可能多的东西来制作一个多功能工具，同时保持简单。支持多项测试、冗长级别、IP 欺骗等功能。

**安装**

目前，该项目需要不稳定的标准库功能，因此这就是为什么您必须切换到夜间频道以避免编译错误:

**$ rustup 覆盖设置每夜**

**板条箱建筑**

**$货物安装设备**

**从源构建**

**$ git 克隆 https://github.com/Gymmasssorla/anevicon.git $ CD anevicon $ cargo build–release**

**预编译的二进制文件**

在您的系统上运行 Anevicon 最简单的方法是从[现有版本](https://github.com/Gymmasssorla/anevicon/releases)下载预编译的二进制文件，这不需要任何外部软件(不像前两种方法)。

**选项**

**anevicon 5 . 0 . 3
Temirkhan Myrzamadi**[**gymmasssorla@gmail.com**](mailto:gymmasssorla@gmail.com) **一款基于 UDP 的服务器压力测试工具，用 Rust 编写。
用法:
anevicon[FLAGS][OPTIONS]–receiver…
FLAGS:
-b，–Allow-broadcast 允许套接字发送数据包到一个广播
地址
-h，–help 打印帮助信息
-V，–version 打印版本信息
OPTIONS:
–date-time-format
一种在日志消息中显示本地日期和时间的格式。键入** `**man strftime**` **查看格式规范
当您希望测试一个服务器超过一天时，指定不同的星期格式可能会有所帮助
。[默认:%X]
-l，–packet-length
重复发送随机生成的指定字节长度的数据包
。默认为 32768
-p，–数据包计数
发送的数据包数。当达到此限制时，
程序将退出[默认值:18446744073709551615]
–每系统调用数据包数
程序将仅使用一个
系统调用发送的数据包数。操作完成后，测试摘要将被打印出来。
出于某些
性能原因，不建议将该选项设置为低值。[default: 600]
-r，–receiver…
生成的流量的接收者，指定为 IP 地址和
端口号，用冒号分隔。
该选项可多次指定，以并行模式测试多个
接收器。
将对所有接收器进行相同的测试。运行该程序的多个
实例来描述每个接收器的具体特征。
-f，–send-file
将指定的文件内容解释为单个数据包，并
将其重复发送给每个接收者
-m，–send-message
将指定的 UTF-8 编码文本消息解释为单个
数据包，并将其重复发送给每个接收者
–send-periodicity
send mmsg 系统调用之间的时间间隔。该选项可用于
降低测试强度【默认:0 秒】
-t，–发送超时
发送每个数据包的超时。如果达到超时，
则稍后将发送数据包。[default: 10secs]
-s，–sender
生成的流量的发送方，指定为 IP 地址和端口号
，用冒号分隔[default: 0.0.0.0:0]
-d，–test-duration
整个测试持续时间。当达到该极限时，程序
将退出。由于长时间的 sendmmsg 系统调用，可能会在几秒钟后退出。为了更加精确，减小** `**--packets-per-syscall**` **的值。[默认值:64 年 64 小时 64 秒]
-v，–详细度
启用一个可能的详细度级别。零级
不打印任何东西，最后一级打印所有东西【默认值:3】
【可能值:0，1，2，3，4，5】
-w，–wait
测试执行前的一段等待时间，用于防止错误(不想要的)测试的启动
【默认值:5 秒】
更多信息参见**[**https://github.com/Gymmasssorla/anevicon**](https://github.com/Gymmasssorla/anevicon)

 **另读—[2018 年最受欢迎的黑客工具](https://kalilinuxtutorials.com/most-popular-hacking-tools-in-2018/)

**用作程序**

**最小命令**

您只需要提供测试服务器地址，该地址由一个 IP 地址和一个端口号组成，用冒号分隔。默认情况下，所有发送套接字都有您的本地地址:

#使用您的本地地址测试 example.com 站点的 80 端口$ anevicon–接收方 93.184.216.34:80

**多个接收器**

Anevicon 还具有以并行模式测试多个接收器的功能，从而将负载分配到您的处理器内核上。为此，只需多次指定`--receiver`选项。

#并行测试 example.com 的 80 端口和 google.com 的 13 端口$ anevicon–接收方 93.184.216.34:80–接收方 216.58.207.78:13

**IP 欺骗**

使用 IP 欺骗技术，黑客可以保护他们的带宽免受服务器响应消息的影响，并隐藏他们的真实 IP 地址。您可以通过`--sender`命令行选项模仿它，如下所述:

#使用自己的 IP 地址测试 example.com 站点的 80 端口$ anevicon–接收方 93.184.216.34:80–发送方 93.184.216.34:80

**结束条件**

请注意，由于安全原因，上面的命令可能无法在您的系统上运行。为了使您的测试具有确定性，有两个结束条件叫做`--test-duration`和`--packets-count`(分别是测试持续时间和数据包计数):

#使用两个限制选项测试 example.com 站点的 80 端口$ anevicon–接收器 93.184.216.34:80–测试持续时间 3 分钟–数据包计数 7000

**数据包大小**

请注意，当且仅当两个指定的结束条件之一为真时，下面的测试才会结束。此外，您可以用字节指定全局数据包长度:

#用 4092 字节的数据包长度测试 example.com 的 80 端口$ anevicon–接收方 93.184.216.34:80–数据包长度 4092

**自定义消息**

默认情况下，Anevicon 会生成一个指定大小的随机数据包。在某些基于 UDP 的测试中，数据包内容是有意义的，这就是你如何使用`--send-file`或`--send-message`选项来指定它:

#使用自定义文件' message . txt ' $ anevicon–receiver 93.184.216.34:80–send-file message . txt
#使用自定义文本消息$ anevicon–receiver 93.184.216.34:80–send-message“你好吗？”

**测试强度**

在某些情况下，您不需要传输尽可能多的数据包，您可能希望降低数据包发送的强度。为此，有一个更简单的选项叫做`--send-periodicity`。

#测试 example.com，在每次发送 mmsg 系统调用$ anevicon–接收器 93.184.216.34:80–发送之后等待 270 微秒-周期 270 微秒

**详细等级**

Anevicon 支持从 0 到 5 的几个详细级别。零级不打印任何内容，第一级只打印错误，第二级添加警告，第三级添加通知，第四级添加调试，第五级-跟踪。

#使用第四详细级别$ anevicon 接收器 93.184.216.34:80-详细级别 4 测试 example.com 的 80 端口

**日期时间格式**

您可以明确指定用于显示每条日志消息的自定义日期时间格式。如果您想在一天以上的时间内测试某些东西，设置日期和周的格式可能会有所帮助:

#使用显示月、日、年、小时、分钟和秒的格式进行测试$ a 接收机 93.184.216.34:80-日期-时间-格式" %D %X "

**每个系统调用的数据包**

出于性能原因，Anevicon 默认使用 [sendmmsg](http://man7.org/linux/man-pages/man2/sendmmsg.2.html) syscall，显著降低了 CPU 使用率。还支持指定每个系统调用发送的数据包数量。

#测试 example.com 站点的 80 端口，每个系统调用 1200 个数据包$ anevicon–接收器 93.184.216.34:80–每个系统调用 1200 个数据包

**发送超时**

网络操作有时不会立即执行。这就是为什么程序支持代表持续时间的`--send-timeout`选项，在此之后，如果没有发送数据包，将会显示一个错误。

#使用 200 毫秒的超时时间测试 example.com 站点的 80 端口$ anevicon–receiver 93.184.216.34:80–send-time out 200 毫秒

**测试前等待**

系统中最脆弱的部分是位于电脑和椅子之间的物体。因此，为了防止执行错误的测试，有一个默认情况下等待 5 秒钟的`--wait`选项:

#测试 example.com 站点，在执行之前等待 30 秒$＄anevicon–接收方 93.184.216.34:80–等待 30 秒

**信用:Temirkhan Myrzamadi**

[**Download**](https://github.com/Gymmasssorla/anevicon)**