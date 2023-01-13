# SUDO 杀手:识别和利用数独规则的工具

> 原文：<https://kalilinuxtutorials.com/sudo_killer/>

[![SUDO_KILLER : A Tool To Identify & Exploit Sudo Rules](img/c1eb537a629069218ac839e7c7427a4a.png "SUDO_KILLER : A Tool To Identify & Exploit Sudo Rules")](https://1.bp.blogspot.com/-gQoOSwQvLJQ/XlCgbnMinYI/AAAAAAAAFE4/asyqsWchLSEFO4ZddF75Dv4KksbiV-zYQCLcBGAsYHQ/s1600/SUDO_KILLER.png)

SUDO 杀手是一个可以在 linux 环境下通过几种方式滥用 SUDO 来提升权限的工具。该工具有助于识别 sudo 规则中的错误配置、正在使用的 sudo 版本中的漏洞(CVEs 和 vulns)以及危险二进制文件的使用，所有这些都可能被滥用来提升 ROOT 权限。

然后，它会提供一个命令或本地攻击的列表，这些命令或攻击可能会被用来提升权限。值得注意的是，该工具不会代表您执行任何利用，利用将需要手动执行，这是有意的。

**特性**

由工具执行的一些检查/功能。

*   错误配置
*   危险的二进制
*   sudo-CVEs 的易受攻击版本
*   危险的环境变量
*   凭据收集
*   脚本所在的可写目录
*   可能被替换的二进制文件
*   身份缺失脚本

**用途**

**示例在线模式**

**。/sudo _ killer . sh-c-e-r report . txt-p/tmp**

**离线模式示例**

在要审计的系统/受害者计算机上运行 extract.sh。将待审计系统/受害者计算机上/tmp/sk_offline.txt 的输出复制到您的主机。

*   **注意:离线模式下缺少三个检查，仍在开发中…即将推出…**

使用以下参数运行 SK:

**。/sudo _ killer . sh-c-I/path/sk _ offline . txt**

**可选参数**

*   -c:包括关于 sudo 版本的 CVE 检查
*   -i:从 extract.sh 导入(脱机模式)
*   -e:包括 sudo 规则/ sudoers 文件的导出
*   -r:报告名称(保存输出)
*   -p:保存导出和报告的路径
*   -s:为 sudo 检查提供用户密码(不推荐++除了 CTF)
*   救命啊

**cv 检查**

要更新 CVE 数据库，请执行以下脚本。/cve_update.sh

**提供密码(重要)**

如果您需要输入一个密码来运行 sudo -l，那么如果您不使用参数-s 提供密码，这个脚本将无法运行。

**如何在目标/审计机器上运行 SK**

如果你在一台有互联网连接的机器上，只需 git 克隆这个工具并运行它。如果你在一台没有互联网的机器上，那么在你的主机上进行 git 克隆，压缩工具(tar ),然后通过 http/SMB(Apache web server/python simple httpserver/SMB server/NC)传输压缩文件，然后在目标系统上解压缩文件，尽情享受吧！

**注释**

它本身不会自动利用漏洞，它是故意这样设计的，但会检查配置和漏洞，然后向您提出以下建议(如果您幸运的话，到 root 的路径很近！) :

*   要利用的命令列表
*   功绩列表
*   关于攻击的方式和原因的一些描述

**为什么没有密码也可以运行“sudo -l”？**

默认情况下，如果 NOPASSWD 标记应用于主机上用户的任何条目，他或她将能够运行“sudo -l”而无需密码。可以通过 verifypw 和 listpw 选项覆盖此行为。

但是，这些规则只影响当前用户，所以如果用户模拟是可能的(使用 su ),那么 sudo -l 也应该从这个用户启动。

有时，即使没有密码无法访问 sudo -l，也可以读取/etc/sudoers 文件。

**演示**

[https://www.youtube.com/embed/Q8iO9mYrfv8?list=PLQPKPAuCA40FMpMKWZLxQydLe7rPL5bml&enablejsapi=1](https://www.youtube.com/embed/Q8iO9mYrfv8?list=PLQPKPAuCA40FMpMKWZLxQydLe7rPL5bml&enablejsapi=1)

**警告**

这是杀手计划的一部分。它仍在开发中，可能会有一些问题，请创建一个问题，如果你发现任何问题。**

其他工具将在接下来的几个月中添加到杀手级项目中，敬请关注。也欢迎想法、错误报告和贡献！

**学分**

这个脚本是我在 github 和野外找到的在线资源的帮助下开发的。与 CVEs 相关的开发的作者也有功劳。作者信息和链接可以在漏洞和运行工具时提供的注释中找到。特别要感谢 Vincent Puydoyeux，他给了我开发这个工具和 Koutto 的想法，帮助我处理 docker 的事情并改进了这个工具。

[**Download**](https://github.com/TH3xACE/SUDO_KILLER)