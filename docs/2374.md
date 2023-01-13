# SQLRecon:一个 C# MS SQL 工具包，设计用于攻击性侦察和后期开发

> 原文：<https://kalilinuxtutorials.com/sqlrecon/>

[![](img/44488f777ec3574f2d70f191aeda4b98.png)](https://blogger.googleusercontent.com/img/a/AVvXsEiOu6clx_wNufKB1NbOhgdF1nBOQOf6CnYcGwJvLYKzFR8jp7MOfDMmGwXAHS_TuZ2SZsQQ31pGFtJBRI7yWxVNNkjSs3sOgdxPqkZuN3Xo6eeuvVgjhzuFQUmaw0eq8LIHe0oFskDcQbVz2zFlzWyYPL_hiCPekHU0MIdo8M1Xg744o9VRECiX7ie1=s728)

**SQLRecon** 是一个 C# MS-SQL 工具包，设计用于攻击性侦察和后期利用。有关每种技术的详细使用信息，请参考 wiki。

# 用法

您可以从 releases 页面获取 SQLRecon 的副本。或者，您可以随意自己编译解决方案，这应该像克隆回购协议一样简单，双击解决方案文件并构建。

## 强制参数

强制参数由身份验证类型(Windows、本地或 Azure)、连接参数和模块组成。

*   **-a**-认证类型
    *   **-一个 Windows**-使用 Windows 认证。这使用当前用户令牌。
    *   **-本地**-使用本地认证。这需要本地数据库用户的凭据。
    *   **-a Azure**-使用 Azure AD 域用户名和密码认证。这需要域用户的凭据。

如果认证类型是 **Windows** ，那么您将需要提供以下参数。

*   **-s 服务器名**–SQL 服务器主机名
*   **-d 数据库**–SQL server 数据库名称
*   **-m 模块**–您想要使用的模块

如果认证类型是**本地**，那么您将需要提供以下参数。

*   **-d 数据库**–SQL server 数据库名称
*   **-u 用户名**-本地 SQL 用户的用户名
*   **-p 密码**-本地 SQL 用户的密码
*   **-m 模块**–您想要使用的模块

如果认证类型是 **Azure** ，那么您将需要提供以下参数。

*   **-d 数据库**–SQL server 数据库名称
*   **-r DOMAIN.COM**-域的 FQDN
*   **-u 用户名**-域用户的用户名
*   **-p 密码**-域用户的密码
*   **-m 模块**–您想要使用的模块

## 标准模块

标准模块用于与单个 MS SQL server 进行交互。

*   **QUERY-o QUERY**–执行任意 SQL 查询
*   **whoami**–查看您以何种用户身份登录
*   **映射**–查看您映射到哪个用户
*   **角色**–枚举用户是否映射了公共和/或系统管理员角色
*   **数据库**–显示 SQL server 上的所有数据库
*   **表格**–显示您连接到的数据库中的所有表格
*   **search -o 关键字**–在您所连接的数据库的表格中搜索列名。
*   **smb -o 共享**–捕获 NetNTLMv2 哈希
*   **Enable XP**–启用 xp_cmdshell(需要 sysadmin 角色或类似角色)
*   **Disable XP**–禁用 xp_cmdshell(需要 sysadmin 角色或类似角色)
*   **xpcmd -o 命令**–执行任意系统命令(需要 sysadmin 角色或类似角色)
*   **Enable ole**–启用 OLE 自动化程序(需要系统管理员角色或类似角色)
*   **禁用 ole**–禁用 OLE 自动化程序(需要系统管理员角色或类似角色)
*   **olecmd -o 命令**–执行任意系统命令(需要 sysadmin 角色或类似角色)
*   **Enable clr**–启用自定义 CLR 程序集(需要 sysadmin 角色或类似角色)
*   **Disable clr**–禁用自定义 CLR 程序集(需要 sysadmin 角色或类似角色)
*   **模拟**–枚举任何可以模拟的用户帐户
*   **链接**–枚举任何链接的 SQL 服务器

## 模拟模块

模拟模块用于在模拟的 SQL 用户的上下文中与单个 MS SQL server 进行交互。

*   **iquery-I impersonate user-o QUERY**–以模拟用户的身份执行任意 SQL 查询
*   **ienablexp-I impersonate user**–启用 xp_cmdshell(需要 sysadmin 角色或类似角色)
*   **idisablexp-I impersonate user**–禁用 xp_cmdshell(需要 sysadmin 角色或类似角色)
*   **ixpcmd -i IMPERSONATEUSER -o 命令**–执行任意系统命令(需要 sysadmin 角色或类似角色)
*   **ienableole-I impersonate user**–启用 ole 自动化程序(需要 sysadmin 角色或类似角色)
*   **idisable ole-I impersonate user**–禁用 OLE 自动化程序(需要系统管理员角色或类似角色)
*   **iolecmd -i IMPERSONATEUSER -o 命令**–执行任意系统命令(需要系统管理员角色或类似角色)

## 链接的 SQL Server 模块

当您能够通过已建立的连接与链接的 SQL server 进行交互时，链接的 SQL Server 模块是有效的。

*   **l databases**-l Linked servername–显示链接的 SQL server 上的所有数据库
*   **l tables**-l Linked servername–显示您在链接的 SQL server 上连接到的数据库中的所有表
*   **lquery**-l linked servername-o QUERY–在链接的 SQL 服务器上执行任意 SQL 查询

[**Download**](https://github.com/skahwah/SQLRecon)