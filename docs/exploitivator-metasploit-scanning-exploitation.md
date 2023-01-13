# Exploitivator:自动化 Metasploit 扫描和开发

> 原文：<https://kalilinuxtutorials.com/exploitivator-metasploit-scanning-exploitation/>

[![Exploitivator : Automate Metasploit Scanning And Exploitation](img/e7efebdfa8f8bfb2a24f5a354fa06d14.png "Exploitivator : Automate Metasploit Scanning And Exploitation")](https://1.bp.blogspot.com/-iYMIMNXeIuY/XfPO-dmbdkI/AAAAAAAAD9Q/ZWklPhDAzgg20CCPpi2uG-lN3LN88CniQCLcBGAsYHQ/s1600/MSF.png)

Exploitivator 是一个自动化 Metasploit 扫描和利用工具。这只在卡莉身上测试过。

它依赖于 Python 的 msfrpc 模块，这里详细介绍:[https://www . trustwave . com/Resources/spider labs-Blog/Scripting-Metasploit-using-MSGRPC/](https://www.trustwave.com/Resources/SpiderLabs-Blog/Scripting-Metasploit-using-MSGRPC/)

安装必要的 Kali 包和 PostgreSQL gem for Ruby:apt-get install PostgreSQL libpq-dev git-core gem install pg

从 git 安装 msfrpc Python 模块的当前版本:git clone git://github . com/spider labs/msfrpc . git msfrpc CD msfrpc/Python-msfrpc Python setup . py install。

**又读-[攻击范围:模拟攻击&的工具收集数据到 Splunk](https://kalilinuxtutorials.com/attack-range-simulate-attacks-splunk/)**

**用途**

在运行任一脚本之前，请加载 msfconsole 并启动 MSGRPC 服务。可以使用 Metasploit 中的 msfrpcd 启动 MSGRPC，如下所示:load msgrpc Pass=abc123

扫描和/或利用的结果将出现在 Metasploit 控制台和输出文件(msf_scan_output.txt 和 exploitivator_output.txt)中。

使用 MSFScan 对一组目标主机运行多个 Metasploit 扫描。使用 Exploitivator 对一组目标主机运行 Nmap 脚本扫描，并自动利用任何报告为易受攻击的主机。

**命令行用法:**

示例:应用程序可以按如下方式运行，其中“10.128.108.178”是攻击机器的 IP 地址，“hosts.txt”是目标主机列表，“msf”是 Metasploit Postgres 用户名，“abc123”是 Metasploit Postgres 密码:。/exploit ivator . py-l 10 . 128 . 108 . 178-f hosts . txt-u MSF-m ABC 123

**MSFScan**

命令行用法:**。/msf_scan.py 文件名。/msf_scan.py 文件名 MSF _ DB _ Username MSF _ DB _ Password**

示例:应用程序可以按如下方式运行，其中“hosts.txt”是目标主机列表，“msf”是 Metasploit Postgres 用户名，“abc123”是 Metasploit Postgres 密码:。/msf_scan.py hosts.txt msf abc123

使用脚本的默认 Metasploit Postgres 用户名(msf)和脚本的默认 Metasploit Postgres 密码(abc123)，以“hosts.txt”作为目标主机列表运行。/msf_scan.py hosts.txt

**配置文件**

这两个脚本都依赖于配置文件来提供所需的 Nmap 和 Metasploit 诈骗和攻击的详细信息。

**MSFScan**

该脚本使用名为“scan_types.cfg”的配置文件。这包含将对目标运行的任何 Metasploit 扫描的路径列表。例如:辅助/扫描器/dcerpc/端点映射器辅助/扫描器/smb/smb_version 辅助/扫描器/x11/open_x11 辅助/扫描器/发现/IPv6 _ 多播 _ping 辅助/扫描器/发现/IPv6 _ 邻居辅助/扫描器/smb/smb_login

该脚本使用两个配置文件(exploitivator_scan.cfg 和 exploitivator.cfg)。一个用于指定 Nmap 扫描和参数(exploitivator_scan.cfg)，一个用于指定 Metasploit 有效负载和参数(exploitivator.cfg)。这些使用“##”作为分隔符，并具有以下格式。

exploit ivator _ scan . CFG:[Label]# #[Nmap 命令行参数]#[用于文件输出的 Nmap 命令行参数]# #[可选–如果正在使用 Nmap 的 greppable 输出，则使用 grep 命令]

在上面的格式中:

1.  第一部分是将扫描链接到漏洞的标签
2.  第二部分是 Namp 命令行的一部分，它指定了要运行的扫描类型的详细信息，如端口和脚本
3.  第三部分是 Namp 命令行的一部分，它定义了 Nmap 输出文件(Exploitivator 处理 XML 或 greppable Nmap 输出)
4.  可选的第四部分是 gep 命令，您希望使用它来识别。“gnmap”文件

文件内容示例如下所示:SMB_08-067##-p U:137，U:139，T:139，T:445–脚本 sm b-vuln-ms08-067 . NSE # #-oX ms _ 08 _ 067 . XML SMB _ 09-050 # #-p U:137，U:139，T:139，T:445–脚本 sm b-vuln-CVE 2009-3103 . NSE # #-脚本

exploit ivator . CFG:[Label]# #[Metasploit 利用路径]# #[可选–Metasploit 负载详细信息]

文件内容示例如下所示:SMB _ 08-067 # # exploit/windows/SMB/ms08 _ 067 _ netapi # # windows/meter preter/bind _ TCP SMB _ 09-050 # # exploit/windows/SMB/ms09 _ 050 _ sm B2 _ negotiate _ func _ index # # windows/meter preter/bind _ TCP SMB _ 10-061 # # exploit/windows/SMB/ms10 _ 061 _ spoolss # # windows/meter preter/index

[**Download**](https://github.com/N1ckDunn/Exploitivator)