# ADLab:定制的 PowerShell 模块，用于设置活动目录实验室环境来进行渗透测试

> 原文：<https://kalilinuxtutorials.com/adlab/>

[![](img/2b70948859ce872e9938162115d2c700.png)](https://blogger.googleusercontent.com/img/a/AVvXsEjNfkYIgDrPsEwLbjzv3lDTNKbl0I9z3PA0a42dx482izJ8Rcs9Jp_JKJQGmQ_RbqnrO6-il40OKeOWpk9A-K8jYW6sbqORQqhTQSTkFXX8SXou5JgebqJcSxvBvpE0yp5v24vdh30RnS-7iBX0OXCQzRUJMlk_6tio6GjEy8C6FL9o9tpm4QxDwgGH=s676)

**ADLab** ，本模块的目的是自动部署一个活动目录实验室，以进行内部渗透测试。

感谢 Joe Helle 和他的 PowerShell 为 Pentesters 提供了关于攻击媒介生成的课程。

* * *

**指令**

**准备**

**可选但推荐:将模块移入`PSModulePath`**

**#** **显示 PSModulePath
$ env:PSModulePath . split("；")
#将模块移至路径
移动项目。\ ADLab \ " C:\ Windows \ system32 \ Windows powershell \ v 1.0 \ Modu**les \ "

**导入模块**

# **导入全局模块
导入模块 ADLab
#导入本地模块
导入模块。\ADLab.psm1**

**初始实验室设置**

**调用-DCPrep**

此功能准备将当前虚拟机/计算机用作新林的域控制器。它设置一个静态 IP 地址，将 DNS 服务器设置为本地主机，并重命名计算机。

# **使用所有默认值准备当前虚拟机，同时显示详细输出
Invoke-DCPrep-Verbose
#设置自定义主机名并使用 Google DNS 访问互联网
Invoke-DCPrep-Hostname " DC "-new IP v4 DNS server " 8 . 8 . 8 . 8 "
#使用自定义 IP 和默认网关并显示详细输出
Invoke-DCPrep-Verbose-new IP v4 address " 192 . 168 . 1 . 99 "-new IPv6 gateway " 192 . 168 .**

**调用-森林部署**

该功能安装 AD DS 功能并设置新的 Active Directory 林，无需任何用户输入。完成后重新启动计算机。

**安装 FQDN 为“bufu-sec.local”的新林，默认 DSRM 密码为“password！”
Invoke-forest deploy-Domain bufu-sec.local
安装一个 FQDN 为“bufu-sec . local”的新林，DSRM 密码设置为“P@ssword！”并显示调试消息
Invoke-forest deploy-Domain " bufu-sec . local "-dsrm password " P @ ss word！"-罗嗦**

**调用-DNS 部署**

该功能从安装 DNS 功能开始。然后，它添加主区域并配置服务器转发器。

**在当前主机上安装和配置 DNS，并显示详细输出。**

**Invoke-DNS deploy-Verbose-network id 192 . 168 . 47 . 0/24-ZoneFile " 192 . 168 . 47 . 2 . in-addr . arpa . DNS "-server forwarder 1.1.1.1**

**调用-DHCPDeploy**

该功能从在当前机器上安装 DHCP 功能开始。然后，它添加必要的安全组，并向域控制器授权新的 DHCP 服务器。最后，它用提供的值配置新的 DHCP 作用域。

**在本地 DC 上安装和配置 DHCP。
Invoke-DHCP deploy-Verbose-ScopeName " Default "-ScopeID 192 . 168 . 47 . 0-StartIP 192 . 168 . 47 . 100-EndIP 192 . 168 . 47 . 200-subnet mask 255 . 255 . 255 . 0-DNS server 192 . 168 . 47 . 10-Router 192 . 168 . 47 . 10
在指定的
Invoke-DHCP deploy-Verbose-ScopeName " Default "-scope id 192 . 168 . 47 . 0-StartIP 192 . 168 . 47 . 100-EndIP 192 . 168 . 47 . 200-subnet mask 255 . 255 . 255 . 0-DNS server 192 . 168 . 47 . 10-路由器 192.168.47.10 -DCFQDN DC01.bufu**

**内容**

**调用-ADLabFill**

该函数首先创建在全局 groups 变量中定义的组和 ou。默认情况下，它会为每个 OU 生成 10 个用户对象。

**用对象填充森林并显示详细输出
Invoke-ADLabConfig-Verbose
为每个 OU 创建 50 个用户并显示详细输出
Invoke-ADLabConfig-Verbose-user count 50**

**攻击媒介**

 **该函数从域中获取一定数量的随机用户，并为每个用户设置 DoesNotRequirePreAuth 标志。不包括默认帐户，如 Administrator 和 krbtgt。默认情况下，使 5%的用户可重复漫游。

**使 5%的用户成为可漫游用户并显示详细输出
Set-ASREPRoasting-Verbose
使域中的 10 个随机用户成为可漫游用户
Set-ASREPRoasting-VulnerableUsersCount 10
使用户 bufu 成为可漫游用户并显示详细输出
Set-ASREPRoasting-Users bufu-Verbose
使提供的用户列表成为可漫游用户并显示详细输出
Set-ASREPRoasting-Users(" bufu "，" pepe**

**Set-BadACLs**

该功能首先授予 Chads 组对 Domain Admins 的一般权限。然后，它授予 Degens 组对 Chads 组的一般权限。最后，它将来自 Degens 组的一些用户的通用权限授予 Normies 组的一些用户。

**#创建易受攻击的 ACL 并显示详细输出
Set-BadACLs -Verbose**

**Set-PSRemoting**

该函数首先配置 GPO 以允许 WinRM 通过 TCP 端口 5985 连接到加入域的系统。然后，它通过 GPO 启用 PS Remoting。

# **启用 PS Remoting 并显示详细输出
Set-PSRemoting -Verbose**

[**Download**](https://github.com/xbufu/ADLab)**