# 数字取证实验室:面向学生和教师的免费动手数字取证实验室

> 原文：<https://kalilinuxtutorials.com/digital-forensics-lab/>

[![](img/0ed39e1003b96c3229b4808c726b9514.png)](https://blogger.googleusercontent.com/img/a/AVvXsEgrM4ZYFJUt6-T0C_QOi1Ar-msjM4hfrLqmW7-w4s-5NAX4zAToB90YDxY0lU-DGCSI-bZeE2yVDIHiVXn6cLeX4RksXssZv56Xib_Wkg4i2s44K3optYWubN1V55QVvM8AjHTyRuyMONaI6FIcxYmkeoAmjm9vKXZ_BPFUP9SpicGBU1CCvJvC-GGw=s946)

**数字取证实验室**是一个面向学生和教师的免费动手数字取证实验室。

**储存库的特征**

*   动手数字取证实验室:专为学生和教师设计
*   基于 Linux 的实验室:所有实验室都完全基于 Kali Linux
*   实验截图:每个实验都有带说明截图的 PPT
*   全面:涵盖数字取证中的许多主题
*   免费:所有工具都是开源的
*   更新:该项目由 DOJ 资助，将不断更新
*   基于案例研究的 JSON 文件中的两种形式化取证情报

**工具安装(2021 年 12 月 6 日新增)**

**方法一:导入定制的 Kali VM 镜像**

定制的 Kali VM = Kali (2020.4) +工具，用于完成上面列出的大多数实验(p2p 数据泄漏案例除外)

*   安装 Virtualbox
*   导入定制的 Kali 2020.4。注意:默认硬盘大小为 80G。

**方法二:使用定制脚本安装工具(该脚本仅在 Kali 2020.4 上测试)**

以下脚本将安装完成上面列出的大部分实验所需的工具(p2p 数据泄漏案例除外，该案例在 PPT 中有自己的脚本描述)。如果您需要我们在脚本中添加更多工具，请告诉我们。

*   安装 Virtualbox
*   安装 Kali 2020.4。注意:建议您将 Kali VM 的磁盘大小配置为 80G，因为每个泄漏案例映像的大小为 30G+
*   如何运行安装脚本的说明，或者您可以简单地按照下面的命令

**wget https://raw . githubusercontent . com/frank wxu/digital-forensics-lab/main/Help/tool-install-zsh . sh
chmod+x tool-install-zsh . sh
。/tool-install-zsh.sh**

安装的工具。请注意，工具的大多数命令都可以全局执行。现在，您可以跳过 PPT 中的大多数工具安装步骤。

**调查 NIST 数据泄露**

案例研究是调查一个涉及知识产权盗窃的图像。这项研究包括

*   由 NIST 创建的大型复杂案例研究。您可以访问场景，DD/Encase 图像。你也可以在他们的网站上找到解决方案。
*   数字取证中的 14 个动手实验/主题

**涵盖的主题**

| 实验室 | 涵盖的主题 | pps 的大小 |
| --- | --- | --- |
| 实验室 0 | 环境设置 | 2M |
| 实验 1 | Windows 注册表 | 3M |
| 实验 2 | Windows 事件和 XML | 3M |
| 实验三 | Web 历史和 SQL | 3M |
| 实验 4 | 电子邮件调查 | 3M |
| 实验室 5 | 文件更改历史和 USN 日志 | 2M |
| 实验 6 | 网络证据和皮包 | 2M |
| 实验室 7 | 网络驱动器和云 | 5M |
| 实验室 8 | 主文件表($ term)和日志文件($logFile)分析 | 13 米 |
| 实验室 9 | Windows 搜索历史记录 | 4M |
| 实验室 10 | Windows 卷影副本分析 | 6M |
| 实验室 11 | 回收站和反取证 | 3M |
| 实验室 12 | 数据雕刻 | 3M |
| 实验室 13 | 破解 Windows 密码 | 2M |

* * *

**调查 P2P 数据泄露**

P2P 数据泄露案例研究旨在帮助学生应用各种取证技术来调查涉及 P2P 的知识产权盗窃。这项研究包括

*   一个大而复杂的案件，涉及到一个未被雇佣的客户。这个案例类似于 NIST 数据泄露实验室。然而，它提供了一个更清晰、更详细的时间表。
*   有解释的确凿证据。与每项活动相关的每项证据都将随时间表一起解释。
*   数字取证中的 10 个动手实验/主题

**涵盖的主题**

| 实验室 | 涵盖的主题 | pps 的大小 |
| --- | --- | --- |
| 实验室 0 | 实验室环境设置 | 4M |
| 实验 1 | 磁盘映像和分区 | 5M |
| 实验 2 | Windows 注册表和文件目录 | 15 米 |
| 实验三 | MFT 时间表 | 6M |
| 实验 4 | USN 期刊时间线 | 3M |
| 实验室 5 | 自动日志文件 | 9M |
| 实验 6 | 文件签名 | 8M |
| 实验室 7 | 电子邮件 | 9M |
| 实验室 8 | Web 历史记录 | 11 米 |
| 实验室 9 | 网站分析 | 2M |
| 实验室 10 | 时间表(摘要) | 13K |

* * *

**调查非法占有图像**

本案例研究旨在调查非法持有犀牛图像的行为。这张图片由 Golden G. Richard III 博士提供，最初用于 DFRWS 2005 年牛仔竞技挑战赛。NIST 托管 USB DD 镜像。存储库中也有该图像的副本。

**涵盖的主题**

| 实验室 | 涵盖的主题 | pps 的大小 |
| --- | --- | --- |
| 实验室 0 | 使用 Wireshark 的 HTTP 分析(文本) | 3M |
| 实验 1 | 使用 Wireshark 进行 HTTP 分析(图片) | 6M |
| 实验 2 | Rhion 占有调查 1:文件恢复 | 9M |
| 实验三 | Rhion 持有调查 2:隐写术 | 4M |
| 实验 4 | Rhion 占有调查 3:从 FTP 流量中提取证据 | 3M |
| 实验室 5 | Rhion 占有调查 4:从 HTTP 流量中提取证据 | 5M |

**调查邮件骚扰**

案例研究是调查一名学生发给一名教员的骚扰邮件。本案由 digitalcorpora.org 主持。你可以从他们的网站获取 senario 的描述和网络流量。该存储库仅提供实验说明。

**涵盖的主题**

| 实验室 | 涵盖的主题 | pps 的大小 |
| --- | --- | --- |
| 实验室 0 | 使用 Wireshark 调查骚扰电子邮件 | 3M |
| 实验 1 | 鲨鱼法医游戏攻略 | 2M |
| 实验 2 | 使用 t-shark 调查骚扰电子邮件 | 2M |

**调查非法文件转移**

案例研究是调查计算机内存，以重建一个时间表的非法数据转移。该案例包括将敏感文件从服务器传输到 USB 的场景。

**涵盖的主题**

| 实验室 | 涵盖的主题 | pps 的大小 |
| --- | --- | --- |
| 实验室 0 | 记忆取证 | 11 米 |
| 第一部分 | 了解嫌疑人和账户 |  |
| 第二部分 | 了解嫌疑人的电脑 |  |
| 第三部分 | 网络取证 |  |
| 第四部分 | 调查命令历史 |  |
| 第五部分 | 调查嫌疑人的 USB |  |
| 第六部分 | 调查 Internet Explorer 历史记录 |  |
| 第七部分 | 调查文件浏览器历史记录 |  |
| 第八部分 | 时间轴分析 |  |

**调查窃听案**

案例研究，包括 NIST 提供的磁盘图像，是为了调查一个在无线接入点范围内拦截互联网流量的黑客。

**涵盖的主题**

| 实验室 | 涵盖的主题 | pps 的大小 |
| --- | --- | --- |
| 实验室 0 | 黑客案件 | 8M |

**调查 Android 10**

该图片由约书亚·希克曼创作，由数字语料库托管。

| 实验室 | 涵盖的主题 | PPT 的大小 |
| --- | --- | --- |
| 实验室 0 | 介绍像素 3 | 3M |
| 实验 1 | 像素 3 图像 | 2M |
| 实验 2 | 像素 3 设备 | 4M |
| 实验三 | 像素 3 系统设置 | 5M |
| 实验 4 | 概述:应用生命周期 | 11 米 |
| 实验 5.1.1 | AOSP 应用调查:消息传递 | 4M |
| 实验 5.1.2 | AOSP 应用程序调查:联系人 | 3M |
| 实验 5.1.3 | AOSP 应用调查:日历 | 1M |
| 实验 5.2.1 | GMS 应用调查:消息传递 | 6M |
| 实验 5.2.2 | GMS 应用调查:拨号器 | 2M |
| 实验 5.2.3 | GMS 应用程序调查:地图 | 8M |
| 实验 5.2.4 | GMS 应用程序调查:照片 | 6M |
| 实验 5.3.1 | 第三方应用调查:Kik | 4M |
| 实验 5.3.2 | 第三方应用调查:textnow | 1M |
| 实验 5.3.3 | 第三方应用调查:whatsapp | 3M |
| 实验 6 | 像素 3 生根 | 5M |

**调查无人机 DJI**

数据集包括从 DJI 控制器(移动设备)提取的逻辑文件和设备使用的 SD 卡映像。无人机数据集由 VTO 实验室创建。实验室包括 GPS 调查和缓存图像检索。注意是草稿。我们稍后将改进实验室。

| 实验室 | 涵盖的主题 | pps 的大小 |
| --- | --- | --- |
| 实验室 0 | DJI 马维克航空移动公司 | 13 米 |
| 实验 1 | DJI Mavic Air MicroSD Raw | 2M |
| 实验 2 | DJI Mavic Air MicroSD 封装 | 2M |

**工具**

*   测试的命令

| 名字 | 命令 | 贮藏室ˌ仓库 | 安装方法 |
| --- | --- | --- | --- |
| 葡萄酒 | 葡萄酒-版本 | https://source.winehq.org/git/wine.git/ | 习俗 |
| 维尼托 | 维内托-h | https://github.com/AtesComp/Vinetto | 习俗 |
| imgclip | imgclip -h | https://github.com/Arthelon/imgclip | 易于安装 |
| RegRipper | rip.pl -h | https://github.com/keydet89/RegRipper3.0 | 自定义剪贴画 |
| 窗口预取分析器 | 预取. py -h | https://github.com/PoorBillionaire/Windows-Prefetch-Parser.git | 习俗 |
| python-evtx | evtx_dump.py -h | https://github.com/williballenthin/python-evtx | 易于安装 |
| libesedb-utils | esedbexport -h | https://github.com/libyal/libesedb | 易于安装 |
| libpff | pffexport -h | https://github.com/libyal/libpff | 易于安装 |
| USN-Record-Carver | usncarve.py -h | https://github.com/PoorBillionaire/USN-Record-Carver | 易于安装 |
| USN-日志-解析器 | 美国海军陆战队 | https://github.com/PoorBillionaire/USN-Journal-Parser | 易于安装 |
| 时间解码 | time_decode.py -h | https://github.com/digitalsleuth/time_decode | Git clone |
| 分析 | 分析工具 | https://github.com/dkovar/analyzeMFT | 自定义剪贴画 |
| libvshadow | vshadowinfo 信息-h | https://github.com/libyal/libvshadow | 自定义剪贴画 |
| INDXParse | indx per . py-- |  | 自定义剪贴画 |
| 雕刻 sqlite。 | undark -h | https://github.com/inflex/undark.git | 自定义剪贴画 |
| 隐写检测 | 隐写检测-V |  | 自定义剪贴画 |
| 隐写破解 | stegbreak -V |  | 自定义剪贴画 |
| 隐写工具包 | jphide |  | 自定义剪贴画 |
| jpsestego-toolkitek | jpseek |  | 自定义剪贴画 |
| 挥发性-2 | 第一卷 | https://github.com/volatilityfoundation/volatility.git | 自定义剪贴画 |
| liblnk-utils | lnkinfo -h |  | 易于安装 |
| JLECmd |  | https://f001.backblazeb2.com/file/EricZimmermanTools/JLECmd.zip | Git clone |
| recentfilecache 剖析器 |  | https://github.com/prolsen/recentfilecache-parser |  |
| LogFileParser |  | https://github.com/jschicht/LogFileParser.git | Git clone |
| UsnJrnl2Csv |  | ttps://github . com/jschicht/usnjrnl 2 CSV . git | Git clone |

*   通过 apt 安装的其他工具有 python3-pip、leafpad、terminator、sqlite3、tree、xmlstarlet、libhivex-bin、pasco、libhivex-bin、npm、binwalk、foremost、hashdeep、ewf-tools、nautilus

[**Download**](https://github.com/frankwxu/digital-forensics-lab)