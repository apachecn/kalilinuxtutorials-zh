# OSINT-SPY:对电子邮件/域/IP 地址/组织执行 OSINT 扫描

> 原文：<https://kalilinuxtutorials.com/osint-spy/>

[![OSINT-SPY : Performs OSINT Scan On Email/Domain/IP_Address/Organisation](img/cfbf4ab867227fba427f7713804bbf90.png "OSINT-SPY : Performs OSINT Scan On Email/Domain/IP_Address/Organisation")](https://4.bp.blogspot.com/-2MDdE6dkoiA/XNkCV_ZqU7I/AAAAAAAAAQE/pTCDEmxSGO89wow-OWnCuhoMKVRgd5leQCLcBGAs/s1600/New%2BProject.png)

使用 OSINT-SPY 对电子邮件/域/ip 地址/组织执行 OSINT 扫描。数据挖掘者、信息安全研究人员、渗透测试人员和网络犯罪调查人员可以使用它来找到有关其目标的深层信息。

**该工具概述**

*   对 IP 地址/域/电子邮件地址/ BTC(比特币)地址/设备执行扫描
*   了解最新的比特币区块信息
*   列出所有特定网站和服务器支持的密码
*   检查某个网站是否容易受到心脏出血的攻击？
*   转储 skype 数据库中的所有联系人和消息
*   远程分析恶意软件或恶意文件

**也可阅读-**[**icleak:查找工具&从 CUCM**T5 托管的手机配置文件中提取凭证】](https://kalilinuxtutorials.com/iculeak/)

**许可证信息**

**OSINT-SPY** 及其文档覆盖 GPL-3.0(通用公共许可证 v3.0)。

**使用 OSINT
网站搜索:www.osint-spy.com**

**用法:osint-spy.py【选项】**
选项:
-h，–帮助显示此帮助信息并退出。
–BTC _ block 查找最新比特币区块链信息。
–BTC _ date 查找给定日期的比特币区块链信息。
–BTC _ address 查询给定比特币地址的余额和交易信息。
–SSL _ cipher 列出给定服务器使用的所有密码。
–SSL _ bleed 检查服务器是否易受心脏出血漏洞的攻击。
–域名获取给定网站或组织的详细信息。
–电子邮件收集给定电子邮件地址的信息。
–设备查找连接到互联网的设备。
–ip 从给定的 IP 地址中枚举信息。
–skype _ db 提供 Skype 数据库的位置，以便从中获取所有信息，包括聊天记录和联系人信息。
–恶意软件查明给定文件是否被恶意软件感染。
–载体给出载体文件的路径，在该路径后面要添加文本。
–setgo _ text 输入隐藏在载体文件后面的文本。
–stego _ find 给出一个 stego 文件，它会尝试查找隐藏文本。

**所需设置**

*   Python 2.7
*   使用 install_linux.py(用于在 linux 上安装所有依赖项和库)
*   使用 install_windows.py(用于在 windows 上安装所有依赖项和库)

**贡献者**

**沙拉德·库马尔—@ sk _ security**

**设置环境**

安装和使用 OSINT-SPY 非常容易。安装过程非常简单，只有 4 个步骤。
1。下载或克隆 OSINT-SPY github 库。
2。下载并安装所有依赖项。
3。生成 API 密钥
4。在配置文件

中添加 API 键开始吧！！

第一步——在你的系统上下载 OSINT-PSY。为了安装 OSINT-SPY，只需克隆 github 库。下面是您可以用来克隆 OSINT-SPY 库的命令。
git 克隆 https://github.com/SharadKumar97/OSINT-SPY.git
步骤 2——下载和安装依赖项。
一旦你克隆了 OSINT-SPY，你会发现一个目录名为 OSINT-SPY。只需转到该目录并安装依赖项。如果您在 windows 上使用 OSINT-SPY，则运行 install_linux.py 文件，如果您使用 linux，则运行 install _ Linux . py
python install _ Linux . py
或
python install _ windows . py

**生成 API 密钥**

在使用这个工具之前，我们需要一些 API 键。下面是我们暂时在这个工具中使用的 API。
1。Clearbit API
2。肖丹 API
3。全接触 API
4。病毒 _ 总 API
5。email hunter API

Clearbit API

在 clear bit 注册并激活您的帐户。一旦你登录，你会发现 API 的一个部分。去那里复制你的秘密 API 密匙并粘贴到 config.py 文件中。Config.py 文件可以在 OSINT-SPY 的 modules 目录中找到。

Shodan API

在 Shodan 注册并激活您的帐户。一旦您激活您的帐户，然后登录 Shodan。登录后，您会在概览选项卡中找到一个 API 密钥。复制该键并粘贴到 config.py 文件中。

FullContact API

在 Full Contact 注册自己。你可以用你的邮箱注册，也可以用谷歌注册。登录后，您会在仪表板前面找到您的 API 密钥。只需复制该密钥并将其粘贴到 config.py 文件中。

VirusTotal API

在 virus total 注册。一旦您登录，您将在您的个人资料菜单中找到我的 Api 密钥部分。只需到那里复制您的公共 API 密钥并粘贴到 config.py 文件中。

EmailHunter API

在 Email Hunter 注册自己。登录后，进入 API 选项卡，点击眼睛图标查看您的 API 密钥。将 API 密钥复制到 config.py 文件中。

**用途**

OSINT-SPY 是非常方便的工具，易于使用。你所要做的就是把值传递给参数。为了启动 OSINT-SPY，只需编写—
python osint-spy.com

–BTC _ block

–BTC _ block 参数为您提供最新比特币区块链的信息。

用法:
python osint-spy . py–BTC _ block

–BTC _ date

–BTC _ date 参数会给你一个从给定日期开始的比特币区块链的信息。

用法:
python osint-spy . py–BTC _ date 2017 06 20

–BTC _ address

–BTC _ address 会给你一个关于特定比特币主人的信息。

python osint-spy . py–BTC _ address 1 dst 3g M6 jthxhuonkfqxrdpzppffz 1 wghpw

–SSL _ cipher

–SSL _ cipher 将显示给定网站支持的所有密码。

python osint-spy . py–SSL _ cipher google.com

–SSL _ bleed

–SSL _ bleed 会发现给定网站是否易受 heartbleed 攻击？。

python osint-spy . py–SSL _ bleed google.com

–domain

–domain 将为您提供特定域名的详细信息，包括 whois、dns、密码、位置等等。

python osint-spy . py–域名 google.com

–电子邮件

–电子邮件将从各种公开来源收集有关给定电子邮件地址的信息。

python osint-spy . py–电子邮件 david@toorcon.org

–设备

–设备将从 shodan 搜索给定的设备，并将列出公共 IP 上所有可用的设备。

python osint-spy . py–设备网络摄像头

–ip

–IP 将从公共来源收集给定 IP 地址的所有信息。

python osint-spy . py–IP 127 . 0 . 0 . 1

–skype _ db

–Skype _ db 将从给定的 Skype 数据库中找出所有联系人和消息历史记录。这对法医调查员来说很有用。在 Windows 中，Skype 数据库可以在 AppData\Roaming\Skype\(您的用户名)\main.db 中找到，在 Mac OSX 中，数据库可以在/Users/(您的 Mac 用户 anme)/Library/Support/Skype/(您的 skyoe 用户名)/main . db
/python osint-spy . py–Skype _ db main . db

–恶意软件

–恶意软件将给定文件发送到 virustotal，并给出给定文件是否。

python osint-spy . py–恶意软件 abc.exe

–carrier 和–stego _ text

–carrier 和–stego _ text 用于隐藏任何图像后面的文本。–运营商将指定您想要隐藏文本的图像。–stego _ text 将指定您要添加的文本。

python osint-spy . py–运营商 image.jpg–stego _ text This _ is _ secre _ text

–stego _ find

–stego _ find 会找出任何图片背后隐藏的文字。

python osint-spy . py–stego _ 寻找 hidden.jpg

[**Download**](https://github.com/SharadKumar97/OSINT-SPY)