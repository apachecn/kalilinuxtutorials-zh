# HostHunter:使用 OSINT 发现主机名

> 原文：<https://kalilinuxtutorials.com/hosthunter-hostnames-osint/>

HostHunter 是一个使用 OSINT 技术发现主机名的侦察工具。

HostHunter v1.5 是一个工具，可以有效地发现和提取大量目标 IP 地址中的主机名。它利用简单的 OSINT 技术。它生成一个包含侦察结果的 CSV 文件。

截图也是作为测试版功能加入的。

**演示**

目前 GitLab 的标记语言不支持 HTML 或 CSS 对图像的控制，因此下面的链接缩略图很大。

也可阅读: [KDE 应用程序 19.04 版本](https://kalilinuxtutorials.com/kde-applications-19-04-release/)

**安装**

用 Python 3.7.2 测试。

**Linux**

使用 wget 命令下载最新的 Google Chrome debian 包。

$ wget https://dl . Google . com/Linux/direct/Google-chrome-stable _ current _ amd64 . deb

$ dpkg-I ./Google-chrome-stable _ current _ amd64 . deb

$ sudo apt-get install-f

安装 python 依赖项。

$ pip 安装-r 要求. txt

**简单用法举例:**

$ python 3 host hunter . py <targets.txt>$ cat vhosts . CSV</targets.txt>

更多示例

**HostHunter 帮助页面**

**$ python3 hosthunter.py -h
用法:host hunter . py[-h][-V][-f FORMAT][-o OUTPUT][-b][-sc]targets
|<—host hunter V 1.5-帮助页面— > |
位置参数:
targets 设置目标 IPs 文件的路径。
可选参数:
-h，–help 显示此帮助信息并退出
-V，–version 显示当前版本。
-f 格式，–FORMAT FORMAT
在 CSV 和 TXT 输出文件格式之间选择。
-o 输出，–输出输出
设置输出文件的路径。
-b，–bing 使用 Bing.com 搜索引擎发现更多与目标 IP 地址相关的主机名
。
-sc，–截屏
捕捉任何相关 Web
应用的截屏。**

**在启用 Bing 和屏幕捕获模块的情况下运行 HostHunter】**

**$ python 3 host hunter . py–bing-sc-f CSV-o hosts . CSV**

**显示结果**

**$ cat hosts.csv**

**查看截图**

**$打开。/screen_captures/**

**特性**

*   使用 Python3
*   废料 Bing.com 结果
*   支持。txt 和。csv 输出文件格式
*   验证目标 IPv4 地址
*   拍摄目标的屏幕截图
*   从 SSL 证书中提取主机名
*   利用黑客目标 API

演职员表:安德烈亚斯·乔治乌

[Download](https://github.com/SpiderLabs/HostHunter)