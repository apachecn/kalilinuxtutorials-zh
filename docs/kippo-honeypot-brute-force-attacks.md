# kippo–SSH 蜜罐

> 原文：<https://kalilinuxtutorials.com/kippo-honeypot-brute-force-attacks/>

[![Kippo – SSH Honeypot](img/cee7534d2f7c0149d7131980fcbf5984.png "Kippo – SSH Honeypot")](https://1.bp.blogspot.com/-X202UUIeeno/XQl-GaTTH2I/AAAAAAAAA5A/StSDTVWwhCs61ob7Fqb4jDeOYCBo_lnZwCLcBGAs/s1600/SSH%2BHoneypot.png)

Kippo 是一个中型交互 SSH 蜜罐，旨在记录暴力攻击，最重要的是，记录攻击者执行的整个 shell 交互。

下面是一些有趣的 Kippo 安装日志(借助 Ajaxterm 可以在 web 浏览器中查看)。请注意，自记录这些日志以来，一些命令可能已经得到了改进。

*   2009 年 11 月 22 日
*   2009 年 11 月 23 日
*   2009 年 11 月 23 日
*   [2010-03-16](http://kippo.rpg.fi/playlog/?l=20100316-233121-1847.log)

**特性**

一些有趣的功能:

*   能够添加/删除文件的假文件系统。包括一个完整的类似 Debian 5.0 安装的假文件系统
*   添加虚假文件内容的可能性，因此攻击者可以“猫”文件，如/etc/passwd。仅包含最少的文件内容
*   以兼容 [UML 的](http://user-mode-linux.sourceforge.net/)格式存储的会话日志，便于使用原始计时进行重放
*   就像 Kojoney 一样，Kippo 保存用 wget 下载的文件，供以后检查
*   诡计；ssh 假装连接到某个地方，exit 并不真正退出，等等

**亦读-[Salsa 工具:ShellReverse TCP/UDP/ICMP/DNS/SSL/bind TCP&AV Bypass，AMSI 打补丁](https://kalilinuxtutorials.com/salsa-tools-shellreverse/)**

**要求**

所需软件:

*   操作系统(在 Debian、CentOS、FreeBSD 和 Windows 7 上测试)
*   Python 2.5 以上版本
*   扭曲 8.0 到 15.1.0
*   密码是什么
*   Zope 接口

参见 Wiki 获取一些安装说明。

**如何运行它？**

根据您的喜好编辑 kippo.cfg 并运行以下命令启动蜜罐:

**。/start.sh**

start.sh 是一个简单的 shell 脚本，它使用 twistd 在后台运行 Kippo。可以通过手动运行 twistd 给出详细的启动选项。例如，要在前台运行 Kippo:

**twistd -y kippo.tac -n**

默认情况下，Kippo 监听端口 2222 上的 ssh 连接。您可以更改它，但不要将其更改为 22，因为它需要 root 权限。请改用端口转发。(更多信息:[制作 KippoReachable](https://github.com/desaster/kippo/wiki/Making-Kippo-Reachable) )。

感兴趣的文件:

*   dl/–用 wget 下载的文件存储在这里
*   log/kippo . log–记录/调试输出
*   日志/tty/–会话日志
*   utils/playlog . py–重放会话日志的实用程序
*   utils/create fs . py–用于创建 fs.pickle
*   fs . pickle——假文件系统
*   honey fs/——伪文件系统的文件内容——在这里可以随意复制一个真实的系统

[**Download**](https://github.com/desaster/kippo)