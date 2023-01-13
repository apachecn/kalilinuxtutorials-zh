# Tyton:内核模式 Rootkit 猎人

> 原文：<https://kalilinuxtutorials.com/tyton-kernel-rootkit-hunter/>

Tyton Linux 内核模式 Rootkit Hunter for 4.4.0-31+。

#### **检测到的攻击**

*   隐藏模块
*   系统调用表挂钩
*   网络协议挂钩
*   Netfilter 挂钩
*   归零的进程信息节点
*   处理比赛场地预订
*   中断描述符表挂钩

**也可阅读:**[Hatch——暴力破解工具，用于暴力破解大多数网站](https://kalilinuxtutorials.com/hatch-brute-force-tool/)

#### **附加功能**

**通知**:用户(包括我自己)并不主动监控他们的日志，所以包含了一个用户通知守护进程来监控日志并使用 libnotify 向用户显示。通知是由 XDG 自动运行安装后启用的，所以如果你的 DM 没有`/etc/xdg/autostart`它将失败。

DKMS:为 Arch 和 Fedora/CentOS 增加了动态内核模块支持(希望在不久的将来扩展)。DKMS 允许内核升级期间内核模块的(近乎)无缝升级。这对于提供滚动发布或者频繁升级内核的发行版来说非常重要。

#### **泰顿安装**

来自源

**Ubuntu/Debian/Kali**

**sudo apt 安装 Linux-headers-$(uname-r)gcc make lib notify-dev pkg-config libgtk-3-dev libsystemd-dev
git 克隆 https://github.com/nbulischeck/tyton.git
CD tyton
make
sudo insmod tyton . ko**

**注:**对于 Ubuntu 14.04，libsystemd-dev 命名为 libsystemd-journal-dev。

**拱门**

**sudo pacman-S Linux-headers gcc make libnotify libsystemd pkgconfig GTK 3
git 克隆 https://github.com/nbulischeck/tyton.git
CD tyton
make
sudo insmod tyton . ko**

**注意:**建议通过 AUR 安装，这样你就可以从 DKMS 中获益。

**Fedora/CentOS**

**dnf 安装 kernel-devel gcc make libnotify libnotify-devel systemd-devel GTK 3-devel GTK 3
git 克隆 https://github.com/nbulischeck/tyton.git
CD tyton
make
sudo insmod tyton . ko**

**内核模块参数**

内核模块可以通过命令行在插入时传递一个特定的超时参数。

为此，运行命令 sudo insmod tyton.ko timeout=X，其中 X 是您希望内核模块在再次执行扫描之前等待的分钟数。

**AUR**

在 AUR [这里](https://aur.archlinux.org/packages/tyton-dkms-git/)可以买到。

您可以使用您选择的 AUR 助手来安装它:

**酸奶-s tyton-dkms-git
yay-s tyton-dkms-git
pak ku-s tyton-dkms-git**

[**Download**](https://github.com/nbulischeck/tyton)