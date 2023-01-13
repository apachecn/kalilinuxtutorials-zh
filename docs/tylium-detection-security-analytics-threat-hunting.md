# Tylium:用于入侵检测、安全分析和威胁追踪的主要数据管道

> 原文：<https://kalilinuxtutorials.com/tylium-detection-security-analytics-threat-hunting/>

[![Tylium : Primary Data Pipelines For Intrusion Detection, Security Analytics & Threat Hunting](img/ea06d8960de8ab1979a579f5e58f192a.png "Tylium : Primary Data Pipelines For Intrusion Detection, Security Analytics & Threat Hunting")](https://1.bp.blogspot.com/-2pgxWdL8eLI/XaVQjZ_P8MI/AAAAAAAAC7Q/Vs7Kb62WxyoyJKz2Am1wu_N_fQ0Xpuh2gCLcBGAsYHQ/s1600/300px-HandofGod.png)

**Tylium** 是用于入侵检测、安全分析和威胁追踪的主要数据管道。这些文件包含用于生成 EDR(端点检测和响应)数据以及标准系统日志的配置。

这些配置使得能够使用 F/OSS(自由和/或开源工具)产生这些数据流。)F/OSS 工具包括 Auditd for LinuxWindows 的 Sysmon 和 Mac 的 Xnumon。还包括一套配置 Suricata 事件和规则的注意事项。

这些数据集列举和/或生成威胁搜寻技术和各种安全分析所需的安全相关事件。

Tylium 是 SpaceCake 项目的一部分，用于在云和传统环境中使用 Linux 和 Windows 的开源工具进行多平台入侵检测、安全分析和威胁搜索。

**也读作-[MalConfScan:Volatility 插件，用于提取已知恶意软件](https://kalilinuxtutorials.com/malconfscan-extracts-configuration-data-malware/)的配置数据**

**内容**

**Linux**

auditd . YAML–一组用于通过 Linux 的 auditd 子系统生成文件、网络和进程事件的 auditd 规则

system logs . MD–Linux 本地操作系统和 web 服务器日志的矩阵

**MacOS**

configuration . plist–在 MacOS 上使用 xnumon 项目生成类似 sysmon 的事件的配置

**苏里卡塔**

云与陆地环境中 Suricata 的事件和规则设置说明

**视窗**

event logs . MD–选择 Windows 事件日志消息及其位置的矩阵

sysmon-config-base . XML–一个 Sysmon 配置文件，用于使用 Sysmon for Windows 生成文件、网络、注册表、网络、进程和 WMI 事件

[**Download**](https://github.com/randomuserid/Tylium)