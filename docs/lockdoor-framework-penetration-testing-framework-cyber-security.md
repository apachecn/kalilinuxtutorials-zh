# Lockdoor 框架:一个包含网络安全资源的渗透测试框架

> 原文：<https://kalilinuxtutorials.com/lockdoor-framework-penetration-testing-framework-cyber-security/>

[![Lockdoor Framework : A Penetration Testing Framework with Cyber Security Resources](img/ba319ec77fe49a224b001854bf320557.png "Lockdoor Framework : A Penetration Testing Framework with Cyber Security Resources")](https://1.bp.blogspot.com/-hs7drro9nKM/XZbj_NT0YoI/AAAAAAAACy4/nRmumAp13i0rWtXUDrZzCPuf8Qs15Vb9gCLcBGAsYHQ/s1600/logo205x250.gif)

**LockDoor** 是一个旨在**帮助渗透测试人员、bug 赏金猎人和网络安全工程师**的框架。这个工具是为基于 Debian/Ubuntu/ArchLinux 的发行版设计的，为渗透测试创建一个相似的和熟悉的发行版。但是包含了 Pentesters 最喜欢和最常用的工具。

作为 pentesters，我们大多数人都有自己的“/pentest/”目录，所以这个框架可以帮助你建立一个完美的目录。所有这些！它使测试过程自动化，帮助您更快更轻松地完成工作。

在 Kali，Ubuntu，Arch，Fedora，Opensuse 和 Windows 上测试。

**特性**

附加值:(它与其他框架的不同之处)。

**测试工具选择**

*   **工具？** : **锁门**不包含所有的测试工具(附加值)，实话实说吧！谁曾经使用过你在所有那些渗透测试发行版上找到的所有工具？Lockdoor 只包含 Pentesters 最喜欢的(附加值)和最常用的工具(附加值)。
*   **什么工具？**:工具包含 **Lockdoor** 是 Kali、Parrot Os、BlackArch 上最好的工具(附加值)的集合。也有一些私人工具(增值)来自其他一些黑客团队(增值)，如 InurlBr，伊朗网络。不要忘了我在 Github 上发现的一些很酷很神奇的工具，它们是由一些完美的人类 beigns(附加值)制作的。
*   **轻松定制**:轻松添加/移除工具。(附加值)
*   **安装**:您可以使用 installer.sh 自动安装该工具，手动安装或在 Docker 上安装【即将推出】

**资源和备忘单:(附加值)**

*   **资源**:这就是**锁门**的附加值，锁门不仅仅包含工具！测试和安全评估结果报告模板(附加值)、测试演练示例和模板(附加值)等。
*   **备忘单**:每个人都可能会忘记一些关于加工或工具使用的事情，甚至一些检查。Cheatsheets(附加值)角色来了！有关于一切的备忘单，框架上的每个工具以及任何枚举、利用和后利用技术。

**另请阅读-[terra form AWS 安全基线:设置您的 AWS 帐户](https://kalilinuxtutorials.com/terraform-aws-secure-baseline/)**

**安装**

**自动**

git 克隆 https://github.com/SofianeHamlaoui/Lockdoor-Framework.git & CD 锁门框架
chmod +x ./install.sh
。/install.sh

**手动**

**安装要求**

python python-pip python-requests python 2 python 2-pip gcc ruby PHP git wget BC curl netcat subversion JRE-open JDK make automake gcc Linux-headers gzip

**安装 Go**

wget https://dl.google.com/go/go1.13.linux-amd64.tar.gz
tar-xvf go1.13.linux-amd64.tar.gz
mv go/usr/local
export go root =/usr/local/go
export PATH = $ GOPATH/bin:$ go root/bin:$ PATH
RM go1.13.linux-amd64.tar.gz

**安装门锁**

**# cloning** git 克隆 https://github.com/SofianeHamlaoui/Lockdoor-Framework.git&&CD Lockdoor-Framework
**#创建配置文件
# INSTALLDIR =您要安装 lock door 的位置(Ex:/opt/sofiane/pentest)**
echo " Location:" $ install dir>$ HOME "/。config/lockdoor/lock door . conf "
**#移动资源文件夹**
mv tools resources/* install dir
**#从 PyPi 安装 lock door**
pip 3 安装 lock door

[**Download**](https://github.com/SofianeHamlaoui/Lockdoor-Framework)