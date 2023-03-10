# Dolos 斗篷:自动 802.1x 旁路

> 原文：<https://kalilinuxtutorials.com/dolos-cloak-automated-802-1x-bypass-network-penetration/>

[![Dolos Cloak : Automated 802.1x Bypass](img/dd4d0c1c4f77b188f63f53a0c7257b1d.png "Dolos Cloak : Automated 802.1x Bypass")](https://1.bp.blogspot.com/-gzX1v6gSX_s/XYZGwYrOFsI/AAAAAAAACko/UMYO70hLPiQtj1zo07WryVgGOH-HsuUwQCLcBGAsYHQ/s1600/802.png)

**Dolos 斗篷**是一个 python 脚本，旨在帮助网络渗透测试人员和 red teamers 通过使用高级中间人攻击来绕过 802.1x 解决方案。

该工具能够利用目标网络上已经允许的受害者设备的有线连接，而不会将受害者设备踢出网络。它被设计为在运行 Kali ARM 的 Odroid C2 上运行，并需要两个外部 USB 以太网加密狗。

这个工具应该可以在其他硬件和发行版上运行，但是到目前为止它只在 Odroid C2 上测试过。

**也可理解为-[PostShell–利用后绑定/反向连接外壳](https://kalilinuxtutorials.com/postshell-post-exploitation-bind-backconnect-shell/)**

**它是如何工作的？**

**Dolos** 斗篷使用 iptables、arptables 和 ebtables NAT 规则来欺骗可信网络设备的 MAC 和 IP 地址，并混入常规网络流量中。

在引导时，该脚本不允许任何出站网络流量离开 Odroid，以便隐藏其网络接口的 MAC 地址。

接下来，该脚本创建一个网桥接口，并将两个外部 USB 以太网加密狗添加到网桥中。所有流量，包括任何 802.1x 身份验证步骤，都在这两个接口之间的网桥上传递。在这种状态下，该设备的作用类似于一个窃听器。

一旦 Odroid 插入可信设备(台式机、IP 电话、打印机等)之间。)和网络，脚本监听网桥接口上的数据包，以确定受害设备的 MAC 地址和 IP。

一旦脚本确定了受害设备的 MAC 地址和 IP 地址，它就会配置 NAT 规则，以使输出和路由后链上的所有流量看起来像是来自受害设备。此时，设备能够与网络通信，而不会被烧毁。

一旦 Odroid 欺骗了受害设备的 MAC 地址和 IP 地址，脚本就会发出 DHCP 请求，以确定其默认网关、搜索域和名称服务器。它使用响应来配置其网络设置，以便设备可以与网络的其余部分通信。

在这一点上，Odroid 在网络上扮演了一个隐秘的角色。运营商可以通过内置网卡 eth0 连接到 Odroid，以获得网络访问权限。

该设备还可以配置为发送反向外壳，以便操作员可以将该设备用作投件箱，并在网络上远程运行命令。例如，可以将脚本配置为在运行中间人攻击后运行 Empire python stager。

然后，您可以使用帝国 C2 连接升级到 TCP 反向外壳或 VPN 隧道。

**安装&使用**

*   在 Odroid C2 上执行 Kali ARM 的默认安装。点击查看布莱克希尔斯的报道[。](https://www.blackhillsinfosec.com/how-to-build-your-own-penetration-testing-drop-box/)

ssh root@169.254.44.44

*   请务必将此项目保存到/root/tools/dolos _ coat
*   将一个外部 USB 网卡插入 Odroid 并运行 dhclient 以访问互联网，从而安装依赖项:

dhclient usbnet0

*   运行安装脚本以获取所有依赖项，并设置 Odroid 在默认情况下在引导时执行 MitM。请记住，这将对设备的网络设置做出重大更改，并禁用网络管理器。在此步骤之前，您可能需要下载任何其他工具:

cd 设置
。/setup.sh

*   你可能需要安装一些 Kali ARM 上没有的其他工具，比如“主机”。Empire、enum4linux 和 responder 也是不错的补充。
*   确保您能够通过内置 NIC eth 0 ssh 到 Odroid。将您的公钥添加到/root/。ssh/authorized_keys 用于快速访问。
*   修改 config.yaml 以满足您的需要。你应该确保接口匹配你的 Odroid 给你的 USB 加密狗的默认名称。顺序在这里并不重要。您应该将 client_ip、client_mac、gateway_ip 和 gateway_mac 留空，除非您使用 LAN tap 来挖掘它们。脚本*应该*能够为我们解决这个问题。仅当您确实知道这些选项的值时，才设置它们。management_int、domain_name 和 dns_server 选项目前只是占位符，但很快就会派上用场。对于 shells，您可以在 config.yaml 中设置一个自定义的 autorun 命令，在中间人攻击自动配置完成时运行。您还可以设置一个 cron 作业来发送回 shells。
*   连接两个 usb 以太网加密狗并重启设备(你需要两个，因为内置的以太网不支持混杂模式)
*   启动设备，等待几秒钟，让 autosniff.py 阻塞输出以太网和 IP 链。然后在可信设备和网络之间插入 Odroid。
*   PWN N00BZ，获得$$$，玩得开心，黑地球

**提示**

*   修改后运行。/scripts/upgrade_to_vpn.sh 将一个隐秘的帝国代理变成一个成熟的 vpn 隧道
*   修改后运行。/scripts/reverse _ listener _ setup . sh 为设备上的反向侦听器设置端口。
*   快跑。/scripts/responder_setup.sh 允许控制我们为 responder 捕获的协议。您应该在网桥接口上运行 responder:

响应者-I mibr

*   请小心，因为有些 NAC 解决方案使用端口 445、443 和 80 来定期验证主机。正在努力解决这个问题…
*   当 autosniff.py 行为不当时，日志会有所帮助。rc.local 设置为存储当前会话日志。/logs/session.log 并登录。/logs/history.log，这样我们可以重新启动，并在需要时检查最后一个会话的日志。日志文件中有很酷的东西，比如网络信息、错误消息和所有设置 NAT ninja 魔法的 bash 命令。

[**Download**](https://github.com/fkasler/dolos_cloak)