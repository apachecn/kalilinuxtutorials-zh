# PoisonApple : macOS 持久性工具

> 原文：<https://kalilinuxtutorials.com/poisonapple/>

[![PoisonApple : macOS Persistence Tool](img/916d853e2c25969057eabe4dd2f0cca8.png "PoisonApple : macOS Persistence Tool")](https://1.bp.blogspot.com/-GXpI3G7Y-Jg/YHdPWTQvzJI/AAAAAAAAIuQ/wuR7FlkogvAPG1ac2FkRQ_MTfHEhqsV4wCLcBGAsYHQ/s728/PoisonApple%25281%2529.png)

PoisonApple 是一个命令行工具，用于在 macOS 上执行各种持久化机制技术。该工具旨在供威胁猎人用于网络威胁模拟目的。

**安装**

*   **做起来:**

**$ pip3 安装 poison apple–用户**

**注意:** PoisonApple 是用 Python 3.9 编写的&，用 Python 3.6+应该可以

**重要注意事项！**

*   PoisonApple 会修改你的 macOS 系统，建议只在虚拟机上使用 PoisonApple。尽管使用该工具添加的任何持久性机制技术也可以很容易地删除(-r)，**请谨慎使用**！
*   请注意:该工具可能会导致常见的反病毒/ EDR /其他 macOS 安全产品生成警报。
*   要深入了解这些技术是如何工作的，请参阅 Objective-See 的 Patrick Wardle 的[Mac 恶意软件艺术，第 1 卷:分析-第 0x2 章:持久性](https://taomm.org/PDFs/vol1/CH%200x02%20Persistence.pdf)。这是一个奇妙的资源。

**用途**

参见 PoisonApple 开关选项(–帮助):

**$ poison apple–help
用法:poison apple[-h][-l][-t TECHNIQUE][-n NAME][-c COMMAND][-r]** 
**命令行工具，在 macOS 上执行各种持久化机制技术。

可选参数:**
-h，–help 显示此帮助消息并退出
-l，–list 列出可用的持久性机制技术
-t 技术，–TECHNIQUE 技术
要使用的持久性机制技术
-n NAME，–NAME NAME 用于持久性的文件或标签的名称
-c 命令，–COMMAND
要为持久性执行的命令
-r，–remove 删除持久性机制

*   **可用技术列表:**

+——————————————————+
| atjob |
+————————+
| bashrc |
+————————+
| cron |
+—————+
| cron root |
+————

*   **应用持久机制:**

**$ poison apple-t LaunchAgentUser-n 测试
[+]成功！持久性机制操作成功:LaunchAgentUser**

*   如果没有指定命令(-c)，将使用默认的触发器命令，该命令在每次触发持久性机制时写入桌面上的文件:

**$ cat ~/Desktop/poison apple-LaunchAgentUser**
触发@ Tue Mar 23 17:46:02 CDT 2021
触发@ Tue Mar 23 17:46:13 CDT 2021
触发@ Tue Mar 23 17:46:23 CDT 2021
触发@ Tue Mar 23 17:46:33 CDT 2021
触发@ Tue Mar 23

*   **删除持久化机制:**

**$ poison apple-t LaunchAgentUser-n testing-r
……**

*   **使用自定义命令:**

**$ poison apple-t LaunchAgentUser-n foo-c " echo foo>>/Users/user/Desktop/foo "**
**……**