# Kali Linux 2020.1 版本

> 原文：<https://kalilinuxtutorials.com/kali-linux-2020-1/>

[![Kali Linux 2020.1 Release](img/f12fd4ad0cdde170e72429dbca184de5.png "Kali Linux 2020.1 Release")](https://1.bp.blogspot.com/-NxyuH8ZsBjo/XjGPC7j2mBI/AAAAAAAAEq0/lJsTQjf5UuoROKeToXwv1cmSkT1rnFHdgCLcBGAsYHQ/s1600/Kali%2BLinux%25281%2529.png)

我们非常兴奋地宣布 2020 年的第一个版本，Kali Linux 2020.1。它包括一些激动人心的新更新:

*   [非根默认](https://www.kali.org/news/kali-default-non-root-user/)
*   Kali 单一安装程序映像
*   [Kali NetHunter 无根](https://www.kali.org/docs/nethunter/nethunter-rootless/)
*   主题和卡利-卧底的改进
*   新工具

**非根**

纵观 Kali(及其前身 BackTrack、WHAX 和 Whoppix)的历史，默认凭证一直是`root/toor`。这是没有了。在 Kali 2020.1 中，我们不再默认使用超级用户帐号 root。默认用户帐户现在是一个标准的无特权用户。

`**root/toor**`已死。`**kali/kali**`万岁。

**网络猎人图片**

移动笔测试平台 Kali NetHunter 也有一些新的改进。你现在不再需要启动你的手机来运行 Kali NetHunter，但是这也有一些限制。为了满足每个人的需求，Kali NetHunter 现在有以下三个版本:

*   **NetHunter**–需要带有定制恢复和补丁内核的根设备。没有任何限制。设备特定的图像可在[这里](https://www.offensive-security.com/kali-linux-nethunter-download/)获得。
*   **NetHunter Light**–需要带自定义恢复的根设备，但没有自定义内核。具有较小的限制，即没有 WiFi 注入或 HID 支持。具体的建筑图片可在[这里](https://www.offensive-security.com/kali-linux-nethunter-download/)获得。
*   **NetHunter Rootless**–可安装在所有使用 Termux 的标准、未经修改的设备上。一些限制，比如 Metasploit 中缺少 db 支持，没有 root 权限。安装说明可在[这里](https://www.kali.org/docs/nethunter/nethunter-rootless/)获得。

NetHunter 文档页面包含了更详细的比较。

**升级到 Kali Linux 2020.1**

**现有升级**如果您已经安装了 Kali，请记住您可以随时进行快速更新:

kali @ kali:~ $ cat<<eof sudo="" tee="">deb http://www . kali . org/kali-rolling main non-free contributing ...
eof
kali @ kali:~
kali:~ $ sudo apt update&&sudo apt-y full upgrade
kali @ kali</eof>

你现在应该在 Kali Linux 2020.1 上。我们可以通过以下方式进行快速检查:

kali @ kali:~ $ grep version/etc/OS-release
version = " 2020.1 "
version _ id = " 2020.1 "
version _ code = " kali-rolling "
kali @ kali:~ $
kali @ kali:~ $ uname-v
**1 SMP debian**

注意:`**uname -r**`的输出可能因架构不同而有所不同。

[**Download**](https://www.kali.org/downloads/)