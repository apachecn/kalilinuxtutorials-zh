# 探索者:使用社会工程精确定位智能手机

> 原文：<https://kalilinuxtutorials.com/seeker-locate-smartphones-using-social-engineering-2/>

[![Seeker : Accurately Locate Smartphones Using Social Engineering](img/c4429a7abfcf7651b6a9779d767297b2.png "Seeker : Accurately Locate Smartphones Using Social Engineering")](https://1.bp.blogspot.com/-v0Y52e3-Xv4/Xe0vzk8TJHI/AAAAAAAAD10/Lr5f_ozB-Dw5di1Zwl2h80nzen4H8CEWwCLcBGAsYHQ/s1600/seeker%25281%2529.png)

Seeker 背后的概念很简单，就像我们托管钓鱼页面以获取凭证一样，为什么不托管一个像许多流行的基于位置的网站一样请求您的位置的假页面。

它在内置的 PHP 服务器中的**上托管了一个假网站，并使用 **Serveo** 生成一个链接，我们将该链接转发给目标，网站请求位置许可，如果目标允许，我们可以获得:**

*   经度
*   纬度
*   准确(性)
*   海拔——并不总是可用
*   方向–仅在用户移动时可用
*   速度–仅在用户移动时可用

除了位置信息，我们还获得了没有任何权限的**设备信息**:

*   操作系统
*   平台
*   CPU 核心的数量
*   RAM 的数量–近似结果
*   屏幕分辨率
*   GPU 信息
*   浏览器名称和版本
*   公共 IP 地址
*   IP 地址侦察

该工具是一个概念证明，仅用于教育目的，Seeker 显示了恶意网站可以收集哪些关于您和您的设备的数据，以及为什么您不应该单击随机链接并允许关键权限，如位置等。

**也可以理解为-[burp suite:Secret Finder 扩展，用于从 HTTP 响应](https://kalilinuxtutorials.com/burpsuite-secret-finder/)中发现 API keys/token**

**这与 IP 地理定位有何不同？**

*   其他工具和服务提供的 IP 地理定位一点也不准确，不能给出目标的位置，而是 ISP 的大概位置。
*   搜索者使用 HTML API 并获得位置许可，然后使用设备中的 GPS 硬件获取经度和纬度，因此搜索者最适合智能手机，如果 GPS 硬件不存在，例如在笔记本电脑上，搜索者将退回到 IP 地理位置，或者它将查找缓存的坐标。
*   一般来说，如果用户接受位置许可，接收到的信息的精度是**精确到大约 30 米**，精度取决于设备。

**注**:由于某些原因，iPhone 上的定位精度约为 65 米。

**模板**

您可以从以下模板中选择一个供搜索者使用的模板:

*   靠近你
*   Google Drive(由@Akaal_no_one 建议)

**测试于**

*   卡利 Linux 2019.2
*   BlackArch Linux
*   Ubuntu 19.04
*   卡利·网络猎人
*   泰尔穆克
*   鹦鹉操作系统

**安装**

**卡莉 Linux / Ubuntu / Parrot OS**

**git 克隆 https://github.com/thewhiteh4t/seeker.git
CD seeker/
chmod 777 install . sh
。/install.sh**

**BlackArch Linux**

**pacman -S 导引头**

**码头工人**

**码头工人拉着怀特 4t/导引头**

**Termux**

**git 克隆 https://github.com/thewhiteh4t/seeker.git
CD seeker/
chmod 777 termux _ install . sh
。/termux_install.sh**

**已知问题**

*   像 Serveo 和 Ngrok 这样的服务在俄罗斯等一些国家是被禁止的。，所以如果它在你的国家被禁止，你可能得不到一个 URL，如果没有，那么首先阅读关闭的问题，如果你的问题没有被列出，创建一个新的问题。

**演示**

https://www.youtube.com/watch?v=FEyAPjkJFrk[**Download**](https://github.com/thewhiteh4t/seeker)