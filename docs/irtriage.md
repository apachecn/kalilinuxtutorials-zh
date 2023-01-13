# IRTriage:事件响应 Triage–用于取证分析的 Windows 证据收集

> 原文：<https://kalilinuxtutorials.com/irtriage/>

[![IRTriage : Incident Response Triage – Windows Evidence Collection For Forensic Analysis](img/6baff724532bbb0c588b39faa804ac2c.png "IRTriage : Incident Response Triage – Windows Evidence Collection For Forensic Analysis")](https://1.bp.blogspot.com/-RG-xDB1Lla8/YIMpy5P3LaI/AAAAAAAAI0o/Ck5vbQD41jAN91802znUm6D-yog8b9HjgCLcBGAsYHQ/s728/IRTriage.png)

对法医分析师有价值的系统信息的脚本集合。在除 WinXP 之外的所有 Windows 版本中，IRTriage 将自动“以管理员身份运行”。

最初的来源是由 Michael Ahrendt 编写的 Autoit 脚本。不幸的是，迈克尔最后一次修改是在 2012 年 11 月 9 日[发布的](http://mikeahrendt.blogspot.ca/2012/01/automated-triage-utility.html)

我让 Michael [知道](http://mikeahrendt.blogspot.com/2012/01/automated-triage-utility.html?showComment=1455628200788#c6111030418808145121)我已经分叉了他的项目:我很高兴地宣布他祝福我分叉他的源代码，开源万岁！)

**如果在事故中无法使用完整的磁盘映像，该怎么办？**

假设您正在调查十几个或更多可能被感染或受损的系统。你能花 2-8 个小时对这些电脑的硬盘进行取证复制吗？在这种情况下，快速取证“检伤分类”是这种情况的解决方案。收集一些关键文件可以解决这个问题，而不是复制所有内容。

*   **IRTriage 将收集:**
    *   系统信息
    *   网络信息
    *   注册表配置单元
    *   磁盘信息，以及
    *   转储内存。

IRTriage 的强大功能之一是从“卷影拷贝”中收集信息，这可以击败许多反取证技术。

IRTriage 本身只是一个 autoit 脚本，它依赖于其他工具，例如:

*   Win32|64dd(不含 Moonsols)或 FDpro *(HBGary 的商业产品)
*   系统内部套件
*   侦探工具包
*   Regripper
*   NirSoft => MFTDump 和 WinPrefetchView
*   md5deep 和 sha1deep
*   CSV 文件视图
*   7zip
*   和一些 windows 内置命令。

在发生事故的情况下，您希望对“证据机器”进行最小的更改，因此我建议您将 IRTriage 复制到 USB 驱动器，这里唯一的问题是，如果您计划转储内存，USB 驱动器必须大于计算机中安装的物理 ram。

启动 GUI 应用程序后，您可以选择想要收集的信息。每个类别都在单独的选项卡中。所有收集到的信息将被转储到一个标有[主机名-日期-时间]的新文件夹中。

**新闻:triage-ir v0.851 的变化**

*   将项目重命名为 IRTriage
*   版本已更改为 v2。[YY。MM.DD]以便于识别最后的更改。
*   将项目更新为当前可用的工具。
*   修复了“执行的命令”记录错误
*   将“事件日志. txt”更改为“事件日志. csv”(制表符分隔)
*   已将编译时工具文件夹更改为“”。\编译\工具"(本地到脚本)
*   修复了在本地脚本目录中打开 ini 文件的对话框

**版本 2016.02.24 IRTriage 现在真正兼容以下版本的 Windows:**

*   Windows 工作站“WIN_10”、“WIN_81”、“WIN_8”、“WIN_7”、“WIN_VISTA”、“WIN_XP”、“WIN_XPe”，
*   Windows 服务器:“WIN_2016”、“WIN_2012R2”、“WIN_2012”、“WIN_2008R2”、“WIN_2008”、“WIN_2003”。

**2016 . 02 . 26 *版开始增加新功能:**

*** Processes()**
–tcpvcon-ANC-accept EULA>process 2 port map . CSV
–task list/SVC/FO CSV>process 2 exe map . CSV
–wmic/output:Processes cmd . CSV process get Caption，Commandline，Processid，ParentProcessId，session id/format:CSV

*** system info()**
–wmic/output:install list . CSV product 添加了查看采集后事件日志的复选框
–cmd.exe；添加了在采集后打开 IRTriage 命令行的复选框

**版本 2016.03.08**

*   增加了基于 v0.4.0 的 ReactOS 的自定义编译版“cmd.exe”
*   +它现在可以使用 Linux 等效命令:
    *   清除= cls
    *   cp =复制
    *   df =免费
    *   env = set
    *   ln = mklink
    *   ls = dir
    *   mv =移动
    *   pwd = cd，chdir
    *   rm =删除，删除，擦除
    *   睡眠=暂停
    *   uname = ver，版本
    *   vmstat =内存，mem

**版本 2016.03.08**

*   开始清理代码，试图使模块化更容易。
*   增加了编译时使用 HBGary 的 FDpro(商用)或 [Moonsol 的(免费)](http://www.moonsols.com/downloads/1)内存采集软件的选项。
    *   如果你有 HBGary 的 FDpro 把它放在。\Compile\Tools 文件夹代替“零字节”大小的文件，通过将 FDpro.exe 替换为“小于 100 字节”大小的文件，很容易切换回 Moonsol 的内存采集软件:-)

**版本 2016.03.10**

*   继续清理代码，删除了未使用的函数 CommandROSLOG()
*   在 CSV 中添加了$MFT parce
*   增加了采集完成后查看 IncidentLog.csv 的功能。

**版本 2016.03.11**

*   更新的 cmd.exe
*   增加了采集完成后打开 cmd.exe 的能力。

**版本 2016.03.14**

*   向 CSV 添加预取部分

**版本 2016.03.24**

*   在工具菜单中增加了 IRTriage 更新(更新按钮混淆了)

**版本 2016.03.28**

*   修复了 IRTriage 更新(是=下载更新，否=显示更新信息，取消=取消更新)

**版本 2016.03.29**

*   将 Didier Stevens 的新命令 privilege 和 info 整合到 ReactOS 的最新版本 cmd.exe 中。这两个新命令对于法医分析师来说都是无价的。
*   IRTriage 命令处理器的来源。

**版本 2016.03.30**

*   固定卷影复制功能
*   cmd.exe 4.1 版的微小更新

未来的更新\功能将基于此报告:[现场分流开源取证工具箱它们有效吗？](http://www.researchgate.net/profile/Stavros_Shiaeles/publication/236681282_On-scene_Triage_open_source_forensic_tool_chests_Are_they_effective/links/00b4953ac91d0d0086000000.pdf?inViewer=true&pdfJsDownload=true&disableCoverPage=true&origin=publication_detail)