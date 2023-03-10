# SUDO 杀手:识别和利用 Sudo 规则在 Sudo 中的错误配置和漏洞的工具

> 原文：<https://kalilinuxtutorials.com/sudo-killer-misconfigurations-vulnerabilities/>

[![SUDO KILLER : A Tool To Identify & Exploit Sudo Rules’ Misconfigurations & Vulnerabilities Within Sudo](img/dea31739823f29bd8a92558d50b9adb1.png "SUDO KILLER : A Tool To Identify & Exploit Sudo Rules’ Misconfigurations & Vulnerabilities Within Sudo")](https://1.bp.blogspot.com/-BXu8CtdO4Ro/XTWa7kSlguI/AAAAAAAABgA/IrEQuIMFw98e5rh0pALXDxRpg-9m2IPhwCLcBGAs/s1600/vulnerabilities.png)

SUDO 杀手是一个以不同方式帮助滥用 SUDO 的工具，其主要目标是在 Linux 环境下执行权限提升。

该工具有助于识别 sudo 规则中的错误配置、正在使用的 sudo 版本中的漏洞(CVEs 和 vulns)以及危险二进制文件的使用，所有这些都可能被滥用来将权限提升到 ROOT。

然后，SUDO 杀手会提供一个可以用来提升权限的命令或本地漏洞列表。

**SUDO 杀手**不会代表您执行任何攻击，攻击将需要手动执行，这是有意的。

**默认用法**

**例子:。/sudo _ killer . sh-c-r report . txt-e/tmp/**

**又读-[DIE:为 Windows、Linux&MAC OS](https://kalilinuxtutorials.com/die-windows-linux-macos/)确定文件类型的程序**

**论据**

*   k:关键词
*   e:出口位置(出口/etc/sudoers)
*   c:包括关于 sudo 版本的 CVE 检查
*   s:为 sudo 检查提供用户密码(不推荐++除了 CTF)
*   r:报告名称(保存输出)
*   h:救命

**【cv 检查】**

要更新 CVE 数据库，请执行以下脚本。/cve_update.sh

**重要！！！**

如果您需要输入一个密码来运行 sudo -l，那么如果您不使用参数-s 提供密码，这个脚本将无法运行。

* *注意:sudo_killer 本身不会自动利用漏洞，它是故意这样设计的，但会检查配置错误和漏洞，然后向您提出以下建议(如果您幸运的话，到 root 的路径很近！) :

*   要利用的命令列表
*   功绩列表
*   关于攻击的方式和原因的一些描述

**为什么可以不用密码运行“sudo -l”？**

默认情况下，如果 NOPASSWD 标记应用于主机上用户的任何条目，他或她将能够运行“sudo -l”而无需密码。可以通过 verifypw 和 listpw 选项覆盖此行为。

但是，这些规则只影响当前用户，所以如果用户模拟是可能的(使用 su ),那么 sudo -l 也应该从这个用户启动。

有时，即使没有密码无法访问 sudo -l，也可以读取/etc/sudoers 文件。

**从码头工人**那里拉过来

服务坞站开始【T3 xace/sudo _ killer _ demo】坞站运行–RM-it th3xace/sudo _ killer _ demo

**使用 Dockerfile** 在本地构建

服务坞站启动
git 克隆[https://github . com/th3 xace/sudo _ killer . git](https://github.com/TH3xACE/SUDO_KILLER.git)
CD sudo _ killer
dock build-T3 xace/sudo _ killer _ demo。
码头运行–RM-it th3xace/sudo _ killer _ demo

并且它将产生具有低用户权限的交互式外壳。

**学分**

剧本是我自己写的，但是在 github 和野外找到的很多在线资源的帮助下，我感谢那些激励我的人。当运行脚本时使用他们的利用/描述时，会显示致谢名单和链接。

特别赞扬文森特·普伊多约🙂是谁给了我开发这个工具的想法。

**免责声明**

这个脚本仅用于教育目的。未经允许请勿使用。通常的免责声明适用，尤其是 me (TH3xACE)对直接或间接使用这些程序提供的信息或功能所造成的任何损害不承担责任。作者或任何互联网提供商对这些程序或其衍生程序的内容或误用不承担任何责任。通过使用这些程序，您接受任何损害(数据丢失、系统崩溃、系统受损等)的事实。)使用脚本造成的后果不是我的责任。

[**Download**](https://github.com/TH3xACE/SUDO_KILLER)