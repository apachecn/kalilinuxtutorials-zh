# HashCatch:自动捕捉附近 WiFi 网络的握手

> 原文：<https://kalilinuxtutorials.com/handshakes-wifi-networks/>

[![HashCatch : Capture Handshakes Of Nearby WiFi Networks Automatically](img/14546b2762300d8844a91ef416b3f94e.png "HashCatch : Capture Handshakes Of Nearby WiFi Networks Automatically")](https://camo.githubusercontent.com/02596350a47a8677bd01a082058db6e95002b811/68747470733a2f2f61736369696e656d612e6f72672f612f4151457a4c53786f3774656f78507a4e534a66776e34554e512e737667)

**Hashcatch** 解除连接到附近所有 WiFi 网络的客户端的身份验证，并尝试捕捉握手。它可以在任何 Linux 设备上使用，包括 Raspberry Pi 和 Nethunter 设备，这样你就可以在遛狗的时候捕捉握手。

**从源安装**

*   `**git clone https://github.com/staz0t/hashcatch**`
*   安装必备组件并确保它们正常工作
*   [可选]将 hashcatch 目录添加到您的路径中
*   `**./hashcatch --setup**`
*   回答提示
*   第一

**使用软件包安装**

1.  从[版本](https://github.com/aircrack-ng/aircrack-ng/releases)中下载相应的包进行分发
2.  **运行** `**sudo pacman -U ./hashcatch-<ver>-1-any.pkg.tar.xz**` **或** `**sudo apt install ./hashcatch_<ver>_all.deb**`
3.  `**sudo hashcatch --setup**`
4.  回答提示
5.  第一

**先决条件**

*   空气裂化
*   hashcat-utils
*   hcxtools
*   japan quarterly 日本季刊

**也可阅读-[NebulousAD:自动化凭证审计工具](https://kalilinuxtutorials.com/nebulousad-automated-credential-auditing-tool/)**

**用法**

`**sudo hashcatch**`启动哈希卡

`**hashcatch --help**`打印帮助屏幕

*   Hashcatch 无限期运行，直到键盘中断
*   捕获的握手将存储在**/usr/share/hash atch/handshakes/**中
*   捕获的 WiFi 网络的 BSSID 和 ESSID 将被添加到**/usr/share/hash atch/db**
*   如果你的目标是 wifi 网络，花大约 20 到 30 秒在 wifi 的范围内，以确保握手捕捉
*   [实验]如果您在采集时连接到互联网，以下数据也将添加到数据库文件中
    *   纬度
    *   经度
    *   信号半径
    *   记录时间
    *   注意:Alexander Mylnikov 运行的 API 使用公共数据库返回路由器 MAC 地址的详细位置信息，这值得称赞

**配置文件**

*   该配置文件可以在/etc/hashcatch/hashcatch.conf 中找到
*   您可以稍后编辑“接口”字段来设置您选择的接口
*   您还可以添加一个“忽略”字段，以提及您希望 hashcatch 在运行时忽略的 WiFi 网络
*   请参考下面给出的示例，了解应将条目添加到配置文件的格式
*   格式`**option name=option1,option2,option3**`
*   选项名称、等号和选项之间没有空格
*   例子

interface = WLAN 0
ignore = Google Starbucks，AndroidAP

**新增功能**

*   更多位置功能
*   自动上传到网站开始破解握手

**已知问题**

*   [OSX]从用户提出的问题来看，似乎 airodump-ng 在 OSX 不能正常工作。由于它是 hashcatch 的依赖项，OSX 用户可能无法运行 hashcatch。

**注意:** PMKID 攻击不包括在 hashcatch 中，因为并非所有路由器都容易受到攻击，因此检查攻击会增加测试一个 AP 所需的时间。Pixiedust 攻击，并通过 WPS 收集信息虽然在有针对性的攻击中是有效的，但它也增加了测试一个 AP 所花费的时间，这对于该工具的任务来说是不理想的，该工具的任务是尽可能快。此外，在我的测试中，我发现每 10 个接入点就有一个支持 WPS 的路由器。因此，hashcatch 提供的结果将是不一致的，它可能会错过捕捉额外握手的机会。因此，到目前为止，hashcat 将继续使用传统的 deauth 和 capture 方法。

[**Download**](https://github.com/staz0t/hashcatch)