# DazzleUP:一个检测特权提升漏洞的工具

> 原文：<https://kalilinuxtutorials.com/dazzleup/>

[![DazzleUP : A Tool That Detects The Privilege Escalation Vulnerabilities](img/7d77452eedee1d58adcbe46d07a7758a.png "DazzleUP : A Tool That Detects The Privilege Escalation Vulnerabilities")](https://1.bp.blogspot.com/-8udqVjNokvk/Xywy97wdS6I/AAAAAAAAHOg/IMjcDIwsZM432du0y4rn_Z5EG-Jb1hx-ACLcBGAsYHQ/s728/dazzleUP%25281%2529.png)

**DazzleUP** 是一款工具，用于检测 Windows 操作系统中由于错误配置和缺少更新而导致的权限提升漏洞。dazzleUP 检测以下漏洞。

**漏洞利用检查**

dazzleUP 的第一个特性是，在查找缺失的补丁时，它使用 Windows Update Agent API，而不是 WMI(像其他的一样)。dazzleUP 检查以下漏洞。

*   DCOM/NTLM 映像(腐烂/多汁的土豆)脆弱性
*   CVE-2019-0836
*   CVE-2019-0841
*   CVE-2019-1064
*   CVE-2019-1130
*   CVE-2019-1253
*   CVE-2019-1385
*   CVE-2019-1388
*   CVE-2019-1405
*   CVE-2019-1315
*   CVE-2020-0787
*   CVE-2020-0796

当目标系统是微软当前支持的 Windows 10 操作系统(内部版本 1809、1903、1909 和 2004)时，执行漏洞检查。如果在不支持的操作系统上运行；dazzleUP 将警告您“dazzleUP 不支持目标系统内部版本号，传递缺少的更新控件…”。

**错误配置检查**

dazzleUP 对每个 Windows 操作系统执行以下错误配置检查。

*   始终安装高架
*   凭据管理器中的凭据枚举
*   McAfee 的 SiteList.xml 文件
*   可修改的二进制文件保存为注册表自动运行
*   可修改的注册表自动运行键
*   可修改的服务二进制文件
*   可修改的服务注册表项
*   DLL 劫持的%PATH%值
*   无人值守安装文件
*   未引用的服务路径

**操作使用–1**

您可以直接使用单机版来使用 dazzleUP。EXE 并获得结果。截图如下。

**操作使用–2**

你可以在钴击的信标上使用`dazzleUP.cna`文件直接使用反射 DLL 版本的 dazzleUP。截图如下。了解更多信息；[https://www.cobaltstrike.com/aggressor-script/index.html](https://www.cobaltstrike.com/aggressor-script/index.html)

[**Download**](https://github.com/hlldz/dazzleUP#operational-usage---2)