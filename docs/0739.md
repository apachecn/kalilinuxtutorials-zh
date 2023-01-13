# JShielder:强化 Linux 服务器脚本/ Secure LAMP-LEMP 部署者/ CIS Benchmark G

> 原文：<https://kalilinuxtutorials.com/jshielder-hardening-script/>

[![JShielder : Hardening Script for Linux Servers/ Secure LAMP-LEMP Deployer/ CIS Benchmark G](img/d3e37d93b69119e4de08b9be5323a2b4.png "JShielder : Hardening Script for Linux Servers/ Secure LAMP-LEMP Deployer/ CIS Benchmark G")](https://1.bp.blogspot.com/-ulWqg3vaXy4/XS6-9aOS-UI/AAAAAAAABYc/N0Sbug5zAfAF_e87xdsEbd-vhmXQiQ4pgCLcBGAs/s1600/Jsheilder.png)

JSHielder 是一个开源的 Bash 脚本，旨在帮助系统管理员和开发者保护他们将要部署任何 web 应用或服务的 Linux 服务器。

这个工具自动化了安装托管 web 应用程序所需的所有软件包以及强化 Linux 服务器的过程，几乎不需要用户干预。

新添加的脚本遵循 CIS 基准指南，为 Linux 系统建立安全的配置状态。

这个工具是一个 Bash 脚本，可以自动加强 Linux 服务器的安全性，其步骤如下:

*   配置主机名
*   重新配置时区
*   更新整个系统
*   创建一个新的管理员用户，这样您就可以安全地管理您的服务器，而不需要与 root 用户进行远程连接。
*   帮助用户生成安全的 RSA 密钥，以便远程访问您的服务器是从您的本地电脑和没有传统的密码独家完成
*   配置、优化和保护 SSH 服务器(一些设置遵循 CIS 基准)
*   配置 IPTABLES 规则以保护服务器免受常见攻击
*   禁用未使用的文件系统和网络协议
*   通过安装配置 fail2ban 来保护服务器免受暴力攻击
*   安装和配置火炮作为一个蜜罐，监测，封锁和警报工具
*   Installs PortSentry
*   安装、配置和优化 MySQL
*   安装 Apache Web 服务器
*   安装、配置和保护 PHP
*   通过配置文件并安装 ModSecurity、ModEvasive、Qos 和 SpamHaus 模块来保护 Apache
*   通过安装 ModSecurity NginX 模块来保护 NginX
*   安装 RootKit 猎人
*   保护根主目录和 Grub 配置文件
*   安装 Unhide 以帮助检测恶意隐藏进程
*   安装安全审计和入侵防御系统 Tiger
*   限制对 Apache 配置文件的访问
*   禁用的编译器
*   为系统更新创建每日 Cron 作业
*   通过 sysctl 配置文件进行内核强化(调整)
*   /tmp 目录强化
*   PSAD IDS 安装
*   启用流程记帐
*   支持无人值守升级
*   MOTD 和未经授权的访问横幅
*   禁用 USB 支持以提高安全性(可选)
*   配置限制性默认 UMASK
*   配置和启用审计
*   按照 CIS 基准配置审计规则
*   Sysstat 安装
*   ArpWatch 安装
*   CIS 基准测试后的其他强化步骤
*   安全 cron
*   自动化设置 GRUB 引导程序密码的过程
*   保护启动设置
*   为关键系统文件设置安全文件权限

**#新！！**

*   使用 ModSecurity 部署 LEMP

**也可阅读-[Commando VM:Complete man diant Offensive VM(突击队 VM)，首款基于 Windows 的全渗透测试虚拟机分发](https://kalilinuxtutorials.com/commandovm-complete-mandiant-offensive-vm/)**

**增加了 CIS 基准 JShielder 脚本**

*   遵循 CIS 基准指南的独立强化脚本[https://www.cisecurity.org/benchmark/ubuntu_linux/](https://www.cisecurity.org/benchmark/ubuntu_linux/)

**运行工具**

**。/jshielder.sh**

作为根用户

**问题**

有问题请在 Github 上为 JShielder 新开一期。

**发行版可用性**

*   Ubuntu Server 16.04LTS
*   Ubuntu Server 18.04LTS

**变更日志**

*   v2.4 增加了 ModSecurity 的 LEMP 部署
*   继 LAMP Deployer 的一些 CIS 基准测试项目之后，v2.3 的更多强化步骤
*   v2.2.1 删除了 Ubuntu 16.04 上的 suhosing 安装，修复了 MySQL 配置、GRUB 引导加载程序设置功能，服务器 ip 现在通过 IP 路由获得，不依赖于接口命名
*   v2.2 根据 CIS 基准指南增加了新的强化选项
*   v2.1 强化了 SSH 配置，调整了内核安全配置，修复了 iptables 规则无法在启动时加载。添加了 auditd、sysstat、arpwatch 安装。
*   更多部署选项，选择菜单，PHP Suhosin 安装，更干净的代码
*   1.0 版-新代码

致谢:**杰森·索托**

[**Download**](https://github.com/Jsitech/JShielder)