# PF_RING:高速数据包处理框架

> 原文：<https://kalilinuxtutorials.com/pf_ring/>

PF_RING 是一个 Linux 内核模块和用户空间框架，它允许您高速处理数据包，同时为数据包处理应用程序提供一致的 API。

基本上每个人都必须每秒处理许多数据包。术语“许多”根据您用于流量分析的硬件而变化。

范围从 1,2GHz ARM 上的 80k 包/秒到低端 2,5GHz Xeon 上的 15M 包/秒及以上。它不仅使您能够更快地捕获数据包，还能更有效地捕获数据包，从而节省 CPU 周期。

**又读:** [nDPI:开源深度包检测软件工具包](https://kalilinuxtutorials.com/ndpi-packet-inspection-toolkit/)

**从 GIT 安装**

它可以从 https://github.com/ntop/PF_RING/的 GIT 下载源代码格式，或者使用我们在 http://packages.ntop.org 的仓库从软件包安装，如从软件包安装一节所述。在本章中，我们将介绍从源代码安装。

克隆我们的库以下载 PF_RING 源代码:

git 克隆 https://github.com/ntop/PF_RING.git

PF_RING 源代码包括:

*   用户空间 SDK。
*   libpcap 的增强版本，它透明地利用了 PF_RING。
*   PF_RING 内核模块。
*   PF_RING ZC 驱动。

**内核模块安装**

为了编译内核模块，你需要安装 linux 内核头文件(或者内核源码)。

CD PF _ RING/kernel
make
sudo make install

**运行 PF_RING**

在使用任何应用程序之前，应该加载 pf_ring 内核模块:

cd PF_RING/kernel
sudo insmod。/pf _ ring . ko[最小数量插槽= N][启用发送捕获=1|0] [启用 ip 碎片整理=1|0]

其中:

**min_num_slots**
内核模块应该能够入队的最小数据包数量(默认值–4096)。
**enable _ TX _ capture** 置 1 捕获输出数据包，置 0 禁用捕获输出数据包(默认–RX+TX)。
**enable _ ip _ defrag** 置 1 启用 IP 碎片整理，仅对 RX 流量进行碎片整理(默认–禁用)

**举例:**

CD PF _ RING/kernel
sudo insmod PF _ RING . ko min _ num _ slots = 65536 enable _ tx _ capture = 0

**司机**

如果您想在英特尔适配器上实现 10 千兆位及以上的线速数据包捕获，您应该使用 ZC 驱动程序。您可以使用 ethtool 检查驱动程序系列:

ethtool -i eth1 | grep 驱动程序
驱动程序:ixgbe

并使用 driver 文件夹中的 load_driver.sh 脚本加载相应的驱动程序:

CD PF _ RING/drivers/Intel
make
CD IX gbe/IX gbe-*-ZC/src
sudo。/load_driver.sh

**Libpfring 和 Libpcap 安装**

libpfring 和 libpcap 都是以源代码格式发布的。它们可以按如下方式编译和安装:

cd PF_RING/userland/lib
。/configure&make
sudo make 安装
光盘../libpcap
。/configure&make
sudo make install

注意，传统的基于静态链接 pcap 的应用程序需要针对新的支持 PF_RING 的 libpcap.a 进行重新编译，以便利用它。在这种情况下，不要期望在没有重新编译现有应用程序的情况下使用它。

[**Download**](https://github.com/ntop/PF_RING)