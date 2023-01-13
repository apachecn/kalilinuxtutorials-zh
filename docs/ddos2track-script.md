# DDOS 2 track–避免 HTTP 洪水攻击的脚本

> 原文：<https://kalilinuxtutorials.com/ddos2track-script/>

使用 Ddos2track 工具，您可以阻止 HTTP 洪水攻击，并使用蜜罐将其分解。

该工具在检测到 DDOS 攻击后会向您发送广告邮件！

首先开始蜜罐服务器( **tools/analyze/logger.py** )。

此时，在另一个窗口中开始定位器(**tools/detector/detector . sh**)。

万一攻击者在预先配置的端口(80)攻击您的服务器，指示器将在 5 秒钟内将所有攻击者请求重定向到蜜罐，然后攻击者 IP 将被阻止。

#### **又读[lib 钠——好用的软件库](http://kalilinuxtutorials.com/libsodium/)**

您可以修改选项并激活重定向 2 攻击者，此选项允许您将所有流量重定向到攻击者 IP，因此攻击者将对其自己的网络进行攻击😉

要查看所有 DDoS 请求，您可以在' **/tools/analyzer/ddos.log** 查看日志。要查看所有攻击者 IP，您可以在'**tools/detector/attackers . txt**查看日志

## **安装 Ddos2track**

chmod 777 INSTALL.sh

## **利用**

。/DDOS 2 跟踪指令

[![](img/a51de913dc60eee505c4a68651ee8e4d.png)](https://github.com/lockedbyte/ddos2track)