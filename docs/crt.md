# CRT:Azure 的 CrowdStrike 报告工具

> 原文：<https://kalilinuxtutorials.com/crt/>

[![](img/35eed8e5ba10ead31884f9645c405e50.png)](https://blogger.googleusercontent.com/img/a/AVvXsEhD2igjoH8CWeN5YpElrHGEHUhw7D7VXm9Ve1qoYVEMZABkXkkwYDlReQFyIrrbCJlaiV6Vx6D-KjJb01GVAy390675HZAmyg1grj9IY4zCSPjx3Rt_YwKGVXjXzZp4PjEymispebNZ_CbioUjNSaf-MEEXaXQzpKUL9gXLyh6AjR7M0G3pE7tf7G72=s760)

**CRT** 是在 Azure AD/O365 租户中查询以下配置的工具，它可以揭示难以找到的权限和配置设置，以帮助组织保护这些环境。

在线交换(O365):

*   联盟配置
*   联邦信托
*   邮箱上配置的客户端访问设置
*   远程域的邮件转发规则
*   邮箱 SMTP 转发规则
*   邮件传输规则
*   被授予“完全访问”权限的代理人
*   被授予任何权限的委托人
*   具有“代理发送”或“SendOnBehalf”权限的代理
*   启用 Exchange Online PowerShell 的用户
*   启用了“绕过审核”的用户
*   全局地址列表(GAL)中隐藏的邮箱
*   收集管理员审核日志记录配置设置。

Azure 广告:

*   具有 KeyCredentials 的服务主体对象
*   O365 管理组报告
*   委派权限和应用程序权限

查询租户合作伙伴信息:为了查看租户合作伙伴信息，包括分配给合作伙伴的角色，您必须以全局管理员身份登录 Microsoft 365 管理中心:

https://admin.microsoft.com/AdminPortal/Home#/partners

### 先决条件

下列 PowerShell 模块是必需的，将自动安装:

*   ExchangeOnlineManagement
*   AzureAD

**注意**:要返回被查询配置的完整范围，需要以下角色:

*   全局管理

当全局管理权限不可用时，该工具会通知您哪些信息因此对您不可用。

### 用法

未指定参数:*将在运行脚本的目录中自动创建一个名为日期和时间(YYYYDDMMTHHMM)的文件夹。默认身份验证方法将提示每个连接与 MFA 兼容。*

**。\Get-CRTReport.ps1**

`**-BasicAuth**`参数:*[可选]如果没有对您的用户主体实施 MFA，您可以使用该参数，该参数将仅提示一次身份验证，并使用`**Get-Credential**`存储凭证。(不推荐)*

**。\ get-crtre port . PS1-basic**基础]

`**-JobName**`参数:*【可选】使用 JobName 参数区分不同的租户。如果没有指定作业名，日期/时间格式的文件夹将放在工作目录中。*

**。\ Get-CRT report . PS1-job name my job name**

`**-Commands**`参数:*[可选]使用此参数，用引号、逗号或空格分隔指定您想要运行的特定命令。*

**。\ Get-CRT report . PS1-Job name MyJobName-working directory ' C:\ Path \ to \ Job \ Folder '-Commands " command 1，Command2"**

`**-AzureEnvironmentName & -ExchangeEnvironmentName**`参数:*[可选]使用此参数，指定 Azure 或 Exchange 环境名称。使用 tab complete 可以搜索可接受的值。*

**。\ Get-CRT report . PS1-exchange environment name o 365 usgovgcchigh-azure environment name AzureUSGovernment**

可用命令:

**fed config
FedTrust
client access
remote domains
SMTPForward
transport rules
fullaccesgranted
AnyAccessGranted
sendas granted
exo powershell
AuditBypassEnabled
hidden mailbox
key credentials
o365 admingroups
DelegateAppPerms
AdminAuditL**ogConfig

`**-Interactive**`参数:*[可选]根据租户中的数据量，一些命令可能需要很长时间来处理。使用 Interactive 参数，您可以选择在模块运行之前跳过任何特定的命令。*

**。\ Get-CRT report . PS1-Job name my Job name-working directory ' C:\ Path \ to \ Job \ Folder '-Interactive**

[**Download**](https://github.com/CrowdStrike/CRT)