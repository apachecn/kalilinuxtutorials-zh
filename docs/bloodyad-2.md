# bloodyAD:活动目录权限提升框架

> 原文：<https://kalilinuxtutorials.com/bloodyad-2/>

[![](img/7f58b9ea1897dcda032c92f4a6fec768.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi1lVCSxQMimzrySTsYZtHtQhQNczumgKhBLnSGwaptPTOl-kG1D-4-dxroGwKi-UGftxY-Tg9sOEiquIfNpIopsuBQ_C8RkLt3U58FElsgMJIxEBy-hGfy4XX3kd5hwyUGxoXWwQmWBmN6WrpiX8TQ3U2I-ofSgkBzNHdRNXeQ9A3t5ptpnfU2jlNr/s760/blody%20logo%20(1).png)

`**bloodyAD.py**`活动目录权限升级是一把瑞士军刀

## 描述

此工具可以对域控制器执行特定的 LDAP/SAMR 调用，以便执行 AD 特权。

`**bloodyAD**`支持使用明文密码、pass-the-hash、pass-the-ticket 或证书进行身份验证，并绑定到域控制器的 LDAP 服务以执行 AD 特权。

它被设计成透明地与 SOCKS 代理一起使用。

## 安装

首先，如果您在 Linux 上运行它，您必须在您的操作系统上安装`**libkrb5-dev**`以便 kerberos 能够工作:

**Debian/Ubuntu/Kali
apt-get 安装 libkrb5-dev
Centos/RHEL
yum 安装 krb5-devel
Fedora
dnf 安装 krb5-devel
Arch Linux
pacman-S krb5**

python 包可用:

**pip 安装 blood YAD
blood YAD–host 172 . 16 . 1 . 15-d blood . local-k change password John . doe ' password 123！'**

或者，您可以克隆回购:

**git 克隆–深度 1 https://github.com/CravateRouge/bloodyAD
pip 安装。
bloody ad–host 172 . 16 . 1 . 15-d bloody . local-k change password John . doe ' password 123！'**

### 属国

*   python3
*   DSinternals
*   冲击
*   Ldap3
*   Gssapi (linux)或 Winkerberos (Windows)

## 用法

简单用法:

bloody ad–host 172 . 16 . 1 . 15-d bloody . local-u Jane . doe-p:70016778 CB 0524 c 799 AC 25 b 439 BD 6a 31 更改密码 john.doe 'Password123！'

注意:你可以在 https://cravaterouge.github.io/找到更多的例子

所有可用功能的列表:

**【blood YAD】$ blood YAD-h
用法:blood YAD[-h][-d DOMAIN][-u USERNAME][-p PASSWORD][-k][-c CERTIFICATE][-s][–HOST HOST]
{ getobject attributes，setAttribute，addUser，addComputer，delObject，changePassword，addObjectToGroup，addForeignObjectToGroup，delObjectFromGroup，getChildObjects，setShadowCredentials，setGenericAll，setRbcd，setDCSync –Kerberos
-c CERTIFICATE，–CERTIFICATE CERTIFICATE
CERTIFICATE authentic ation，例如:“path/to/key:path/to/cert”
-s，–secure 尝试使用 LDAP over TLS aka LDAPS(默认为 LDAP)
–主机主机 DC 的主机名或 IP(例如:my.dc.local 或 172.16.1.3)
命令:
{getObjectAttributes，setAttribute，addUser，addComputer，delObject，changePassword**

## 有用的命令

**获取群成员
blood YAD-u John . doe-d bloody-p password 512！–host 192 . 168 . 10 . 2 getobject attributes Users 成员
获取最小密码长度策略
bloody ad-u John . doe-d bloody-p password 512！–host 192 . 168 . 10 . 2 getobject attributes ' DC = bloody，DC=local' minPwdLength
获取 AD 功能级别
bloody AD-u Administrator-d bloody-p password 512！–host 192 . 168 . 10 . 2 getobject attributes ' DC =血腥，DC =本地' msDS-Behavior-Version
获取该域的所有用户
blood YAD-u John . doe-d bloody-p password 512！–host 192 . 168 . 10 . 2 Get child objects ' DC =血腥，DC =本地'用户
获取该域的所有计算机
bloody ad-u John . doe-d bloody-p password 512！–host 192 . 168 . 10 . 2 Get child objects ' DC =血腥，DC =本地'计算机
获取该域的所有容器
bloody ad-u John . doe-d bloody-p password 512！–host 192 . 168 . 10 . 2 get child objects ' DC =血腥，DC =本地'容器
启用 DONT_REQ_PREAUTH 进行 asre proast
blood YAD-u Administrator-d bloody-p password 512！–host 192 . 168 . 10 . 2 setuseracountcontrol John . doe 0x 400000
Disable account Disable
blood YAD-u Administrator-d bloody-p password 512！–host 192 . 168 . 10 . 2 setUserAccountControl John . doe 0x 0002 False
获取 user account control 标志
bloody ad-u Administrator-d bloody-p password 512！–主机 192 . 168 . 10 . 2 getobject attributes John . doe user account control
读取 GMSA 帐户密码
blood YAD-u John . doe-d bloody-p password 512–主机 192 . 168 . 10 . 2 getobject attributes gmsaAccount $ msDS-managed password
读取将计算机对象添加到域的配额
bloody ad-u John . doe-d bloody-p password 512！–主机 192 . 168 . 10 . 2 getobject attributes ' DC =血腥，DC =本地' ms-DS-machineaccountoquota**

[**Download**](https://github.com/CravateRouge/bloodyAD)