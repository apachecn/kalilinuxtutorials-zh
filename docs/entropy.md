# Entropy:开发 Netwave 和 GoAhead IP 网络摄像头的工具集

> 原文：<https://kalilinuxtutorials.com/entropy/>

[![Entropy : Set Of Tools To Exploit Netwave & GoAhead IP Webcams](img/4113e0015063981cd1b112a42053e24f.png "Entropy : Set Of Tools To Exploit Netwave & GoAhead IP Webcams")](https://1.bp.blogspot.com/-a5mq04L0UnI/XmaToRrgPHI/AAAAAAAAFWY/acaP9q8KEg08kJTAHSZeNCK1Y8fG1Gj4QCLcBGAsYHQ/s1600/Entropy.png)

**Entropy** Toolkit 是一套利用 Netwave 和 GoAhead IP 网络摄像头的工具。熵是一个强大的网络摄像头渗透测试工具包。

**安装**

**cd 熵
chmod +x install.sh
。/install.sh**

**卸载**

**cd 熵
chmod +x uninstall.sh
。/uninstall.sh**

**也可阅读-[WiFi Passview:一个基于开源批处理脚本的 WiFi Passview For Windows](https://kalilinuxtutorials.com/wifi-passview/)**

**执行**

**熵-h**

**用法:**熵[-h][-b[1 | 2]][-o][–超时]
[-t][-c][-q |-v]
[-a |-I |–shod an |–zoomeye]
[-u]

**可选参数:**
-h，–help 显示此帮助消息并退出
-b [1|2]，–brand[1 | 2]
选择(1)Netwave，(2)GoAhead。
-o，–输出
输出到您输入的路径。
–超时超时，以秒为单位。
-t，–task
运行并行连接的任务数。
-c，–count
你想从 ZoomEye 获得的 IP 数量。
-q，–安静安静模式。
-v，–详细详细模式。
-a，–地址
IP:网络摄像头的端口地址。
-i，–输入
网络摄像头的 IP:端口地址列表。
–Shodan 您的 Shodan API 密钥。
–zoo meye 您的 ZoomEye API 密钥。
-u，–更新更新熵工具包。

**工具包示例**

*   **利用单个网络摄像头的示例**

**熵-b 1 -i 192.168.1.100:80 -v**

*   **从文件中利用网络摄像头的示例**

**熵-b 2 -l iplist.txt -v**

*   **使用 shodan 利用网络摄像头的示例**

**熵-B2-v–shodan PSK qe1 gyxggecyz 2191 h2jos 9 qvgd**

**免责声明**

未经双方同意，使用熵工具包攻击目标是非法的。最终用户有责任遵守所有适用的地方、州、联邦和国际法律。开发人员不承担任何责任，也不对本程序造成的任何误用或损坏负责。

[**Download**](https://github.com/entynetproject/entropy)