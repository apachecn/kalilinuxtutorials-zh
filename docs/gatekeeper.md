# 看门人:第一个开源 DDoS 保护系统

> 原文：<https://kalilinuxtutorials.com/gatekeeper/>

[![Gatekeeper : First Open-Source DDoS Protection System](img/2eeb8b5f2563702e972856f5143f1e03.png "Gatekeeper : First Open-Source DDoS Protection System")](https://1.bp.blogspot.com/-eQ542xMYRMQ/YD_iO9IbuxI/AAAAAAAAIbc/aPdbwZhKAe4thRa-QSqQMgWd2QLJIilUgCLcBGAsYHQ/s728/DDoS%2BProtection%25281%2529.png)

**Gatekeeper** 是第一个开源的 DoS 保护系统。它被设计成可以扩展到任何峰值带宽，因此它可以抵御现在和将来的 DoS 攻击。尽管 Gatekeeper 的体系结构在地理上是分布式的，但描述必须对传入流量实施的所有决策的网络策略是集中式的。

这种集中策略使网络运营商能够利用在非常高的延迟下不可行的分布式算法(例如，分布式数据库)，并同时对抗多个多向量 DoS 攻击。

网守的目标用户是机构的网络运营商、服务和内容提供商、企业网络等。它不适合个人互联网用户使用。

**如何设置？**

**配置大页面**

DPDK 要求使用 hugepages 在[要求文件](http://doc.dpdk.org/guides/linux_gsg/sys_reqs.html#use-of-hugepages-in-the-linux-environment)中可以找到安装大型页面的说明。在许多系统上，以下 hugepages 设置就足够了:

**$ echo 256 | sudo tee/sys/kernel/mm/huge pages/huge pages-2048 kb/NR _ huge pages**

*   **选项 1:获取包**

debian gate keeper 包可以在项目的[发布版](https://github.com/AltraMayor/gatekeeper/releases)页面获得。

**安装**

下载完软件包后，可以使用以下命令安装它们:

```
$ tar -zxvf gatekeeper-ubuntu-18.04-packages.tar.gz
$ cd gatekeeper-ubuntu-18.04-packages
$ sudo dpkg -i libgkrte-*.deb \
    libgkdpdk-dev_*_amd64.deb \
    gatekeeper-dpdk_*_amd64.deb \
    gatekeeper-dpdk-dev_*_amd64.deb \
    gatekeeper-dpdk-igb-uio-dkms_*_amd64.deb \
    gatekeeper-dpdk-rte-kni-dkms_*_amd64.deb \
    gatekeeper-bird_*_amd64.deb \
    gatekeeper_*_amd64.deb 
```

`gatekeeper-dpdk-dev`包是 DKMS 包的一个依赖项，它在包安装和内核升级期间构建各自的内核模块。

**配置网络适配器**

编辑`/etc/gatekeeper/envvars`文件并插入要绑定到 DPDK 的网络适配器的名称。例如:

**网守 _ 接口= " eth 0 et h1"**

或者，可以指定接口的 PCI 地址:

**gate keeper _ INTERFACES = " 0000:00:07.0 0000:00:08.0 "**

在同一个文件中，您可以选择在`DPDK_ARGS`变量中指定[环境抽象层选项](https://doc.dpdk.org/guides/linux_gsg/linux_eal_parameters.html)，在`GATEKEEPER_ARGS`变量中指定[网关守卫特定选项](https://github.com/AltraMayor/gatekeeper/wiki/Configuration#application-configuration)。

**怎么跑？**

运行以下命令来启动网关守护设备，并确保它在重新启动时自动启动。

**$ sudo systemctl 启动网守
$ sudo systemctl 启用网守**

*   **选项 2:从源代码构建**

**安装依赖关系**

安装以下软件依赖项:

**$ sudo apt-get update
$ sudo apt-get-y-q install git clang dev scripts doxygen huge pages \
build-essential Linux-headers-`uname -r`libmnl 0 libmnl-dev \
libk mod 2 libk mod-dev libnuma-dev libel f1 libelf-dev libc 6-dev-i386 \
autoconf flex bison libncurses 5-dev libreadline-dev**

**注:**`libmnl0`和`libmnl-dev`都需要编译运行`gatekeeper`，而简单运行`gatekeeper`只需要`libmnl0`。编译和运行`gatekeeper`都需要`libkmod2`和`libkmod-dev`，但简单运行`gatekeeper`只需要`libkmod2`。`libnuma-dev`需要编译最新的 DPDK 并支持 NUMA 系统。需要包`libelf-dev`来编译 DPDK，支持从 ELF 文件中读取 BPF 程序，但是只需要`libelf1`来运行它。需要使用包`libc6-dev-i386`来编译文件夹`bpf/`中的 BPF 程序。`autoconf`、`flex`、`bison`、`libncurses5-dev`、`libreadline-dev`包是鸟用的。`devscripts`包用于构建网守 Debian 包。

要使用 DPDK，请确保您具备所有的[环境要求](http://dpdk.org/doc/guides/linux_gsg/sys_reqs.html#running-dpdk-application)。

**克隆存储库**

克隆网关守护设备存储库，包括包含网关守护设备依赖关系的子模块:

**$ git 克隆–递归 http://github.com/AltraMayor/gatekeeper.git**

如果不使用`--recursive`克隆选项，您需要从`gatekeeper`目录中获取包含依赖关系的子模块:

**$ git 子模块初始化
$ git 子模块更新**

**编译**

本节解释如何手动构建网关守护设备。如果你想构建 Debian 包，参考[如何构建包](https://github.com/AltraMayor/gatekeeper#how-to-build-packages)一节。

在`gatekeeper`目录中，运行设置脚本:

**$。setup.sh**

这个脚本编译 DPDK、LuaJIT 和 BIRD，并加载所需的内核模块。此外，它将接口名称及其各自的 PCI 地址保存在文件`lua/if_map.lua`中，以便接口名称可以在网守配置文件中使用。

它还设置了两个环境变量:`RTE_SDK`和`RTE_TARGET`。它们必须在`gatekeeper`编译之前设置好。

运行安装脚本后，您可能希望将环境变量保存在 shell 的首选项文件中。例如，在 Bash 中，您可以:

**$ echo " export RTE _ SDK = $ { RTE _ SDK } ">>$ { HOME }/。个人资料
$ echo " export RTE _ TARGET = $ { RTE _ TARGET } ">>
$ { HOME }/。个人资料**

否则，每次登录时，您都需要再次设置这些环境变量。

一旦编译了 DPDK 并设置了变量，就可以编译`gatekeeper`:

**$ make**

**配置网络适配器**

在使用`gatekeeper`之前，网络适配器必须绑定到 DPDK。为此，您可以使用脚本`dependencies/dpdk/usertools/dpdk-devbind.py`。例如:

**$ sudo dependencies/dpdk/user tools/dpdk-dev bind . py–bind = uio _ PCI _ generic enp 131s 0 f 0**

这个命令将接口`enp131s0f0`绑定到`uio_pci_generic`驱动程序，这样帧就可以直接传递给 DPDK，而不是内核。请注意，该绑定必须在上述步骤中设置网守后进行，以便绑定的接口出现在`lua/if_map.lua`的接口列表中。

**怎么跑？**

一旦`gatekeeper`被编译并且环境被正确配置，运行:

**$ sudo 构建/看门人[EAL 选项]—[看门人选项]**

其中`[EAL OPTIONS]`在双破折号前指定，代表 DPDK 的[环境抽象层的参数](https://doc.dpdk.org/guides/linux_gsg/linux_eal_parameters.html)和`[GATEKEEPER OPTIONS]`在双破折号后指定，代表[关守特定选项](https://github.com/AltraMayor/gatekeeper/wiki/Configuration#application-configuration)。

系统的早期配置，包括 DPDK 中的设备和内存配置，将被记录到 stdout 中。一旦网关守护设备启动，所有信息都会输出到网关守护设备日志中。

**如何构建包？**

Gatekeeper Debian 包可以用下面的命令构建。它们应该从存储库根运行，并假设已经提取了 git 子模块，并且已经安装了构建依赖项，如上所述。Gatekeeper 和子模块将在包构建过程中自动编译。

**$ tar–排除-vcs -Jcvf../keeper _ 1 . 0 . 0 . orig . tar . xz-C..看门人
$ debuild -uc -us**

Gatekeeper 包将在父目录中提供。