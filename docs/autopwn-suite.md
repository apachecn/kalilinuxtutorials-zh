# AutoPWN Suite:用于自动扫描漏洞和利用系统的项目

> 原文：<https://kalilinuxtutorials.com/autopwn-suite/>

[![](img/9f8dd80e80103d145531458f4f145487.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhAPwDQ_8jO8SZmdI79y59Cj5KTD_uyL3FApjSfrrs7cjBzZZZOT6142jQ2PwuiT_I3Vik4JDrcCy9R-zBT8mTm2c5XUXFPdii0CrigAMYhgYjIXQMsG1ntcvag-ritCre34jndgmv6gJv6oX7oj4oO_ONlESqbOYSZ_dQ1dkLZ23MaaXGHrWGV0Nzw/s728/autopwn-suite-project-for-scanning-vulnerabilities-and-exploiting-systems-automatically-840x440%20(1).png)

AutoPWN Suite 是一个自动扫描漏洞和利用系统的项目。

## 特征

*   全自动！(使用`**-y**`标志启用)
*   无需任何用户输入即可检测网络 IP 范围。
*   基于版本的漏洞检测。
*   Web 应用程序漏洞测试。(目前只有 LFI)
*   从您的终端获取有关漏洞的信息。
*   自动下载与漏洞相关的攻击。
*   在网络上制造噪音的噪音模式。
*   鬼鬼祟祟的逃避模式。
*   根据权限自动决定要使用的扫描类型。
*   易于阅读的输出。
*   使用配置文件指定参数。
*   通过 webhook 或电子邮件发送扫描结果。
*   可在 Windows、MacOS 和 Linux 上运行。

## 它是如何工作的？

AutoPWN Suite 使用 nmap TCP-SYN 扫描来枚举主机并检测其上运行的软件版本。在收集了足够的主机信息后，AutoPWN Suite 会自动生成一个“关键字”列表来搜索 NIST 漏洞数据库。

## 装置

您可以使用 pip 安装它。(须藤推荐)

**sudo pip 安装自动生成套件**

运筹学

你可以克隆回购。

**git 克隆 https://github.com/GamehunterKaan/AutoPWN-Suite.git**

运筹学

你可以从 releases 下载 debian (deb)包。

用户不需要安装。/autopwn-suite_1.5.0.deb

## 使用

始终建议使用 root 权限(sudo)运行。

自动模式(这是使用 AutoPWN 套件的预期方式。)

**autown-suite-y**

帮助菜单

**$ autopwn-suite -h
用法:AutoPWN . py[-h][-v][-y][-c CONFIG][-t TARGET][-HF HOSTFILE][-ST { ARP，ping}] [-nf NMAPFLAGS] [-s {0，1，2，3，4，5 }][-a API][-m { evange，noise，normal }]
[-nt time out][-o OUTPUT][-RP { EMAIL，webhook}] [-rpe EMAIL 请不要要求任何东西。(全自动模式)
-c CONFIG，–CONFIG CONFIG
指定要使用的配置文件。(默认:无)
扫描:
扫描选项
-t 目标，–目标目标
要扫描的目标范围。此参数会覆盖 hostfile 参数。(192.168.0.1 或 192.168.0.0/24)
-hf 主机文件，–主机文件主机文件
包含要扫描的主机列表的文件。
-st {arp，ping}，–Scan type { ARP，ping}
扫描类型。
-nf NMAPFLAGS，–nmap flags nmap flags
用于端口扫描的自定义 nmap 标志。(必须指定为:-nf="-O")
-s {0，1，2，3，4，5}，–speed { 0，1，2，3，4，5}
扫描速度。(默认值:3)
-一个 api，–API API 指定用于漏洞检测的 API 密钥，以加快扫描速度。(默认:无)
-m {规避，噪声，正常}，–模式{规避，噪声，正常}
扫描模式。
-nt 超时，–Noise time out 超时
噪音模式超时。(默认:无)
报告:
报告选项
-o 输出，–输出输出
输出文件名。(默认:autopwn.log)
-rp {email，webhook}，–Report { email，webhook}
报表发送方式。
-rpe EMAIL，–report EMAIL EMAIL
用于发送报告的电子邮件地址。
-rpep PASSWORD，–reportemailpassword PASSWORD
发送电子邮件报告的密码。
-rpet EMAIL，–reporte mail to EMAIL
发送报告的电子邮件地址。
-rpef 电子邮件，–report EMAIL from EMAIL
要发送的电子邮件。
-rpes 服务器，–reportemailserver 服务器
用于发送报告的电子邮件服务器。
-rpesp 端口，–电子邮件服务器的 reportemailserverport 端口
端口。
-rpw WEBHOOK，–report WEBHOOK web hook
用于发送报告的 web hook。**

[**Download**](https://github.com/GamehunterKaan/AutoPWN-Suite)