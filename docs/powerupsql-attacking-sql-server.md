# PowerUpSQL 工具包，用于审核 SQL Server 的弱配置审核、大规模权限提升和利用后攻击

> 原文：<https://kalilinuxtutorials.com/powerupsql-attacking-sql-server/>

**PowerUpSQL** 包括支持 SQL Server 发现、弱配置审计、规模权限提升以及操作系统命令执行等利用后操作的功能。它旨在用于内部渗透测试和红队参与。

但是，PowerUpSQL 还包括许多功能，管理员可以使用这些功能快速清点 ADS 域中的 SQL Server，并执行与 SQL Server 相关的常见威胁搜寻任务。

**也可阅读[Burpsuite——Web 应用安全或渗透测试初学者指南](https://kalilinuxtutorials.com/burpsuite/)**

## **设置 PowerUpSQL**

*   从 PowerShell Gallery 安装它。这需要本地管理权限，并将永久安装该模块。

`**Install-Module -Name PowerUpSQL**`

*   `下载项目并导入。这不需要管理权限，只会导入到当前会话中。但是，它可能会被限制性执行策略阻止。`

 ``**Import-Module PowerUpSQL.psd1**`

*   `通过下载支架将其加载到会话中。这不需要管理权限，只会导入到当前会话中。它不应该被执行策略阻止。`

 ``**IEX(New-Object System.Net.WebClient).DownloadString("https://raw.githubusercontent.com/NetSPI/PowerUpSQL/master/PowerUpSQL.ps1")**`

**注意:**要作为备用域用户运行，请先使用 run as 命令启动 PowerShell。

`**runas /noprofile /netonly /user:domain\user PowerShell.exe**`

## **获取命令帮助**

*   要列出模块中的函数，请键入:`Get-Command -Module PowerUpSQL`
*   要列出某个函数的帮助，请键入:`Get-Help FunctionName`

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/NetSPI/PowerUpSQL)``