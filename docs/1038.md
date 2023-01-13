# CAINE 11–GNU/Linux 实时发行版

> 原文：<https://kalilinuxtutorials.com/caine-gnu-linux-live-distribution/>

[![CAINE 11 – GNU/Linux Live Distribution](img/7f1ece10bf369e6255588baaa7303162.png "CAINE 11 – GNU/Linux Live Distribution")](https://1.bp.blogspot.com/-OcCS68iZGKw/Xe919pyilcI/AAAAAAAAD4Y/YNcHJBinLvkKa_am6JKzR6zjTOwGrRBHwCLcBGAsYHQ/s1600/caine.png)

CAINE(计算机辅助调查环境)是一个意大利 GNU/Linux 实时发行版，作为一个数字取证项目而创建。目前，项目经理是 Nanni Bassetti(意大利巴里)。

它提供了一个完整的取证环境，该环境被组织成将现有的软件工具集成为软件模块，并提供一个友好的图形界面。

CAINE 旨在保证的主要设计目标如下:

*   在数字化调查的四个阶段支持数字化调查员的互操作环境
*   用户友好的图形界面
*   用户友好的工具

CAINE 充分代表了开源哲学的精神，因为这个项目是完全开放的，每个人都可以继承以前的开发者或项目经理的遗产。

该发行版是开源的，Windows 端是免费的，最后但同样重要的是，该发行版是可安装的，因此有机会在一个新的品牌版本中重建它。

重要的消息是 CAINE 11.0 以只读模式阻止所有块设备(例如/dev/sda)。你可以在 CAINE 的桌面上使用一个名为 BlockON/OFF 的 GUI 工具。

这种新的写入阻止方法确保所有磁盘都不会被意外写入，因为它们以只读模式锁定。

*   如果您需要写入磁盘，您可以使用 BlockOn/Off 或使用“Mounter”在可写模式下更改策略来解锁它。
*   凯恩在启动时总是更快。
*   CAINE 11.0 可以引导到 RAM (toram)。

**也可阅读-[反垃圾邮件:检测一次性电子邮件地址](https://kalilinuxtutorials.com/antidisposmail-detecting-disposable-email-addresses/)**

**重要特性变化**

*   默认情况下，所有设备都在只读模式下被阻止。
*   新工具，新 OSINT，尸检 4.13 板载，APFS 就绪，BTRFS 法医工具，NVME 固态硬盘驱动程序就绪！
*   SSH 服务器默认禁用(参见[手册](https://www.caine-live.net/page8.html)页启用)。
*   SCRCPY–筛选您的 android 设备
*   解剖 4.13 +麦金农的附加插件。
*   X11VNC 服务器–远程控制 CAINE。
*   哈希卡特
*   新脚本(取证工具–分析菜单)
*   automatc——Mac 的取证工具。
*   bitlocker–易失性插件
*   自动时间线–从易失性内存转储中自动提取取证时间线。
*   固件分析器。
*   CDQR–冷盘快速响应工具
*   许多其他修复和软件更新。

[**Download**](https://www.caine-live.net/page5/page5.html)