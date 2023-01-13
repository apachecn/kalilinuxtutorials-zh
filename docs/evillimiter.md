# Evillimiter:在没有接入的情况下限制同一网络上设备带宽的工具

> 原文：<https://kalilinuxtutorials.com/evillimiter/>

Evillimiter 是一个工具，用于限制连接到您网络的设备的带宽(上传/下载),无需物理或管理访问。

它采用 ARP 欺骗和流量整形来限制网络上主机的带宽。这将在下面详细解释。

**要求**

*   Linux 发行版
*   Python 3 或更高版本

可能缺失的 python 包将在安装过程中安装。

**也可阅读-[IDArling:IDA Pro 的协同逆向工程插件&Hex-Ray](https://kalilinuxtutorials.com/idarling-reverse-engineering-plugin/)**

**安装**

**git 克隆 https://github . com/bitbrute/evillingtor . git
CD evilvilmider
sudo python 3 setup . py install**

**用途**

键入`**evillimiter**`或`**python3 bin/evillimiter**`运行工具。

`**evillimiter**`将尝试自动解析所需信息(网络接口、网络掩码、网关地址等)。

**命令行参数**

| 争吵 | 说明 |
| --- | --- |
| `-h` | 显示列出所有命令行参数的帮助消息 |
| `-i [Interface Name]` | 指定网络接口(如果未指定，则解析) |
| `-g [Gateway Address]` | 指定网关 IP 地址(如果未指定，则解析) |
| `-n [Netmask Address]` | 指定网络掩码(如果未指定，则解析) |
| `-f` | 刷新当前 iptables 和 tc 配置。确保数据包得到正确处理。 |
| `--colorless` | 禁用彩色输出 |

`**evillimiter**` **命令**

| 命令 | 说明 |
| --- | --- |
| `scan` | 扫描网络中的在线主机。开始后要做的第一件事。 |
| `hosts` | 显示先前扫描的所有主机/设备和基本信息。显示交互所需的每个主机的 ID。 |
| `limit [ID1,ID2,...] [Rate]` | 限制与指定 ID 关联的主机的带宽。速率决定网速。
有效费率:`bit`、`kbit`、`mbit`、`gbit`、`tbit`、
例如:`limit 4,5,6 200kbit`或`limit all 1gbit` |
| `block [ID1,ID2,...]` | 阻止与指定 ID 关联的主机的 internet 连接。 |
| `free [ID1,ID2,...]` | 取消限制/取消阻止与指定 ID 关联的主机。取消所有进一步的限制。 |
| `add [IP] (--mac [MAC])` | 将自定义主机添加到主机列表。MAC 地址将自动解析，也可以手动指定。
比如:`add 192.168.178.24`或者`add 192.168.1.50 --mac 1c:fc:bc:2d:a6:37` |
| `clear` | 清除终端窗口。 |
| `?`，`help` | 显示与此类似的命令信息。 |

**限制**

*   **仅限制 IPv4 连接**，因为 [ARP 欺骗](https://en.wikipedia.org/wiki/ARP_spoofing)需要仅出现在 IPv4 网络上的 ARP 数据包。

**免责声明**

[邪恶限制器](https://github.com/bitbrute/evillimiter)由 [bitbrute](https://github.com/bitbrute) “原样”提供，“带所有故障”。对于本软件的安全性、适用性、无病毒、不准确性、印刷错误或其他有害组件，提供商不做任何形式的陈述或担保。任何软件的使用都存在固有的危险，您要独自负责确定 Evil Limiter 是否与您的设备和设备上安装的其他软件兼容。您还全权负责保护您的设备和备份您的数据，并且提供商对您可能因使用、修改或分发本软件而遭受的任何损害不承担任何责任。

[**Download**](https://github.com/bitbrute/evillimiter)