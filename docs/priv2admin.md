# Priv2Admin:允许您(错误)使用 Windows 权限的利用途径

> 原文：<https://kalilinuxtutorials.com/priv2admin/>

[![Priv2Admin : Exploitation Paths Allowing You To (Mis)Use The Windows Privileges](img/19b76a1b9088a64fc8c5e7fe82096736.png "Priv2Admin : Exploitation Paths Allowing You To (Mis)Use The Windows Privileges")](https://1.bp.blogspot.com/-rVCavuNnZyM/YKLCPpoI-YI/AAAAAAAAJHU/OpLA9bwWkCYikXnGnPdVAUfT6VvzBrX8QCLcBGAsYHQ/s728/win_hack%25281%2529.png)

**Priv2Admin** 的想法是将 Windows 操作系统权限“转换”到一个路径，该路径导致:

*   管理员，
*   完整性和/或机密性威胁，
*   可用性威胁，
*   只是一团糟。

在以下位置列出并解释了特权:[https://docs . Microsoft . com/en-us/windows/win32/sec authz/privilege-constants](https://docs.microsoft.com/en-us/windows/win32/secauthz/privilege-constants)

如果目标可以通过多种方式实现，那么优先考虑的是

*   使用内置命令
*   使用 PowerShell(仅当存在工作脚本时)
*   使用非操作系统工具
*   使用任何其他方法

可以用`whoami /priv`查看自己的权限。禁用的特权和启用的一样好。唯一重要的事情是你是否拥有列表中的特权。

**注 1:** 每当攻击路径以令牌创建结束时，您可以假设下一步是使用此类令牌创建新进程，然后控制操作系统。

**注 2:**
**a.** 直接调用`NtQuerySystemInformation()` / `ZwQuerySystemInformation()`，可以在这里找到需要的权限[。
**b.** 对于`NtSetSystemInformation()` / `ZwSetSystemInformation()`所需的权限在这里列出](https://github.com/gtworek/Priv2Admin/blob/master/NtQuerySystemInformation.md)[在这里](https://github.com/gtworek/Priv2Admin/blob/master/NtSetSystemInformation.md)。

注 3: 我只关注操作系统。如果一个特权在 AD 中有效，但在 OS 本身中无效，我将它描述为 OS 中没有使用。如果有人深入挖掘面向广告的场景就好了。

请随意贡献和/或讨论提出的想法。

| 特权 | 影响 | 工具 | 执行通路 | 评论 |
| --- | --- | --- | --- | --- |
| `**SeAssignPrimaryToken**` | ***管理员*** | 第三方工具 | *“它将允许用户使用诸如 potato.exe、juicypotato.exe 和 juicypotato.exe 等工具假冒令牌和权限进入 nt 系统”* | 感谢 Aurélien Chalot 的更新。我会尽快尝试用更像菜谱的方式来表达。 |
| `**SeAudit**` | **威胁** | 第三方工具 | 将事件写入安全事件日志，以欺骗审核或覆盖旧事件。 | 使用 [`**Authz Report Security** **Event**`](https://docs.microsoft.com/en-us/windows/win32/api/authz/nf-authz-authzreportsecurityevent) API 可以编写自己的事件。 |
| `**SeBackup**` | ***管理员*** | 第三方工具 | 1.备份 **`HKLM\SAM`** 和`**HKLM\SYSTEM**`注册表配置单元
2。从`**SAM**`数据库
3 中提取本地账户哈希值。作为本地`**Administrators**`组

的成员，Pass-the-Hash 也可以用来读取敏感文件。 | 更多信息，请参考 **[`SeBackupPrivilege`文件](https://github.com/gtworek/Priv2Admin/blob/master/SeBackupPrivilege.md)。** |
| `**SeChangeNotify**` | 没有人 | – | – | 每个人都拥有的特权。撤销它可能会使操作系统(Windows Server 2019)无法启动。 |
| `**SeCreateGlobal**` | ？ | ？ | ？ |  |
| `**SeCreatePagefile**` | 没有人 | ***内置命令*** | 创建 hiberfil.sys，离线读取，查找敏感数据。 | 需要脱机访问，这无论如何都会导致管理员权限。 |
| `**SeCreatePermanent**` | ？ | ？ | ？ |  |
| `**SeCreateSymbolicLink**` | ？ | ？ | ？ |  |
| `**SeCreateToken**` | ***管理员*** | 第三方工具 | 使用 **`NtCreateToken`创建包含本地管理员权限的任意令牌。** |  |
| `**SeDebug**` | ***管理员*** | **PowerShell** | 复制`**lsass.exe**`令牌。 | 在 [FuzzySecurity](https://github.com/FuzzySecurity/PowerShell-Suite/blob/master/Conjure-LSASS.ps1) 找到的脚本 |
| 【T2`SeDelegateSession-`
`UserImpersonate` | ？ | ？ | ？ | 特权名称被破坏以缩小列。 |
| `**SeEnableDelegation**` | 没有人 | – | – | Windows 操作系统中不使用该权限。 |
| `**SeImpersonate**` | ***管理员*** | 第三方工具 | 来自*土豆家族* (potato.exe、rottenpotato.exe 和 juicypotato.exe)、RogueWinRM 等的工具。 | 类似于 **`SeAssignPrimaryToken`，**通过设计允许在另一个用户的安全上下文下创建一个进程(使用所述用户的令牌的句柄)。

可以使用多种工具和技术来获得所需的令牌。 |
| `**SeIncreaseBasePriority**` | 有效性 | ***内置命令*** | `**start /realtime SomeCpuIntensiveApp.exe**` | 在服务器上可能更有趣。 |
| `**SeIncreaseQuota**` | 有效性 | 第三方工具 | 将 cpu、内存和缓存限制更改为某些值，使操作系统无法启动。 | –在安全模式下不检查配额，这使得修复相对容易。
–相同的权限用于管理注册中心配额。 |
| `**SeIncreaseWorkingSet**` | 没有人 | – | – | 每个人都拥有的特权。调用微调内存管理函数时检查。 |
| `**SeLoadDriver**` | ***管理员*** | 第三方工具 | 1.加载有 bug 的内核驱动比如`**szkg64.sys**`
2。利用驱动程序漏洞

或者，可以使用特权通过 **`ftlMC`** 内置命令卸载安全相关的驱动程序。即:`**fltMC sysmondrv**` | 1.该`**szkg64**`漏洞被列为 [CVE-2018-15732](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-15732)
2。`**szkg64**` [漏洞利用代码](https://www.greyhathacker.net/?p=1025)由[帕尔韦兹·安瓦尔](https://twitter.com/parvezghh)创建 |
| `**SeLockMemory**` | 有效性 | 第三方工具 | 通过移动页面来饥饿系统内存分区。 | PoC 发布者[瓦利德·阿萨(@瓦利德·阿萨)](https://twitter.com/waleedassar/status/1296689615139676160) |
| `**SeMachineAccount**` | 没有人 | – | – | Windows 操作系统中不使用该权限。 |
| `**SeManageVolume**` | ***管理员*** | 第三方工具 | 1.启用令牌
2 中的特权。创建句柄到\。\C:用`**SYNCHRONIZE &#124; FILE_TRAVERSE**`
3。发送`**FSCTL_SD_GLOBAL_CHANGE**`将`**S-1-5-32-544**`替换为`**S-1-5-32-545**`
4。覆盖 utilman.exe 等。 | `**FSCTL_SD_GLOBAL_CHANGE**`可以用这段[代码](https://github.com/gtworek/PSBits/blob/master/Misc/FSCTL_SD_GLOBAL_CHANGE.c)制作。 |
| `**SeProfileSingleProcess**` | 没有人 | – | – | 在改变预取、超取和 ReadyBoost 的参数之前(并且在非常有限的一组命令中，在查询之前),检查特权。这种影响可能会有所调整，因为真正的影响还不知道。 |
| `**SeRelabel**` | **威胁** | 第三方工具 | 合法管理员对系统文件的修改？ | 参见: [MIC 文档](https://docs.microsoft.com/en-us/windows/win32/secauthz/mandatory-integrity-control)

完整性标签很少使用，仅在标准 ACL 上工作。两个主要的场景包括:
–防止使用可利用的应用程序(如浏览器、PDF 阅读器等)进行攻击。
–操作系统文件的保护。使用 SeRelabel 的攻击必须遵守由 ACL 定义的访问规则，这使得它们在实践中用处很小。 |
| `**SeRemoteShutdown**` | 有效性 | ***内置命令*** | `**shutdown /s /f /m \\server1 /d P:5:19**` | 当关机/重启请求来自网络时，特权被验证。127.0.0.1 待调查的情景。 |
| `**SeReserveProcessor**` | 没有人 | – | – | 看起来这个特权不再被使用，它只出现在 winnt.h 的几个版本中。你可以在微软发布的源代码中看到它。 |
| `**SeRestore**` | ***管理员*** | **PowerShell** | 1.使用 SeRestore 特权启动 PowerShell/ISE。
2。使用[Enable-SeRestorePrivilege](https://github.com/gtworek/PSBits/blob/master/Misc/EnableSeRestorePrivilege.ps1)启用权限。
3。将 utilman.old 改名为 utilman.old
4。将 cmd.exe 改名为 utilman.exe
5。锁定控制台，然后按 Win+U | 一些反病毒软件可能会检测到攻击。

替代方法依赖于使用相同的权限替换存储在“程序文件”中的服务二进制文件。 |
| `**SeSecurity**` | **威胁** | ***内置命令*** | –清除安全事件日志:**`wevtutil cl Security`**

–将安全日志缩小到 20MB，让事件尽快刷新:`**wevtutil sl Security /ms:0**`

–读取安全事件日志，了解系统内其他用户的进程、访问和动作。

——知道在雷达下做什么。

–了解记录了哪些事件，以生成大量有效清除旧事件的事件，而不会留下明显的清除证据。 |  |
| `**SeShutdown**` | 有效性 | ***内置命令*** | `**shutdown.exe /s /f /t 1**` | 允许调用大多数 NtPowerInformation()级别。有待调查。 |
| `**SeSyncAgent**` | 没有人 | – | – | Windows 操作系统中不使用该权限。 |
| `**SeSystemEnvironment**` | *未知* | 第三方工具 | 该权限允许使用 **`NtSetSystemEnvironmentValue`、`NtModifyDriverEntry`** 和其他一些系统调用来操作 UEFI 变量。 | –固件环境变量过去常用于非 Intel 平台，现在慢慢回归 UEFI 世界。这个地区没有任何文件记录。
–潜力可能很大(即破坏安全引导)，但提高影响级别至少需要概念验证。 |
| `**SeSystemProfile**` | ？ | ？ | ？ |  |
| `**SeSystemtime**` | **威胁** | ***内置命令*** | 【T2`cmd.exe /c date 01-01-01`
`cmd.exe /c time 00:00` | 该权限允许更改系统时间，这可能会导致审计跟踪完整性问题，因为事件将以错误的日期/时间存储。
–注意日期/时间格式。如果不确定，请使用始终安全的值。
–有时特权的名称使用大写字母“T”，称为 **`SeSystemTime`。** |
| `**SeTakeOwnership**` | ***管理员*** | ***内置命令*** | 1. **`takeown.exe /f "%windir%\system32"`**
2。`**icalcs.exe "%windir%\system32" /grant "%username%":F**`
3。将 cmd.exe 改名为 utilman.exe
4。锁定控制台，然后按 Win+U | 一些反病毒软件可能会检测到攻击。

替代方法依赖于使用相同的权限替换存储在“程序文件”中的服务二进制文件。 |
| `**SeTcb**` | ***管理员*** | 第三方工具 | 操作令牌以包含本地管理员权限。 | 示例代码+exe 创建可在 [PsBits](https://github.com/gtworek/PSBits/tree/master/VirtualAccounts) 找到的任意令牌。 |
| `**SeTimeZone**` | 混乱 | ***内置命令*** | 更改时区**。`tzutil /s "Chatham Islands Standard Time"`** |  |
| `**SeTrustedCredManAccess**` | ？ | ？ | ？ |  |
| `**SeUndock**` | 没有人 | – | – | 该权限在移除时启用，但从未观察到它被选中以授予/拒绝访问权限。在实践中，这意味着它实际上是未使用的，不会导致任何升级。 |
| `**SeUnsolicitedInput**` | 没有人 | – | – | Windows 操作系统中不使用该权限。 |

[**Download**](https://github.com/gtworek/Priv2Admin)