# wslu:Windows 10 Linux 子系统的实用程序集合

> 原文：<https://kalilinuxtutorials.com/wslu/>

[![](img/0ef42d58ddfd240a7fbfc8fe4989a45a.png)](https://blogger.googleusercontent.com/img/a/AVvXsEjiyKVG3x0HVwerrrkaFy3TXTK9MyT6wIDPP2SbDhPQ_5n9FA9rsMpVRtqI4S4dlOmBSW0prh4lbnwBwa4WMZh1ECdhH2FGvP3qwzXFFo6QbJ4AMIbn9uxUT6kJX_7PXkN-VPJmskiPiGqT3XFgnEWjPX5lSx4mEmCcqmhtrz03u2sojWZCTl0Wkpc-=s728)

**Wslu** 是 Windows 10 Linux 子系统的实用程序集合，比如检索 Windows 10 环境变量，或者在 Windows 10 桌面上创建自己喜欢的 Linux GUI 应用快捷方式。

需要 Windows 10 Creators 更新；部分功能需要更高版本的 Windows 10 支持 WSL2。

## 功能

**wslusc**

一个 WSL 快捷方式创建器，用于在 Windows 10 桌面上创建快捷方式。

**wslsys**

WSL 系统信息打印机，用于打印 Windows 10 或 WSL 的系统信息。

**wslfetch**

一个 WSL 截屏信息工具，以优雅的方式打印信息。

**wslvar**

一个 WSL 工具，帮助你获得 Windows 系统环境变量。

**wsl 视图**

*同别名`**wview/wslstart/wstart**`*

一个假的 WSL 浏览器，可以帮助你在默认的 Windows 浏览器中打开链接或在 Windows 上打开文件。

wslupath

*已弃用*

一个转换路径样式的 WSL 工具。

wslact

WSL 的一组快速操作，如快速安装所有驱动器或手动同步 Windows 和 WSL 之间的时间。

## 安装

### 阿尔卑斯 Linux

您可以使用以下命令在 **Alpine Linux 3.12+** 上安装`**wslu**`:

**sudo apk 添加 wslu**

### Arch Linux

AUR 版本的`**wslu**`因违反其政策而被撤下。

从 release 下载最新的软件包，并使用命令:`**sudo pacman -U *.zst**`进行安装

### CentOS/RHEL/甲骨文 Linux

为相应的 Linux 发行版添加存储库:

**第 7 分钟**

**sudo yum-config-manager–add-repo https://download . opensuse . org/repositories/home:/wsl utilities/CentOS _ 7/home:wsl utilities . repo**

**厘斯 8**

**sudo dnf install-y epel-release
sudo dnf config-manager–set-enabled power tools
sudo yum-config-manager–add-repo https://download . opensuse . org/repositories/home:/wsl utilities/CentOS _ 8/home:wsl utilities。**回购

**甲骨文 Linux 8**

**sudo dnf install-y https://dl . fedora project . org/pub/epel/epel-release-latest-8 . no arch . rpm
sudo subscription-manager repos–enable code ready-builder-for-rhel-8-$(/bin/arch)-rpms
sudo yum-config-manager–add-repo https://download . opensuse . org/repositories/home:/wsl utilities/CentOS _ 8/home:wsl utilities . repo【T3**

### 一种自由操作系统

您可以使用以下命令安装`**wslu**`:

**sudo apt install GnuPG 2 apt-transport-https
wget-o–https://pkg . wslutiliti . es/public . key | sudo tee-a/etc/apt/trusted . gpg . d/wslu . ASC
echo】deb https://pkg . wslutiliti . es/debian buster main | sudo tee-a/etc/apt/sources . list
sudo apt update**

**软呢帽**

**sudo dnf copr 启用 wslulities/wslu
sudo dnf 安装 wslu**

### Kali Linux

您可以使用以下命令安装`**wslu**`:

**sudo apt install GnuPG 2 apt-transport-https
wget-o–https://pkg . wslutiliti . es/public . key | sudo tee-a/etc/apt/trusted . gpg . d/wslu . ASC
echo】deb https://pkg . wslutiliti . es/kali-rolling main | sudo tee-a/etc/apt/sources . list
sudo apt**

### 人的本质

立正！

对于 Ubuntu 版本，你不仅应该在这里报告错误，还应该在 Launchpad 报告错误。

预装在最新的应用中。在旧版本的 Ubuntu 上，请安装依赖于`**wslu**`的`**ubuntu-wsl**`:

**sudo 更新
sudo 安装 ubuntu-wsl**

### suse linux 企业服务器

您可以使用以下命令安装`**wslu**`:

**SLES cur _ VERSION = " $(grep VERSION =/etc/OS-release | sed-e s/VERSION =//g-e s/\ "//g-e s/-/*/g)" sudo zypper addrepo https://download . opensuse . org/repositories/home:/wsl utilities/SLE*$ SLES cur _ VERSION/home:wsl utilities . repo
sudo zypper addrepo https://download . opensuse . org/repositorities/graphics/SLE**

[**Download**](https://github.com/wslutilities/wslu)