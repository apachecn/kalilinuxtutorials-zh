# MeterPwrShell:生成完美 Powershell 负载的自动化工具

> 原文：<https://kalilinuxtutorials.com/meterpwrshell/>

[![MeterPwrShell : Automated Tool That Generate The Perfect Powershell Payload](img/4804ad374219e2dbd8472fa0a144f182.png "MeterPwrShell : Automated Tool That Generate The Perfect Powershell Payload")](https://1.bp.blogspot.com/--qnfewPCN20/YJfKYD6zW0I/AAAAAAAAJCA/xP0AemhlRJ4Ac5ss7rJCqpxfZZ4oaSskgCLcBGAsYHQ/s728/MeterPwrShell%25281%2529.png)

**MeterPwrShell** 是生成 Powershell Oneliner 的自动化工具，可以在 Metasploit 上创建 Meterpreter Shell，绕过 AMSI，绕过防火墙，绕过 UAC，绕过任何 AVs。

这个工具由 [Metasploit-Framework](https://github.com/rapid7/metasploit-framework) 和 [amsi.fail](https://amsi.fail/) 提供支持

**注释**

*   千万不要把这个程序产生的有效载荷上传到任何在线扫描仪上。
*   切勿将此程序用于恶意目的。
*   传播这个程序产生的有效载荷并不酷。
*   这个程序产生的任何损害都不是我(作为程序开发者)的责任！！！
*   如果你有一些功能推荐，张贴在问题上。
*   如果你对这个程序有什么问题，试着重新下载一次(相信我)，因为有时我会编辑版本并修复它而不告诉你。
*   如果你想知道我的有效载荷如何绕过任何 AVs，你可以检查一下[这个](https://gist.github.com/GetRektBoy724/9383c9580cb1c9935fc04cc7eb7ef004)和[这个](https://blog.sevagas.com/Bypass-Antivirus-Dynamic-Analysis)。
*   甚至不要试图分叉这个库，你不会得到发布！
*   对于每个有问题或想联系我的人，请使用 Discord。我的不和谐 ID 是:DeadSec#4077。
*   这个工具不是完全开源的(我猜)，是的，你可以尽可能多地重新发布它，但你永远不会得到这个工具的源代码(不要问我为什么)。

**特性(v2.0.0)**

*   自动迁移(使用**前置迁移**
*   **AutoGetSYSTEM** (自动将权限从普通用户提升到系统)
*   禁用所有防火墙概要文件(如果您使用**自动获取系统**功能)
*   完全绕过 Windows Defender 实时保护
*   禁用 Windows Defender 安全功能(如果您使用 **AutoGetSYSTEM** 功能)
*   完全不可用的有效负载(如果您使用自动迁移功能)
*   成功绕过 **AMSI**
*   简短的一行程序
*   绕过防火墙(如果您选择未分级的有效负载)
*   伟大的 **CLI**
*   很多(自己试试)

所有有效负载功能均在 Windows 10 v20H2 上测试

**与 Metasploit 框架的 web_delivery 模块相比，MeterPwrShell 的优势**

*   较短的 stager(或者在这种情况下是较短的一行程序)
*   不需要为登台程序设置服务器
*   支持 Ngrok 内置(这样受害者就不需要在同一个本地网络上)
*   自动内置权限
*   轻松绕过 Windows Defender

**要求**

*   Kali Linux，Ubuntu，或者 Debian(如果你不使用其中任何一个，这个工具将无法工作！！！)
*   Metasploit 框架
*   互联网连接(在受害者和攻击者的计算机上)

**安装**

在发布页面下载您的二进制文件，请根据您的操作系统选择您的二进制文件。尚不支持 i386 架构。

**用途**

##### **。/meter wrshell 2 kalx 64-c 帮助**

**可用参数:help，version，showbanner，showlastdebuglog
help:显示此页面
version:显示 MeterPwrShell 的版本
showbanner:显示 MeterPwrShell 的横幅
showlastdebuglog:嗯，它有点不言自明的 tho**

您也可以使用不带任何标志和参数的 MeterPwrShell

**攻击媒介**

*   BadUSBs
*   恶意快捷方式( [lnk2pwn](https://github.com/it-gorillaz/lnk2pwn/) )
*   文档宏有效负载
*   MS DDE 漏洞
*   极端方式:自己打进去
*   让您对受害者执行命令的任何利用漏洞/漏洞
*   Idk 我已经没有主意了 lmao

[**Download**](https://github.com/GetRektBoy724/MeterPwrShell)