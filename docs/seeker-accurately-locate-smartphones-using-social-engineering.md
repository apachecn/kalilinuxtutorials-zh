# seeker v 1 . 1 . 9–使用社会工程精确定位智能手机

> 原文：<https://kalilinuxtutorials.com/seeker-accurately-locate-smartphones-using-social-engineering/>

[![Seeker V1.1.9 – Accurately Locate Smartphones Using Social Engineering](img/6b2110180aa817fe02df662de80924b3.png "Seeker V1.1.9 – Accurately Locate Smartphones Using Social Engineering")](https://1.bp.blogspot.com/-coP8IPGCAVQ/XdPQVEtF-7I/AAAAAAAADfs/FmOuPjkLmSMy10GjC373DoB5OpVBzbgggCLcBGAsYHQ/s1600/Seeker%25281%2529.png)

**Seeker** 很简单，就像我们托管钓鱼页面以获取凭证一样，为什么不托管一个像许多流行的基于位置的网站那样请求您的位置的虚假页面呢？

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

该工具是一个概念证明，仅用于教育目的，它显示了恶意网站可以收集哪些关于您和您的设备的数据，以及为什么您不应该单击随机链接并允许关键权限，如位置等。

**也可阅读-[勇敢的浏览器-安全、快速&带广告拦截器的私人网络浏览器](https://kalilinuxtutorials.com/brave-browser-secure-fast-private-web-browser-adblocker/)**

**这与 IP 地理定位有何不同？**

*   其他工具和服务提供的 IP 地理定位一点也不准确，不能给出目标的位置，而是 ISP 的大概位置。
*   它使用 HTML API 并获得位置许可，然后使用设备中的 GPS 硬件获取经度和纬度，因此它最适合智能手机，如果 GPS 硬件不存在，例如在笔记本电脑上，它会退回到 IP 地理位置，或者它会查找缓存的坐标。
*   一般来说，如果用户接受位置许可，接收到的信息的精度是**精确到大约 30 米**，精度取决于设备。

**注**:由于某些原因，iPhone 上的定位精度约为 65 米。

**测试日期:**

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

【curl-fssl https://get . docker . com-o get docker . sh

**# build finder**
CD seeker/docker build-t seeker。

**【发射导引头】**
【码头运行-t】【RM 导引头】
**#或从码头结构中拉出**
【码头提升机/导引头】
码头运行

**Termux**

**git 克隆 https://github.com/thewhiteh4t/seeker.git
CD seeker/
chmod 777 termux _ install . sh
。/termux_install.sh**

**用途**

**python 3 seeker . py-h**

**用法:seeker . py[-h][-s SUBDOMAIN]**

**可选参数:**
-h，–help 显示此帮助消息并退出
-s SUBDOMAIN，–SUBDOMAIN 为 Serveo URL 提供子域(可选)
，–KML KML 提供 KML 文件名(可选)
-t TUNNEL，–TUNNEL 指定隧道模式【手动】

# # # # # # # # # # # #
>>在第一个终端以手动方式启动 seeker，就像这样
python 3 seeker . py-t Manual

>>在第二个终端启动 Ngrok 或任何其他隧道服务的端口 8080
。/ngrok http 8080
————————————
——**#子域
# # # # # # # # # # # # #**
python 3 seeker . py-子域 Google
python 3 seeker . py-隧道手册-子域 zomato

**已知问题**

*   像 Serveo 和 Ngrok 这样的服务在俄罗斯等一些国家是被禁止的。，所以如果它在你的国家被禁止，你可能得不到一个 URL，如果没有，那么首先阅读关闭的问题，如果你的问题没有被列出，创建一个新的问题。

**演示**

[https://www.youtube.com/embed/ggUGPq4cjSM?feature=oembed&enablejsapi=1](https://www.youtube.com/embed/ggUGPq4cjSM?feature=oembed&enablejsapi=1)

[**Download**](https://github.com/thewhiteh4t/seeker)