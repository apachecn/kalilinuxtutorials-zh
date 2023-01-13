# 松果:WLAN 红队框架

> 原文：<https://kalilinuxtutorials.com/pinecone-2/>

[![](img/ab4b7c73fb75dadc15a0fb56a129e6a3.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhKiWX7HNYblrmEkxVtGrX18M3A9lpCjOlDVQPs2qyd0FE6DjUF1gY3rMw3VGmUBrAH8JBCJWHS6ZlKEykT705KNcUH-eMWD7ebqo_wXP-m4wDQAB11s6WTO6gK8RlkS2Q9qNgM9jTrIeDaVxkoPt5OEQfi9XciEiQzhCeUWgO260zxZiUNaw7raAwx/s728/logo_full%20(1).png)

**Pinecone** 是一款 WLAN 网络审计工具，适合红队使用。它可以通过模块进行扩展，并且被设计成可以在基于 Debian 的操作系统中运行。松果是专门面向使用树莓皮，作为一个便携式无线审计箱。

该工具仅用于教育和研究目的。仅在明确许可的情况下使用它。

## 安装

要运行松果，你需要一个基于 Debian 的操作系统(已经在 Raspbian、Raspberry Pi 桌面和 Kali Linux 上进行了测试)。松果有以下要求:

*   **Python 3.5+** 。您的发行版可能已经安装了 Python3，如果没有，可以使用`**apt-get install**` **`python3`来安装。**
*   **dnsmasq** (用 2.76 版本测试)。可以使用`**apt-get install dnsmasq**`安装。
*   **hostapd-wpe** (用 2.6 版本测试)。可以使用`apt-get install hostapd-wpe`安装。如果您的发行版存储库没有 hostapd-wpe 包，您可以尝试使用 Kali Linux 存储库预编译包来安装它，或者从它的源代码编译它。

在安装了必要的包之后，您可以使用项目根文件夹中的`**pip3 install -r requirements.txt**`来安装松果的 Python 包需求。

## 用法

为了启动松果，从项目根文件夹中执行`**python3 pinecone.py**`:

**root @ kali:~/pine cone # python pine cone . py
数据库文件:~/pine cone/db/Database . SQLite
pine cone>**

松果通过类似 Metasploit 的命令行界面来控制。您可以键入`**help**`来获得可用命令的列表，或者键入`**help 'command'**`来获得关于特定命令的更多信息:

**松果>帮助
文档化命令(类型帮助):
别名帮助加载 pyscript 设置快捷键使用
编辑历史 py 退出 shell unalias
文档化命令:
反向运行停止
松果>帮助使用
用法:使用模块[-h】
与指定模块交互。
位置参数:
模块模块 ID
可选参数:
-h，–help 显示此帮助信息并退出**

使用命令`**use 'moduleID'**`激活松果模块。您可以使用 Tab 键自动完成来查看当前加载的模块列表:

**松果>使用
攻击/deauth 守护进程/hostapd-wpe 报告/db2json 脚本/基础设施/ap
守护进程/dnsmasq 发现/侦察脚本/攻击/wpa _ 握手
松果>使用发现/侦察
pcn 模块(发现/侦察)>**

每个模块都有选项，当一个模块被激活时，可以通过键入`**help run**`或`**run --help**`看到这些选项。大多数模块的选项都有默认值(运行前检查):

**pcn 模块(discovery/recon) > help run
用法:run [-h] [-i INTERFACE]
可选参数:
-h，–help 显示此帮助消息并退出
-i INTERFACE，–iface INTERFACE
支持监听模式的 WLAN 接口(默认:wlan0)**

当一个模块被激活时，您可以使用`**run [options...]**`命令来启动其功能。模块提供其执行状态的反馈:

**PCN script(attack/wpa _ handshake)>run-s TEST _ SSID
[I]在信道 1 上从 AP 00:11:22:33:44:55 向所有客户端发送 64 个 deauth 帧……
………………………………………………………………………………………………………………………………………………………………………………。
发送了 64 个数据包。
[i]在所有客户端和 AP 之间的信道 1 WPA 握手上监视 10 秒 00:11:22:33:44:55…**

如果模块在后台运行(例如，*脚本/基础设施/ap* )，您可以在模块运行时使用`**stop**`命令停止它:

**PCN script(infra structure/AP)>run
net . IP v4 . IP _ forward = 1
【I】在 iptables 中创建 NAT 规则用于转发 wlan0->eth 0…
【I】启动 hostapd-wpe 和 dnsmasq…
配置文件:~/pinecone/tmp/hostapd-wpe . conf
使用接口 WLAN 0 与 hwaddr 00:11:22:33:44:55 和 SSI**

当您使用完一个模块时，您可以使用`**back**`命令将其停用。您也可以激活另一个模块，再次发出`**use**`命令。

外壳命令可以用命令`**shell**`或快捷键`**!**`执行:

**松果>！ls
许可证模块 module _ template . py pine cone pine cone . py readme . MD requirements . txt todo . MD**

目前，松果侦察 SQLite 数据库存储在项目根文件夹内的 *db/* 目录中。松果需要使用的所有临时文件都存储在项目根文件夹下的 *tmp/* 目录中。

[**Download**](https://github.com/pinecone-wifi/pinecone)