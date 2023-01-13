# Flightsim:生成恶意网络流量和评估控制的实用程序

> 原文：<https://kalilinuxtutorials.com/flightsim-malicious-network-traffic/>

**Flightsim** 是一个轻量级实用程序，用于生成恶意网络流量，并帮助安全团队评估安全控制和网络可见性。

该工具执行测试以模拟 DNS 隧道、DGA 流量、对已知活动 C2 目的地的请求以及其他可疑流量模式。

**安装**

从 [GitHub 发布版](https://github.com/alphasoc/flightsim/releases)页面为您的操作系统下载最新的 flightsim 二进制文件。或者，可以在任何环境(例如 Linux、MacOS、Windows)中使用 [Golang](https://golang.org/doc/install) 构建该实用程序，如下所示:

**也可阅读-[wps can:为安全专业人士编写的 WordPress 漏洞扫描器](https://kalilinuxtutorials.com/wpscan-wordpress-vulnerability-scanner/)**

**去 github.com/alphasoc/flightsim/…吧**

**运行网络飞行模拟器**

安装后，按如下方式测试 flightsim:

**$ Flight sim–help

alpha SOC Network Flight Simulator(https://github.com/alphasoc/flightsim)

Flight sim 是一款为安全团队生成恶意网络流量的应用程序，用于评估安全控制措施(如防火墙)并确保监控工具能够检测恶意流量。

用法:
flightsim [command]
可用命令:
帮助关于任何命令的帮助
运行运行所有模拟器(默认)或特定测试
版本打印版本并退出
标志:
-h，–flightsim 的帮助
使用“flightsim[command]–Help”了解关于命令的更多信息**

该实用程序运行单个模块来生成恶意流量。要执行所有可用的测试，只需使用 **flightsim run** ，它将使用第一个可用的非环回网络接口生成流量。注意:当运行 C2 模块时，flightsim 将从网络犯罪追踪器和 AlphaSOC API 收集当前 C2 地址，因此需要外出互联网访问。

要列出可用模块，请使用**flightsim run–help**。要执行特定的测试，请使用 flightsim run，如下所示。

**$ flightsim Run–help
运行所有模拟器(默认)或某个特定测试
用法:
flightsim Run【C2-DNS | C2-IP | DGA |劫持|扫描| sink | spambot |隧道】【标志】
标志:
-n，为每个模拟器生成的主机数量(默认 10)
–快速运行模拟器快速无睡眠间隔
-h，–help 帮助运行
-i、 –要使用的接口字符串网络接口
$ Flight sim run DGA
alpha SOC 网络飞行模拟器(https://github.com/alphasoc/flightsim)
网口 IP 地址为 172.31.84.103
当前时间为 10-Jan-18 09:30:28
时间模块描述
————————————————————————————————**
09:30:28 DGA 开始
09:30:28 DGA DGA 生成列表 pbuzkkk.top
09:30:35 dga 解析 wfoheoz.xyz
09:30:35 dga 解析 wfoheoz.biz
09:30:36 dga 解析 wfoheoz.top
09:30:36 dga 解析 lhecftf.xyz
09:30:37 dga 解析 lhecftf.biz
09:30:37 dga

全部完成！使用上面的时间戳和详细信息检查 SIEM 中的警报。

**模块描述**

下表列出了该实用程序附带的模块。

| 组件 | 描述 |
| --- | --- |
| `c2-dns` | 生成当前 C2 目的地的列表，并对每个目的地执行 DNS 请求 |
| `c2-ip` | 连接到 10 个随机的当前 C2 IP:端口对，以模拟出口会话 |
| `dga` | 使用随机标签和顶级域模拟 DGA 流量 |
| `hijack` | 通过 ns1.sandbox.alphasoc.xyz 测试 DNS 劫持支持 |
| `scan` | 使用公共端口对 10 个随机 RFC 1918 地址执行端口扫描 |
| `sink` | 连接到 10 个由安全提供商运营的随机下沉目的地 |
| `spambot` | 解析并连接到随机的互联网 SMTP 服务器来模拟垃圾邮件机器人 |
| `tunnel` | 向*.sandbox.alphasoc.xyz 生成 DNS 隧道请求 |

[**Download**](https://github.com/alphasoc/flightsim)