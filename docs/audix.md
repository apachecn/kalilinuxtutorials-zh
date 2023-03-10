# Audix:快速配置 Windows 事件的 PowerShell 工具

> 原文：<https://kalilinuxtutorials.com/audix/>

[![Audix : A PowerShell Tool To Quickly Configure Windows Event](img/9cecbed6969e95fab83b873e1dff5a61.png "Audix : A PowerShell Tool To Quickly Configure Windows Event")](https://1.bp.blogspot.com/-Npnsi8AXmDA/XpNZ8lUNulI/AAAAAAAAF5w/tx6yIYqy_hYE0_pUiPo5cnB8vqFmGd_fgCLcBGAsYHQ/s1600/powershell-red%25281%2529.png)

**Audix** 是一款 PowerShell 工具，用于快速配置安全监控的 Windows 事件审计策略。

**注意:**该工具只会更改本地安全策略。如果应用于具有 GPO 设置的主机，最好在组策略默认配置文件中使用相同的设置，以便所有系统获得相同的配置。如果 GPO 配置文件没有更改为符合这些设置，GPO 强制将覆盖它。

它将允许简单配置 Windows 事件审核策略。默认情况下，窗口的审核策略受到限制。这意味着，对于事件响应者、蓝队队员、CISO 以及希望通过使用 Windows 事件日志来监控其环境的人员，必须配置审核策略设置以提供更高级的日志记录。

该实用程序旨在捕获当前的审计策略设置，对其执行备份(如果需要恢复到以前的状态),并应用更高级的审计策略设置以实现更好的检测功能。

此外，它将强制实施审核策略子类别，以确保这些高级设置持续存在。还有一个调整日志大小限制的设置。Audix 将启用的已启用策略设置的一些示例:

*   **事件 ID:** 4698-4702(已创建/更新/禁用计划任务)
*   **事件 ID:** 4688(新流程已创建。)

**运行中**

*   Git 克隆回购

**git 克隆 https://github.com/littl3field/Audix.git**

导航到该文件夹，并在终端中执行该命令。您必须确保您有管理员权限来执行此操作。

**。\Audix.ps1**

**开发**

*   **我将优先添加这些设置**:
    *   增加日志大小限制(完成)
    *   实施审计策略子类别设置(完成)
*   添加还原选项
*   GPO 设置配置

[**Download**](https://github.com/littl3field/Audix)