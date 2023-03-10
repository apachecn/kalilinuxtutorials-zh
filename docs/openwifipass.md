# OpenWifiPass:苹果 Wi-Fi 密码的开源实现

> 原文：<https://kalilinuxtutorials.com/openwifipass/>

[![OpenWifiPass : An Open Source Implementation Of Apple’s Wi-Fi Password](img/30d4ca1325656117f5baef08e968e561.png "OpenWifiPass : An Open Source Implementation Of Apple’s Wi-Fi Password")](https://1.bp.blogspot.com/-TwAlqwnwNrM/YD6NIcJ9EQI/AAAAAAAAIa0/mKuF-bI9HYsKBBM1pU-T764jY_gAjI1-QCLcBGAsYHQ/s728/wifi%25281%2529.png)

**OpenWifiPass** 苹果 Wi-Fi 密码共享协议中授权者角色的开源实现。

**要求**

*   **硬件:**蓝牙低能耗无线电，如树莓 Pi 4
*   **OS:** Linux(由于`bluepy`的依赖性)

**安装**

克隆此存储库并安装它:

git 克隆 git @ github . com/seewoo-lab/openwifipass . git
pip 3 安装。/openwifipass

**运行**

运行`**openwifipass**`与*任何*请求者共享 Wi-Fi 凭证(**`SSID`**`**PSK**`)(我们需要超级用户权限才能使用蓝牙子系统):

**sudo-E python 3-m openwifipass–SSID<SSID>–PSK<PSK>**

**使用你的 shell 的[引用](https://www.gnu.org/savannah-checkouts/gnu/bash/manual/bash.html#Quoting)去掉`SSID` / `PSK`中某些字符的特殊含义。**在下面的例子中，我们使用单引号(`'`)来防止 PSK 中的`$`字符的外壳扩展。

该协议的成功运行如下所示:

**pi @ raspberrypi:~/openwifipass $ sudo-E python 3-m openwifipass–SSID OWL–PSK ' $ uper $ ecretPassword '
开始扫描…
SSID 匹配在 PWS 广告从 aa:bb:cc:dd:ee:ff
连接设备 aa:bb:cc:dd:ee:ff
发送 PWS1
接收 PWS2
发送 M1
接收 M2
发送 M3
接收 M4 【T10**

**OPACK**

这个项目包含一个可重用的 OPACK(反)序列化器。阅读 [OPACK.md](https://github.com/seemoo-lab/openwifipass/blob/main/OPACK.md) 了解更多信息。

**作者**

*   詹尼克·洛伦茨

**出版物**

*   米兰·斯图特、亚历山大·海因里希、扬尼克·洛伦茨和马蒂亚斯·霍利克。**破坏苹果无线生态系统安全的连续性:通过蓝牙低能耗、AWDL 和 Wi-Fi 对 iOS 和 macOS 进行新的跟踪、DoS 和 MitM 攻击。** *第 30 届 USENIX 安全研讨会(USENIX 安全' 21)* ，2021 年 8 月 11-13 日，加拿大不列颠哥伦比亚省温哥华。*出现*。
*   詹尼克·洛伦茨。**全民 Wi-Fi 共享:逆向工程，破解苹果 Wi-Fi 密码共享协议。**学士论文，*达姆施塔特工业大学*，2020 年 3 月。

**免责声明**

OpenWifiPass 是一款实验性软件，是由[开放无线链接](https://owlink.org)项目逆向工程努力的结果。该守则仅用于记录和教育目的。是*未检验*和*未完成*。例如，代码**不验证请求者**的身份。因此，不要对敏感的 Wi-Fi 凭证使用此实现。OpenWifiPass 不隶属于苹果公司，也不被苹果公司认可。

[**Download**](https://github.com/seemoo-lab/openwifipass)