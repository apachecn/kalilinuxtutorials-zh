# HiddenEye:具有高级功能的现代网络钓鱼工具

> 原文：<https://kalilinuxtutorials.com/hiddeneye-modern-phishing-tool/>

[![HiddenEye : Modern Phishing Tool With Advanced Functionality](img/2a7b513110b203a5949a519d0472dc3e.png "HiddenEye : Modern Phishing Tool With Advanced Functionality")](https://1.bp.blogspot.com/-75b6eGtgLeE/XTXMHOjr_6I/AAAAAAAABg8/CaDV1SNfGL42ZZ-PPVA0-okNcrQssptGQCLcBGAs/s1600/logo%25281%2529.png)

HiddenEye 是一款具有高级功能的现代网络钓鱼工具，目前也支持 Android。现在你将有受害者的实时信息，如:IP 地址，地理位置，ISP，国家，&等等。

**在以下**测试

*   kali Linux–滚动版
*   Parrot OS 滚动版
*   Linux as-18.3 西尔维娅
*   Ubuntu–2010 年 4 月 16 日
*   马科斯高塞拉
*   Arch Linux
*   曼哈罗 XFCE 版 17.1.12
*   黑色拱门
*   Userland 应用程序(适用于 Android 用户)

**先决条件**

*   python3
*   来自 Python 的 Wget
*   服务器端编程语言（Professional Hypertext Preprocessor 的缩写）
*   须藤

**也可阅读-[Blisqy:利用 HTTP-Headers 中基于时间的盲 SQL 注入](https://kalilinuxtutorials.com/blisqy-blind-sql-injection/)**

**有什么新功能**

**兼容性**

*   所有的网站都是手机兼容的。

**键盘记录器**

*   现在你也将有能力捕获受害者的所有按键。
*   您现在可以使用(Y/N)选项来部署按键记录程序。
*   修复了主要问题。

**安卓支持**

*   我们关心 Android 用户，所以现在我们提供了两种在 Android 设备上运行该工具的方法。
    *   **UserLand App**
        *   你必须下载 UserLand 应用程序。[点击这里](https://play.google.com/store/apps/details?id=tech.ula)下载。
        *   要了解更多如何设置 userland 应用程序，请阅读此处的
    *   **Termux 应用**
        *   你必须下载 Termux 应用程序。[点击这里](https://play.google.com/store/apps/details?id=com.termux)下载。
        *   如需更多说明[，请查看说明](https://github.com/DarkSecDevelopers/HiddenEye/blob/master/instructions.md)
        *   Termux 用户使用此命令克隆，除非在运行过程中可能出现错误。

git 克隆-b Termux-支持-分支 https://github.com/DarkSecDevelopers/HiddenEye.git

**提供新外观**

*   现在轻松专注于任务…
*   使用您自己的主题自定义应用程序

**SERVEO URL 类型选择现已推出**

*   serveo 的主要问题已修复。
*   现在你可以选择自定义网址和随机网址。

**添加了大量网络钓鱼页面**

*   页面取自各种工具，包括 ShellPhish、Blackeye、SocialFish。

**如何安装**

*   **黑拱门官方仓库**

**须藤吃豆人的隐眼**

要运行，只需使用

**须藤隐眼**

*   **克隆**

**git 克隆 https://github.com/DarkSecDevelopers/HiddenEye.git**

**【运行中(Linux)】**

**cd HiddenEye
sudo 安装 python 3-pip
sudo pip 3 install-r requirements . txt
chmod 777 HiddenEye . py
python 3 HiddenEye . py**

运筹学

**。/HiddenEye.py**

**【运行(Arch Linux 或 Manjaro)**

CD hidden eye
sudo pacman-Syu
sudo pacman-S python-pip
sudo pip 3 install-r requirements . txt
chmod 777 hidden eye . py
sudo python 3 hidden eye . py

运筹学

须藤。/HiddenEye.py

**针对安卓用户**

*   **在(用户应用程序)中安装**
    *   从 playstore 安装 userland 应用程序。
    *   设置应用程序并从应用程序安装 kali。设置 ssh 用户名(任何名称)和密码。
    *   当 kali 运行时，它会要求输入密码，输入 ssh 密码。然后做苏。之后，kali 将在没有 root 用户的设备上运行，并进行 apt 更新，更多信息请点击此处(https://null-byte . wonder how to . com/how-to/Android-For-hackers-turn-Android-phone-into-hacking-device-without-root-0189649/)

apt 安装 python 3 & & python 3-pip & & unzip & & PHP & & git
git 克隆 https://github.com/DarkSecDevelopers/HiddenEye.git
CD HiddenEye
chmod 777 HiddenEye . py
pip 3 install-r requirements . txt
python 3 HiddenEye . py

*   **在(TERMUX 应用程序)中安装**
    *   首先从 Playstore 安装{ Termux }。
    *   打开后，一个接一个地执行下面的命令

pkg install git python PHP curl open sh grep
pip 3 install wget
git clone-b term-support branch https://github . com/darksecdevelopers/hiddenye . git
CD hiddenye
chmod 777 hiddenyee . py
python hiddenyee . py
或
/hiddenye . py

**一行命令安装在 TERMUX(安卓)**

*   首先从 Playstore 安装{ Termux }。
*   打开后，复制并运行这个命令。

pkg 安装 git python PHP curl OpenSSH grep & & pip 3 安装 wget & & git clone-b Termux-Support-Branch https://github.com/DarkSecDevelopers/HiddenEye.git & & CD hidden eye & & chmod 777 hidden eye . py & & python hidden eye . py

**可用页面**

*   **脸书:**
    *   传统脸书登录页面。
    *   高级投票方法。
    *   用脸书·佩奇的假安全登录。
    *   脸书信使登录页面。
*   **谷歌:**
    *   传统的谷歌登录页面。
    *   高级投票方法。
    *   新的谷歌页面。
*   **领英:**
    *   传统 LinkedIn 登录页面。
*   **Github:**
    *   传统 Github 登录页面。
*   **堆栈溢出:**
    *   传统 Stackoverflow 登录页面。
*   WordPress:T1
    *   类似的 WordPress 登录页面。
*   **推特:**
    *   传统的 Twitter 登录页面。
*   **Instagram:**
    *   传统 Instagram 登录页面。
    *   Instagram 自动链接钓鱼页面。
    *   Instagram 个人资料场景高级攻击。
    *   Instagram 徽章验证攻击*【新】*
    *   Instagram 自动关注钓鱼网页作者([https://github.com/thelinuxchoice](https://github.com/thelinuxchoice))
*   **SNAPCHAT 网络钓鱼:**
    *   传统 Snapchat 登录页面
*   **雅虎钓鱼:**
    *   传统雅虎登录页面
*   **TWITCH 钓鱼:**
    *   传统 Twitch 登录页面[也可使用脸书登录]
*   **微软网络钓鱼:**
    *   传统 Microsoft-Live Web 登录页面
*   **蒸汽钓鱼:**
    *   传统 Steam Web 登录页面
*   **VK 钓鱼:**
    *   传统 VK 网站登录页面
    *   高级轮询方法
*   **ICLOUD 网络钓鱼:**
    *   传统 iCloud Web 登录页面
*   **GitLab 网络钓鱼:**
    *   传统 GitLab 登录页面
*   **网飞钓鱼:**
    *   传统网飞登录页面
*   **来源网络钓鱼:**
    *   传统来源登录页面
*   **Pinterest 钓鱼:**
    *   传统 Pinterest 登录页面
*   **质子邮件网络钓鱼:**
    *   传统的 Protonmail 登录页面
*   **Spotify 网络钓鱼:**
    *   传统 Spotify 登录页面
*   **Quora 钓鱼:**
    *   传统 Quora 登录页面
*   **PornHub 网络钓鱼:**
    *   传统 PornHub 登录页面
*   **Adobe 网络钓鱼:**
    *   传统 Adobe 登录页面
*   **Badoo 网络钓鱼:**
    *   传统 Badoo 登录页面
*   **加密货币网络钓鱼:**
    *   传统加密货币登录页面
*   **DevianArt 网络钓鱼:**
    *   传统 DevianArt 登录页面
*   **DropBox 钓鱼:**
    *   传统 DropBox 登录页面
*   **易贝钓鱼:**
    *   传统易贝登录页面
*   **MySpace 钓鱼:**
    *   传统 Myspace 登录页面
*   **PayPal 网络钓鱼:**
    *   传统 PayPal 登录页面
*   **Shopify 网络钓鱼:**
    *   传统 Shopify 登录页面
*   **威瑞森钓鱼:**
    *   传统威瑞森登录页面
*   **Yandex 钓鱼:**
    *   传统 Yandex 登录页面

**Ascii 错误修复**

*   dpkg-重新配置语言环境
*   然后选择:“所有地区”，然后选择“美国”。UTF-8”
*   之后，重新启动你的机器。然后打开终端并运行命令:“locale”
*   在那里你会看到“en_US。UTF-8”，这是默认语言。而不是 POSIX。

**免责声明**

仅用于教育目的

该工具的使用完全由最终用户负责。开发人员不承担任何责任，也不对本程序造成的任何误用或损坏负责。请阅读[执照](https://github.com/DarkSecDevelopers/HiddenEye/blob/master/LICENSE)。

**信用**

*   nud 4 和
*   乌萨马
*   斯蒂基特
*   十一秒
*   不选择

[**Download**](https://github.com/DarkSecDevelopers/HiddenEye)