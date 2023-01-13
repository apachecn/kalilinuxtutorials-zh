# Fail2Ban:守护进程禁止导致多个身份验证错误的主机

> 原文：<https://kalilinuxtutorials.com/fail2ban/>

[![Fail2Ban : Daemon To Ban Hosts That Cause Multiple Authentication Errors](img/d3cb921a1d745dd5c6ba8fd432892fea.png "Fail2Ban : Daemon To Ban Hosts That Cause Multiple Authentication Errors")](https://1.bp.blogspot.com/-qd0HM80Uemw/Xb7xUbp3p9I/AAAAAAAADPc/OgbBEBR-tl0qjMias90hrsqStVR4G9wNwCLcBGAsYHQ/s1600/Fail2Ban.png)

**Fail2Ban** 扫描类似`**/var/log/auth.log**`的日志文件，禁止 IP 地址进行过多失败的登录尝试。它通过更新系统防火墙规则来拒绝来自这些 IP 地址的新连接，并持续一段可配置的时间。

Fail2Ban 是现成的，可以读取许多标准日志文件，比如 sshd 和 Apache 的日志文件，并且可以很容易地配置为读取您选择的任何日志文件，针对您希望的任何错误。

尽管 Fail2Ban 能够降低不正确身份验证尝试的比率，但它无法消除弱身份验证带来的风险。如果您真想保护服务，请将服务设置为仅使用两个因素或公共/私有身份验证机制。

本自述文件是对 Fail2Ban 的快速介绍。在 fail2ban(1)联机帮助页、 [Wiki](https://github.com/fail2ban/fail2ban/wiki) 、[开发者文档](https://fail2ban.readthedocs.io/)和网站:【https://www.fail2ban.org】T4 上可以找到更多的文档、常见问题和操作方法

**也可阅读-[pock int:为 DFIR/OSINT 专业人士准备的便携式 OSINT 瑞士军刀](https://kalilinuxtutorials.com/pockint-portable-osint-swiss-army-knife-dfir-osint/)**

**安装**

有可能 Fail2Ban 已经打包好供您分发了。在这种情况下，您应该改用 that。

**必需的**:

*   [Python2 > = 2.6 或者 Python > = 3.2](https://www.python.org/) 或者 [PyPy](https://pypy.org/)

**Optional** :

*   [pyinotify > = 0.8.3](https://github.com/seb-m/pyinotify) ，可能需要:
    *   Linux >= 2.6.13
*   [野孩> = 0.0.21](http://www.gnome.org/~veillard/gamin)
*   [systemd > = 204](http://www.freedesktop.org/wiki/Software/systemd) 和 python 绑定:
    *   [python 系统软件包](https://www.freedesktop.org/software/systemd/python-systemd/index.html)
*   dnspython

**安装:**

**tar xvfj fail 2 ban-0 . 11 . 0 . tar . bz2
CD fail 2 ban-0 . 11 . 0
sudo python setup . py install**

或者，您可以将源代码从 GitHub 克隆到您选择的目录中，并从那里进行安装。选择正确的分支，例如 0.11

**git 克隆 https://github.com/fail2ban/fail2ban.git
CD fail 2 ban
sudo python setup . py install**

这将把 Fail2Ban 安装到 python 库目录中。可执行脚本放在`**/usr/bin**`中，配置放在`**/etc/fail2ban**`中。

Fail2Ban 现在应该正确安装了。只需键入:

**fail2ban-client -h**

看看是否一切正常。你应该总是使用 fail2ban-client，永远不要直接调用 fail2ban-server。您可以验证是否安装了正确的版本

**fail 2 ban-客户端版本**

请注意，系统初始化/服务脚本不会自动安装。要将 fail2ban 启用为自动服务，只需将您的发行版脚本从`**files**`目录复制到`**/etc/init.d**`。示例(在基于 Debian 的系统上):

**CP files/debian-initd/etc/init . d/fail 2 ban
update-RC . d fail 2 ban defaults
service fail 2 ban start**

**配置**

您可以使用`**/etc/fail2ban**`中的文件配置 Fail2Ban。可以使用`**fail2ban-client**`发送的命令来配置服务器。fail2ban-client(1)联机帮助页中介绍了可用的命令。另请参见 fail2ban(1)和 jail.conf(5)联机帮助页，了解更多参考信息。

[**Download**](https://github.com/fail2ban/fail2ban)