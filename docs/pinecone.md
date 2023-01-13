# 松果:WLAN 红队框架

> 原文：<https://kalilinuxtutorials.com/pinecone/>

[![](img/c7daaab0236c05a0ecbd72de8aa7e6d4.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiQasQvhtij2lEJNYYRyKYULfEv2izy3-YuXwfo51oUVuEX8WHa_MT6v4CbG98qUqalOBIGJMW6GQYIJX2G11RRSU0naIRzHP5ZPz1IRLIhcJFHLRx0ijJETJhOuVwEsXw_emM3NhID6Eq7SueeRoml6ehpiuj_H2qwo4I3vcXLQS0-mDIuMnRkaA6q/s728/logo_full%20(2).png)

**Pinecone** 是一款 WLAN 网络审计工具，适合红队使用。它可以通过模块进行扩展，并且被设计成可以在基于 Debian 的操作系统中运行。松果是专门面向使用树莓皮，作为一个便携式无线审计箱。

该工具仅用于教育和研究目的。仅在明确许可的情况下使用它。

## 安装

要运行松果，你需要一个基于 Debian 的操作系统(已经在 Raspbian、Raspberry Pi 桌面和 Kali Linux 上进行了测试)。松果有以下要求:

*   **Python 3.5+** 。您的发行版可能已经安装了 Python3，如果没有，可以使用`**apt-get install python3**`安装。
*   **dnsmasq** (用 2.76 版本测试)。可以使用**安装`apt-get install dnsmasq`。**
*   **hostapd-wpe** (用 2.6 版本测试)。可以使用**安装`apt-get install hostapd-wpe`。**如果您的发行版存储库没有 hostapd-wpe 包，您可以尝试使用 Kali Linux 存储库预编译包来安装它，或者从它的源代码编译它。

在安装了必要的包之后，您可以使用项目根文件夹中的`**pip3 install -r requirements.txt**`来安装松果的 Python 包需求。

## 用法

为了启动松果，从项目根文件夹中执行`**python3 pinecone.py**`:

**root @ kali:~/pine cone # python pine cone . py
数据库文件:~/pine cone/db/Database . SQLite
pine cone>**

松果通过类似 Metasploit 的命令行界面来控制。您可以键入`**help**`来获得可用命令的列表，或者键入`**help** **'command'**`来获得关于特定命令的更多信息:

**松果>帮助
文档化命令(类型帮助):
别名帮助加载 pyscript 设置快捷键使用
编辑历史 py 退出 shell unalias
文档化命令:
反向运行停止
松果>帮助使用
用法:使用模块[-h】
与指定模块交互。
位置参数:模块模块 ID
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
[I]在通道 1 上从 AP 00:11:22:33:44:55 向所有客户端发送 64 个 deauth 帧…
发送 64 个数据包。
[i]在所有客户端和 AP 之间的信道 1 WPA 握手上监视 10 秒 00:11:22:33:44:55……**

[Download](https://github.com/pinecone-wifi/pinecone)