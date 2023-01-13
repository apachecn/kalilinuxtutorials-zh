# ADReaper:一个用 Go 编写的 Windows 活动目录测试的快速枚举工具

> 原文：<https://kalilinuxtutorials.com/adreaper/>

[![](img/a8eb312c645034cd3292e9ffb0b60580.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjAPE7k-xbSWB1z805j1wuWE4xPoX0Fn7jMzJhDWFGdy85lVi3ejp5G7fM4lzx0KJLFW2KEnURfUjxItF2mSkBzOB-4EUZnWJoNzcCMLJFKe2Qa08QMubCHgrXdF3iXqCdjiumnleIavvKMo_GTaZYmR3iiM2KLDZQbnsQY_aj2UzhIGom1kXA4TVrS/s728/Microsofts-LDAP-Security-Update-and-the-Impact-on-Financial-Institutions-Today-Featured-Blog-Image%20(1).png)

`**ADReaper**`是一个用`**Golang**`编写的工具，它可以在几秒钟内用 LDAP 查询枚举一个活动目录环境

## 安装

您可以从最新版本下载预编译的 Windows/Linux 可执行二进制文件

### 从源安装

要从源代码构建，克隆 repo 并使用 GO 构建它

**git 克隆 https://github . com/aidnpearce 369/adre open
$ CD adre open/
$ go build**

## 使用

ADReaper 使用各种命令执行枚举，这些命令执行与它相关的 LDAP 查询

**PS C:\ Users \ red teamer \ Desktop \ shared>。\ adreaper . exe
-命令字符串
命令运行
DC-列出域控制器
域信任-列出域信任
用户-列出所有用户
计算机-列出所有计算机
组-列出所有具有成员的组
SPN-列出服务主体对象
从未登录-列出从未登录的用户
GPO-列出组策略对象
ou-列出组织单位
ms-sql 列出 MS-SQL servers
AS re proast–列出 AS-REP 可漫游帐户
unconstrained–列出 Unconstrained 委派帐户
admin-priv–列出具有管理权限的 AD 对象
-dc 字符串
输入 DC
-过滤器字符串
用于用户/组/计算机的过滤器
list–仅列出所有对象
full data–列出具有属性
membership 的所有对象–列出一个对象的所有成员
(默认“列表”)**

要查询域的`**Domain Controller**`的属性，

**。\ adreaper . exe-DC-user-password-command DC**

要查询域的`**Trust Attributes**`，

**。\ adreaper . exe-DC-user-password-command domain-trust**

要从域中列出所有的`**Users**`，

**。\ adreaper . exe-DC-用户-密码-命令用户**

要列出域中所有具有属性的`**Users**`,

**。\ adreaper . exe-DC-user-password-command users-filter full-data**

要列出特定用户的成员资格，

**。\ adreaper . exe-DC-user-password-command users-name-filter membership**

[**Download**](https://github.com/AidenPearce369/ADReaper)