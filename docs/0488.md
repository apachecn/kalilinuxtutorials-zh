# LAPSToolkit:审计和攻击 LAPS 环境的工具

> 原文：<https://kalilinuxtutorials.com/lapstoolkit-audit-attack/>

**LAPSToolkit** 用 PowerShell 编写的函数，利用 PowerView 来审计和攻击已经部署了微软本地管理员密码解决方案(LAPS)的 Active Directory 环境。

它包括查找由系统管理员专门委派的组，查找具有可以查看密码的“所有扩展权限”的用户，以及查看所有启用了 LAPS 的计算机。

请提交问题或对任何问题或性能改进的意见。此项目是使用旧版本 PowerView 的代码创建的。

**又念: [Androguard:逆向工程，恶意软件& Goodware 分析 Android 应用](https://kalilinuxtutorials.com/androguard/)**

**Get-laps 计算机:**

显示所有启用 LAPS 的计算机、密码表达式和密码(如果用户有访问权限)

**Find-LAPSDelegatedGroups:**

搜索所有 ou 以查看哪些 AD 组可以读取 ms-Mcs-AdmPwd 属性

**Find-AdmPwdExtendedRights**

解析启用 LAPS 的每台 AD 计算机的扩展权限，并查找哪个组具有读取权限，以及是否有任何用户具有“所有扩展权限”。

系统管理员可能不知道拥有所有扩展权限的用户可以查看密码，并且可能比委派组中的用户受到的保护更少。

例如，将计算机添加到域中的用户会自动获得“所有扩展权限”权限。由于此函数将解析每台 AD 计算机的 ACL，对于较大的域，这可能需要很长时间。

**鸣谢:肖恩·梅特卡夫(@pyrotek3)、威尔·施罗德(@harmj0y)、卡尔·福萨恩(@kfosaaen)、马特·格雷贝尔(@mattifestation)**

[**Download**](https://github.com/leoloobeek/LAPSToolkit)