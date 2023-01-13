# 沙盒扫描器:从公共沙盒爆炸输出中产生威胁搜索和情报数据的工具

> 原文：<https://kalilinuxtutorials.com/sandbox-scryer/>

[![](img/d32ca27d23c9a759ceb7fe529e7d2b1b.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiqH6ee5sdShgGvfWuJtC1ceX72DwY_MEgh_KM2s5nw6JXEEhFc5fhCxHWd9bs-j_3AMfQ8cXEFGf_lfC0pvLwLAicpF8uuqewzL6eigqYVJyQauo8SR8g4gQxGFhkcpL9GwE_X6YkfvYMniffDffDD6BZv9jt6OrS119-vLv3NnxKUehBLi-GqY4DO/s728/Sandbox_Scryer.png)

**沙盒扫描器**是一款开源工具，用于从公共沙盒引爆输出中产生威胁追踪和情报数据。该工具利用米特 ATT & CK 框架来组织和优先化发现，协助 IOC 的组装，理解攻击运动和威胁追踪。通过允许研究人员向沙盒发送数千个样本来构建可用于 ATT & CK 技术的配置文件，沙盒扫描器提供了前所未有的大规模解决用例的能力。

该工具面向对利用沙盒输出数据进行威胁追踪和攻击分析感兴趣的网络安全专业人员。Sandbox Scryer 工具目前使用免费和公开的混合分析恶意软件分析服务的输出，帮助分析师加快和扩大威胁搜索。

## 存储库内容

【根】**版本**。txt–当前工具版本许可证–定义源代码和其他内容的许可证 readme . MD–此文件

[root \ bin]\ Linux–为在 Linux 中运行工具预先构建二进制文件。目前支持:Ubuntu x64 \ MacOS 在 MacOS 中运行工具的预编译二进制文件。目前支持:OSX 10.15 x64 \ Windows-在 Windows 中运行工具的预构建二进制文件。目前支持:Win10 x64

[root \ Presentation _ Video]Sandbox _ Scryer _ _ black hat _ Presentation _ and _ demo . MP4–视频浏览幻灯片并展示工具演示

[root \截图 _ 和 _ 视频]各种后台截图

[根\脚本] Parse_report_set。*–Windows PowerShell 和 DOS 命令窗口批处理文件脚本，这些脚本调用工具来解析测试集 Collate_Results 中的每个 HA 沙盒报告摘要。*–Windows PowerShell 和 DOS 命令窗口批处理文件脚本，这些脚本调用工具来整理来自分析报告摘要的数据，并生成 MITRE Navigator 层文件

[root \ slides]Black Hat _ Arsenal _ 2022 _ _ Sandbox _ SCR yer _ _ BH _ template . pdf–用于在 Black Hat 2022 上展示沙盒播放器的幻灯片的 PDF 导出

[root \ src]Sandbox _ Scryer–包含 Sandbox Scryer 工具(在 c#中)和 Visual Studio 2019 解决方案文件的源的文件夹

[root\test_data] (SHA256 文件名)。JSON–从提交到混合分析的报告摘要-企业攻击 __ 062322 . JSON–MITRE CTI 数据到攻击技术 _ _ 高 _ _ 060922 . JSON–使用 MITRE 计算器生成的顶级 MITRE ATT 和 ck 技术。用于对在 MITRE Navigator 中生成热图的技术进行排名

[root \ test _ output](SHA256)_ report _ _ summary _ Error _ log . txt–解析包含在名称中的 SHA256 的报告摘要时遇到的错误(如果有)_ report _ _ summary _ Hits _ _ Complete _ list . png–显示解析包含在名称中的 SHA256 的报告摘要时注意到的技术的图形(SHA 256)_ report _ _ summary _ MITRE _ Attck _ Hits . CSV–用于从解析包含在名称中的 sha 256 的报告摘要中选择元数据的整理步骤、技术和策略(shacsv 文件。包括著名技术的排名数据

\ collated _ data collated _ 080122 _ MITRE _ Attck _ heat map . JSON–导入到 MITRE Navigator 的图层文件

## 操作

沙盒编辑器旨在作为命令行工具被调用，以方便脚本编写

操作包括两个步骤:

*   解析，解析指定的报告摘要以提取前面提到的输出
*   校对，其中来自解析步骤的一组解析结果的数据被校对以产生导航层文件

无效示例:

*   从语法上分析
*   校对

如果指定了参数“-h”，将显示内置帮助，如下所示

```
        Options:
           -h  Display command-line options
           -i  Input filepath
           -ita  Input filepath - MITRE report for top techniques
           -o  Output folder path
           -ft Type of file to submit
           -name Name to use with output
           -sb_name Identifier of sandbox to use  (default:  ha)
           -api_key API key to use with submission to sandbox
           -env_id Environment ID to use with submission to sandbox
           -inc_sub Include sub-techniques in graphical output  (default is to not include)
           -mitre_data Filepath for mitre cti data to parse (to populate att&ck techniques)
           -cmd  Command
                 Options:
                    parse  Process report file from prior sandbox submission
                           Uses -i, -ita, -o, -name, -inc_sub, -sig_data   parameters
                    col    Collates report data from prior sandbox submissions
                           Uses -i (treated as folder path), -ita, -o, -name, -inc_sub, -mitre_data   parameters

```

一旦生成导航器层文件，可以通过[https://mitre-attack.github.io/attack-navigator/](https://mitre-attack.github.io/attack-navigator/)将其加载到导航器中进行查看

在导航器中，沙盒报告摘要中记录的技术会突出显示，并根据技术排名的综合得分和沙盒报告摘要中技术的命中计数以更高的热度显示。然而，技术将显示选择元数据。

[Click Here To Download](https://github.com/PayloadSecurity/Sandbox_Scryer)