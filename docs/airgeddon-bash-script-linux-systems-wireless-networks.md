# Airgeddon:这是一个供 Linux 系统审计无线网络的多用途 Bash 脚本

> 原文：<https://kalilinuxtutorials.com/airgeddon-bash-script-linux-systems-wireless-networks/>

[![Airgeddon : This Is A Multi-Use Bash Script For Linux Systems To Audit Wireless Networks](img/534a3a0affff033d595c96427cc7b80b.png "Airgeddon : This Is A Multi-Use Bash Script For Linux Systems To Audit Wireless Networks")](https://1.bp.blogspot.com/-L7Uy-ggbxks/XWOrjDdpTQI/AAAAAAAACLw/qfSXFuvAjdgtsXxumpyp9yPRMre_Yh4HQCLcBGAs/s1600/airgeddon_banner%25281%2529.png)

Airgeddon 是一个供 Linux 系统审计无线网络的多用途 bash 脚本。

**内容&特色**

*   [首页](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki)
*   [特性](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/Features)
*   [截图](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/Screenshots)
*   [壁纸](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/Wallpapers)

**要求**

*   [要求](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/Requirements)
*   [兼容性](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/Compatibility)
*   [必备工具](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/Essential%20Tools)
*   [可选工具](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/Optional%20Tools)
    *   [牛肉小贴士](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/BeEF%20Tips)
    *   [哈希卡提示](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/Hashcat%20Tips)
    *   [Bettercap 提示](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/Bettercap%20Tips)
*   [更新工具](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/Update%20Tools)
*   [内部工具](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/Internal%20Tools)
*   [已知的不兼容性](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/Known%20incompatibilities)

**亦读-[AutoRDPwn:影子攻击框架](https://kalilinuxtutorials.com/autordpwn-shadow-attack-framework/)**

**安装&使用**

必须以根用户的身份运行这个脚本，否则`airgeddon`将无法正常工作。

**通用安装**

**安装方法 1** [(最简单)要求:`git`]

*   克隆存储库
    *   `**~$ git clone --depth 1 https://github.com/v1s1t0r1sh3r3/airgeddon.git**`
*   转到新创建的目录
    *   `**~$ cd airgeddon**`
*   运行它(如果你已经有根权限，删除 **sudo**
    *   `**~/airgeddon$ sudo bash airgeddon.sh**`

**安装方法二** [(备选)要求:`wget` `unzip`]

*   下载文件
    *   `**~$ wget https://github.com/v1s1t0r1sh3r3/airgeddon/archive/master.zip**`
*   解压缩下载的文件
    *   `**~$ unzip master.zip**`
*   转到新创建的目录
    *   `**~$ cd airgeddon-master**`
*   运行它(如果你已经有根权限，删除 **sudo**
    *   `**~/airgeddon-master$ sudo bash airgeddon.sh**`

airgeddon 应该用**bash**启动，而不是用 **sh** 或任何其他类型的 shell

如果您使用另一个 shell 启动脚本，将会出现*语法错误*和错误结果。即使没有初始错误，它们也会在以后出现。总是用**迎头痛击**发动！

**二进制安装**

本节列出了可供您下载和安装 airgeddon 的二进制文件。

*   Arch Linux
    1.  下载 Arch Linux 的最新压缩包
    2.  使用`**~# pacman -U airgeddon-git-x.x-y-any.pkg.tar.xz**`安装
*   Kali Linux
    1.  下载 Kali Linux 的最新 deb 包
    2.  使用`**~# dpkg -i airgeddon_x.x-x_all.deb**`安装

**项目&开发**

*   [支持的语言](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/Supported%20Languages)
*   [投稿&行为准则](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/Contributing-&-Code-of-Conduct)
*   [变更日志](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/Changelog)
*   [免责声明&许可](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/Disclaimer%20&%20License)
*   [联系人](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/Contact)

**致谢&参考文献**

*   [帽尖到](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/Hat%20Tip%20To)
*   [灵感](https://github.com/v1s1t0r1sh3r3/airgeddon/wiki/Inspiration)

[**Download**](https://github.com/v1s1t0r1sh3r3/airgeddon)