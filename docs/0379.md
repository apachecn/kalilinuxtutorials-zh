# Killcast:操纵你网络中的 Chromecast 设备

> 原文：<https://kalilinuxtutorials.com/killcast-chromecast-network/>

Killcast 操纵你网络中的 chromecast 设备。这个工具是一个概念证明，仅用于研究目的，它显示了 Chromecast 设备是如何被任何人轻易操纵和劫持的。

受这个黑客的启发，thewhiteh4t 创建了它，这是一个用于测试和研究目的的开源工具，如果你有一个 Google Home 或 Chromecast，你可以测试并了解如果它们暴露在外或如果你在同一个网络中，操纵这些设备是多么简单。

**特性**

*   提取有趣的信息，如版本，国家，时区等
*   重新命名
*   重新启动
*   执行工厂重置
*   关闭 YouTube、网飞和 Google Play Music 等活跃应用

另请阅读:[h8 mail–电子邮件登录和密码破解搜索](https://kalilinuxtutorials.com/h8mail-email-password-breach/)

**什么是不工作**

*   播放任何 YouTube 视频
*   无法停止播放音乐
*   其他我们不知道的事情😉

**测试于:**

*   Kali Linux 2019.1
*   Ubuntu 18.04
*   泰尔穆克

**安装**

**Ubuntu/Kali Linux/Termux**

**git 克隆 https://github.com/thewhiteh4t/killcast.git
CD kill cast
apt-get 安装 python3
pip 安装请求**

**用途**

**python3 killcast.py -h**

**用法:**

**killcast.py [-h] -t IP**

**操控网络中的 Chromecast 设备**

**可选参数:
-h，–help 显示此帮助信息并退出
-t IP，–IP chrome cast 的 IP 地址
python 3 kill cast . py-t 192 . 168 . 0 . 100**

**视频教程**

[https://www.youtube.com/embed/8wmWnMVE2aw?feature=oembed&enablejsapi=1](https://www.youtube.com/embed/8wmWnMVE2aw?feature=oembed&enablejsapi=1)

[**Download**](https://github.com/thewhiteh4t/killcast)