# KRF:一个 Kernelspace 的随机断层

> 原文：<https://kalilinuxtutorials.com/krf-kernelspace-randomized-faulter/>

[![KRF : A Kernelspace Randomized Faulter](img/113b62f7692c5ca6f0cecfe56d1f24f5.png "KRF : A Kernelspace Randomized Faulter")](https://1.bp.blogspot.com/-CkPQjVCarUs/XUwEMv5zeqI/AAAAAAAABxU/-ub3SZc4atQOn7aEHq-ukgfedAuNvAq_QCLcBGAs/s1600/Image.png)

KRF 是一个欧洲太空英雄、T2 英雄和 T4 英雄。它目前支持 Linux 和 FreeBSD 内核。

故障注入是一种软件测试技术，包括在程序调用的函数中引发故障(“故障”)。如果被调用方未能执行正确的错误检查和处理，这些错误会导致不可靠的应用程序行为或可利用的漏洞。

与许多用户空间故障注入系统不同，KRF 通过一个加载的模块在内核空间运行。这有几个优点:

*   它在静态二进制上工作，因为它不依赖于`LD_PRELOAD`进行注入。
*   因为它拦截原始的系统调用，而不是它们的 libc 包装器，所以它可以将错误注入到由`syscall(3)`或内联汇编发出的调用中。
*   这可能比使用`dlsym`更快，更不容易出错。

还有几个缺点:

*   您可能需要自己构建它。
*   它可能只在 x86(_64)上工作，因为它手动旋转`cr0`。在 Linux 中，可能有一种与架构无关的方法可以做到这一点。
*   它本质上是一个 rootkit。您绝对不应该在非测试系统上运行它。
*   它可能没有涵盖 Linux 内核对系统调用的所有期望，并且可能会以怪异和难以再现的方式破坏其主机的稳定性。

**又读-[xs pear:power full XSS 扫描&参数分析](https://kalilinuxtutorials.com/xspear-powerfull-xss-scanning-parameter-analysis/)**

它是如何工作的？

KRF 重写了 Linux 或 FreeBSD 系统调用表:当通过`**krfctl**`配置时，KRF 用瘦包装器替换了错误的系统调用。

然后，每个包装器使用可配置的目标系统执行检查，以查看该调用是否应该出错，该目标系统能够将特定的`**personality(2)**`、PID、UID 和/或 GID 作为目标。如果进程**不应该**出错，那么调用原来的系统调用。

最后，目标调用通过随机失败函数出错。例如，`**read(2)**`呼叫可能接收到`**EBADF**` **、** `**EINTR**`、**、** `**EIO**`等等中的一个。

**设置**

**兼容性**

**注意**:如果你有流浪者，只需使用流浪者文件并跳转到构建步骤。

KRF 应该可以在任何带有`**CONFIG_KALLSYMS=1**`的最新(4.15 以上)Linux 内核上工作。

这包括 Ubuntu 18.04 上的默认内核，也可能包括许多其他最近的发行版。

**依赖关系**

**注意**:如果你正在使用流浪者，忽略这个。

除了 C 工具链(GCC 可能是 Linux 所必需的)，KRF 唯一的依赖应该是`**libelf**`、内核头文件和 Ruby(用于代码生成)。

所有平台都需要 GNU MakeFreeBSD *另外*需要 BSD Make。

对于带有`**apt**`的系统:

sudo apt 安装 libelf-dev ruby Linux-headers-$(uname-r)

**大楼**

**git 克隆 https://github.com/trailofbits/krf&&CD krf
make-j $(nproc)**

或者，如果您使用的是流浪者:

**git 克隆 https://github.com/trailofbits/krf&&CD krf
游民 up linux & &游民 ssh Linux
# VM 内部
CD/游民
make -j$(nproc)**

或者，对于 FreeBSD:

**git 克隆 https://github.com/trailofbits/krf&&
CD krf CD 游民 up freebsd & &游民 ssh FreeBSD
# VM 内部
CD/游民
gmake #不要闹！**

**用途**

KRF 有三个组成部分:

*   内核模块(`**krfx**`)
*   一个执行实用程序(`**krfexec**`)
*   一个控制实用程序(`**krfctl**`)

要加载内核模块，运行`**make insmod**`。要卸载它，运行`**make rmmod**` **。**

KRF 以中立状态开始:在用户通过`**krfctl**`指定一些行为之前，任何系统调用都不会被拦截或出错:

**#没有诱发故障，即使有 KRF 加载**
ls

#告诉 krf 要故障读(2)和写(2)调用
#注意 krfctl 需要 root 权限
sudo。/src/krfctl/krfctl -F 'read，write '

**#告诉 krf 对任何一个
#personality 为 28(krfexec 设置的值)**
sudo 的程序进行故障诊断。/src/krf CTL/krf CTL-T personal = 28

**#可能故障！**
。/src/krfexec/krfexec ls

**# krfexec 也会正确传递选项**
。/src/krfexec/krfexec echo-n ' no newline '

**#清除故障规范**
sudo。/src/krf CTL/krf CTL-c

**#清除目标规范**
sudo。/src/krf CTL/krf CTL-C

**#没有诱发故障，因为没有系统调用出现故障**
。/src/krfexec/krfexec firefox

在 FreeBSD 上，`**krfexec**` 需要 root 权限。默认情况下，在执行目标之前，它会尝试使用`**SUDO_UID**`和`**getlogin_r**`返回的用户名返回给非根用户。要强制一个特定的 UID，导出`**REAL_UID**` **，**例如:

**REAL_UID=1000 sudo。/src/krfexec/krfexec ls**

**配置**

**注意**:大部分用户应该使用`**krfctl**` 而不是手动操作这些文件。在 FreeBSD 中，这些相同的值可以通过`**sysctl krf.whatever**`而不是 procfs 来访问。

`**/proc/krf/rng_state**`

该文件允许用户读取和修改 KRF PRNG 的内部状态。

例如，以下每一项都会正确地更新状态:

**echo " 1234 " | sudo tee/proc/krf/RNG _ state
echo " 0777 " | sudo tee/proc/krf/RNG _ state
echo " 0x ff " | sudo tee/proc/krf/RNG _ state**

状态是 32 位无符号整数；试图改变它将会失败。

`**/proc/krf/targeting**`

该文件允许用户设置 KRF 用于系统调用定位的值。

**注意** : KRF 使用了一个默认的个性，默认情况下 Linux 内核目前没有使用这个个性。如果你改变这一点，你应该小心避免使它成为 Linux 关心的东西。`**man 2 personality**`有细节。

**echo " 0 28 " | sudo tee/proc/krf/targeting**

28 岁的个性被硬编码进`**krfexec**`。

`**/proc/krf/probability**`

该文件允许用户读取和写入给定(可出错的)系统调用引发故障的概率。

概率表示为倒数，例如，`**1000**` 表示平均而言，`**0.1%**`个可出错的系统调用将出错。

**echo " 100000 " | sudo tee/proc/krf/probability**

`**/proc/krf/control**`

这个文件控制 KRF 出错的系统调用。

**注意**:大多数用户应该使用`**krfctl**` 而不是直接与该文件交互——前者会自动执行 syscall 名称到号码的转换，并在出错时提供更清晰的错误信息。

**#将插槽 0 中的 syscall(通常为 SYS_read)替换为其错误的包装回显“0”| sudo tee/proc/krf/control**

传递任何大于`**KRF_NR_SYSCALLS**`的数字都会导致 KRF 刷新整个 syscall 表，将其返回到中立状态。由于对于任意版本的 Linux 内核来说`**KRF_NR_SYSCALLS**`不一定是可预测的，所以选择一个大的数字(比如 65535)就可以了。

传递一个缺少故障注入包装器的有效系统调用号将导致文件的`**write(2)**`失败，返回`**EOPNOTSUPP**`。

`**/proc/krf/log_faults**`

这个文件控制 KRF 是否在错误的系统调用时发出内核日志。默认情况下，不会发出任何日志消息。

**注意**:大部分用户应该使用`**krfctl**` 而不是直接与这个文件交互。

**#启用故障记录**
echo " 1 " | sudo tee/proc/krf/log _ faults
**#禁用故障记录**
echo " 0 " | sudo tee/proc/krf/log _ faults
**#读取记录状态**
cat/proc/krf/log _ faults

[**Download**](https://github.com/trailofbits/krf)