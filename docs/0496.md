# WinPwn:内部 Windows 渗透测试/ AD 安全的自动化

> 原文：<https://kalilinuxtutorials.com/winpwn-windows-penetrationtest-ad-security/>

在过去的许多内部渗透测试中，由于缺少代理支持，我经常遇到现有 Powershell Recon / Exploitation 脚本的问题。为此，我编写了自己的脚本，它具有自动代理识别和集成功能，名为 WinPwn。

该脚本大多基于其他知名的大型攻击性安全 Powershell 项目。我只通过 IEX 下载字符串将它们一个接一个地加载到 RAM 中，并部分自动执行以节省时间。

是的，它不是 C#，可能会被反病毒解决方案标记。例如，Windows Defender 阻止了一些已知的脚本/功能。

**也可阅读-[Psad:入侵检测&使用 IPtables 进行日志分析](https://kalilinuxtutorials.com/psad-detection-analysis-iptables/)**

不同的本地侦察模块、域侦察模块、侦察升级和开发模块。欢迎任何建议、反馈和评论！

只需用“Import-Module”导入模块。\WinPwn_v0.7.ps1 "或 iex (new-object net.webclient)。download string('[https://raw . githubusercontent . com/SecureThisShit/win pwn/master/win pwn _ v 0.7 . PS1](https://raw.githubusercontent.com/SecureThisShit/WinPwn/master/WinPwn_v0.7.ps1)')

导入后可用的功能:

*   `**WinPwn**` - >用简单的问题引导用户通过所有功能/模块。
*   `**Inveigh**` - >在新的控制台窗口中执行攻击([【https://github.com/Kevin-Robertson/Inveigh】](https://github.com/Kevin-Robertson/Inveigh))，之后使用会话管理进行 SMB-Relay 攻击
*   `**sessionGopher**` - >执行 Sessiongopher 并询问参数()
*   `**Mimikatzlocal**` - >执行 Invoke-WCMDump 和 Invoke-Mimikatz([https://github.com/PowerShellMafia/PowerSploit](https://github.com/PowerShellMafia/PowerSploit))
*   `**localreconmodules**` - >收集系统信息，执行 passhunt([https://github.com/Dionach/PassHunt](https://github.com/Dionach/PassHunt))，执行 Get-Computerdetails 和另一个 Windows 权限提升脚本+Winspect([https://github.com/PowerShellMafia/PowerSploit](https://github.com/PowerShellMafia/PowerSploit)，[https://github.com/A-mIn3/WINspect](https://github.com/A-mIn3/WINspect)，[https://github.com/411Hall/JAWS](https://github.com/411Hall/JAWS)
*   `JAWS` - >执行另一个 Windows 权限提升脚本
*   `**domainreconmodules**` - >执行不同的 Powerview 情境感知功能，并将输出存储在磁盘上。此外，DomainpasswordSpray 的用户列表存储在磁盘上。使用 ADRecon 在 CSV 文件(或 XLS，如果安装了 excel)中生成广告报告。([https://github.com/sense-of-security/ADRecon](https://github.com/sense-of-security/ADRecon)，[https://github.com/PowerShellMafia/PowerSploit](https://github.com/PowerShellMafia/PowerSploit)，[https://github.com/dafthack/DomainPasswordSpray](https://github.com/dafthack/DomainPasswordSpray))
*   `**Privescmodules**` - >在内存中执行不同的 privesc 脚本(夏洛克[https://github.com/rasta-mouse/Sherlock](https://github.com/rasta-mouse/Sherlock)，PowerUp，GPP-Files，WCMDump)
*   `**lazagnemodule**` - >下载并执行 lazagne.exe(如果未被 AV 检测到)([https://github.com/AlessandroZ/LaZagne](https://github.com/AlessandroZ/LaZagne))
*   `**latmov**` - >在域中搜索具有管理员访问权限的系统进行横向移动。Mass-Mimikatz 可以在找到系统后使用。这里也可以使用新凭证的域名密码喷射。
*   `**empirelauncher**` - >在远程系统上启动 powershell 帝国在线([https://github.com/EmpireProject/Empire](https://github.com/EmpireProject/Empire))
*   `**shareenumeration**` - >从 Powerview (Powersploit)调用-文件查找器和调用-共享查找器
*   `**groupsearch**`**->Get-domainpouserlocalgroupmapping–通过组策略映射(Powerview / Powersploit)查找您拥有管理员访问权限或 RDP 访问权限的系统**
*   **`**Kerberoasting**` - >在一个新窗口中执行 Invoke-Kerberos ast 并存储哈希以备以后破解**
*   **`**isadmin**` - >检查本地系统上的本地管理员访问权限**
*   **`**Sharphound**` - >下载 Sharphound 并为 Bloodhound DB 收集信息**
*   **`**adidnswildcard**` - >创建集成 Active Directory 的 DNS 通配符记录，运行 Inveigh 进行海量哈希收集。([https://blog.netspi.com/exploiting-adidns/#wildcard](https://blog.netspi.com/exploiting-adidns/#wildcard)**

 **“obejhzxyarrq . exe”-可执行文件是 jaredhaights PSAttack 工具的混淆版本，用于 app locker/PS-Restriction Bypass([https://github.com/jaredhaight/PSAttack](https://github.com/jaredhaight/PSAttack))。

**待办事项:**

*   从我自己的 creds 存储库中获取脚本([https://github.com/SecureThisShit/Creds](https://github.com/SecureThisShit/Creds))，使其独立于原始存储库中的更改。
*   目前无法正确找到通过 PAC-File 的代理选项
*   混淆所有反病毒脚本

**免责声明**

未经双方事先同意，使用 WinPwn 攻击目标是非法的。最终用户有责任遵守所有适用的地方、州和联邦法律。开发人员不承担任何责任，也不对本程序造成的任何误用或损坏负责。仅用于教育目的。

[**Download**](https://github.com/SecureThisShit/WinPwn)**