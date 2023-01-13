# LinuxCheck : Linux 信息收集脚本 2019

> 原文：<https://kalilinuxtutorials.com/linuxcheck-linux-information-collection-script/>

[![LinuxCheck  : Linux Information Collection Script 2019](img/f9a1d9bf7ec7bfd430b84390065a29fa.png "LinuxCheck  : Linux Information Collection Script 2019")](https://1.bp.blogspot.com/-SvsCT99h97g/XeoMbKs-hKI/AAAAAAAAD0I/RAcYvitG-k0lwnFVt0UsipCRlTZTFwfHwCLcBGAsYHQ/s1600/Linux-Logo.png)

**LinuxCheck** 是一个小型的 Linux 信息收集脚本，主要用于应急响应。可以在 Debian 或者 Centos 下使用。

**特性**

*   CPU 前 10，内存前 10
*   CPU 使用率
*   启动时间
*   硬盘空间信息
*   用户信息，密码信息
*   环境变量检测
*   服务列表
*   系统程序更改(debsums -e 和 rpm -va)
*   网络流量统计
*   网络连接，监听端口
*   港口
*   路由表信息
*   路由转发
*   空袭预防措施
*   DNS 服务器
*   SSH 登录信息
*   SSH 登录 IP
*   iptables 信息
*   SSH 密钥检测
*   SSH 突发 IP
*   Crontab 检测
*   Crontab 后门检测
*   查找通用配置文件
*   查找常用软件
*   审计历史文件
*   查询主机文件
*   lsmod 异常内核模块
*   异常文件检测(nc、隧道、代理常见黑客工具)
*   大文件检测(一些打包的大文件)
*   可用空间，硬盘安装
*   港口
*   LD _ 预载检测
*   LD _ 库 _ 路径
*   ld.so .预载
*   网卡混杂模式
*   最常用的软件
*   在最近 7 天内更改文件时间
*   在过去 7 天内更改文件 ctime
*   View SUID file
*   查找:隐藏文件
*   查找敏感文件(nc、nmap、隧道)
*   别名
*   LSOF -L1
*   SSHD
*   查找 bash bounce shell
*   php webshell 扫描
*   jsp webshell 扫描
*   asp / aspx webshell 扫描
*   采矿过程检测
*   rkhunter 扫描

**也可阅读—[Sooty:SOC 分析师一体化 CLI 工具，用于自动化&加速工作流程](https://kalilinuxtutorials.com/sooty-soc-analysts-all-in-one-cli-tool/)**

**用途**

**联网状态:**

**apt-get 安装 silversearcher-ag
yum -y 安装 _silver_searcher**

**离线状态:**

**Debian:dpkg-I silver searcher-ag _ 2 . 2 . 0-1+B1 _ amd64 . deb
Centos:rpm-IVH the _ silver _ searcher-2 . 1 . 0-1 . el7 . x86 _ 64 . rpm**

$git 克隆[https://github.com/al0ne/LinuxCheck.git](https://github.com/al0ne/LinuxCheck.git)
$ chmod u+x Linux check . sh
$。/LinuxCheck.sh
**如果已经安装了 ag 和 rkhunter，可以直接使用以下命令:**
$ bash-c " $(curl-sSL[https://raw . githubusercontent . com/al0ne/Linux check/master/Linux check . sh](https://raw.githubusercontent.com/al0ne/LinuxCheck/master/LinuxCheck.sh))"
**文件将以**$ IP addr _ hostname _ username _ timestamp . log 格式保存

[**Download**](https://github.com/al0ne/LinuxCheck)