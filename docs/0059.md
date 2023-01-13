# auto vpn–连接到您选择的国家的 VPN

> 原文：<https://kalilinuxtutorials.com/autovpn-connect-vpn/>

AutoVpn 是一种工具，可以自动将您连接到您选择的国家中的随机 Vpn。它使用 openvpn 将你连接到从 [VPN Gate](http://www.vpngate.net/en/) 获得的服务器。

## **编译 Autovpn**

首先将 repo 和`cd`克隆到目录中:

```
$ git clone https://github.com/adtac/autovpn
$ cd autovpn
```

然后运行以下命令来生成可执行文件:

```
$ go build autovpn.go
```

**也可理解为[burp county——主动和被动扫描检查生成器](http://kalilinuxtutorials.com/burpbounty-active-passive-scan/)**

## **要求**

这需要。`openvpn`要在基于`yum`的发行版上安装它:

```
$ sudo dnf install openvpn
```

如果你在基于`apt`的发行版上:

```
$ sudo apt-get install openvpn
```

在 Fedora 23 上测试和工作。不知道窗户。欢迎补丁。

## **用法**

只需运行:

```
$ ./autovpn
```

你就完了。你将被连接到美国的服务器上。欢迎来到美国！

如果你愿意，你可以给一个国家。例如，如果您想要连接到日本的服务器:

```
$ ./autovpn JP
```

您可能需要超级用户权限。别担心，我没有在下面跑。是为了。`openvpn`

### **牌照**

auto vpn–您选择的国家中的简单自动 VPN 版权所有(C) 2017 Adhityaa Chandrasekar 本程序是自由软件:您可以根据自由软件基金会发布的 GNU 通用公共许可证的条款重新发布和/或修改它，可以是许可证的第 3 版，也可以是(由您选择)任何更高版本。分发这个程序是希望它有用，但没有任何保证；甚至没有对适销性或特定用途适用性的暗示担保。更多细节请参见 GNU 通用公共许可证。您应该已经收到了 GNU 通用公共许可证的副本以及这个程序。

### [![](img/a51de913dc60eee505c4a68651ee8e4d.png)](https://github.com/adtac/autovpn)