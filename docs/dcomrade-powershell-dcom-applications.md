# DCOMrade:用于枚举易受攻击的 DCOM 应用程序的 Powershell 脚本

> 原文：<https://kalilinuxtutorials.com/dcomrade-powershell-dcom-applications/>

DCOMrade 是一个 Powershell 脚本，能够列举可能存在漏洞的 DCOM 应用程序，这些应用程序可能允许横向移动、代码执行、数据泄漏等。

该脚本适用于 Powershell 2.0，但也适用于上述所有版本。该脚本目前支持以下 Windows 操作系统(x86 和 x64):

*   微软视窗 7
*   微软视窗 10
*   微软 Windows Server 2012 / 2012 R2 版
*   微软 Windows Server 2016

**也可以理解为:** [Kaboom:自动化渗透测试的脚本](https://kalilinuxtutorials.com/kaboom-penetration-test/)

**工作原理**

首先建立与目标系统的远程连接，该连接在整个脚本中用于大量操作。在目标系统上执行 Powershell 命令，检索所有 DCOM 应用程序及其 AppID。

AppID 用于遍历 Windows 注册表，并检查其条目中没有设置`**LaunchPermission**`子项的任何 AppID，这些 AppID 被存储并用于检索其关联的 CLSID。

该脚本对每个操作系统使用特定的黑名单，这就是为什么目标操作系统有不同的选项。

黑名单会跳过由于 DCOM 应用程序无法激活而可能导致脚本挂起的 CLSID 条目，这将减少目标系统上的负载，并缩短脚本完成的时间。

使用 CLSID，可以激活与之关联的 DCOM 应用程序。“快捷方式”CLSID 用于计算与之关联的`**MemberTypes**`的数量，这样做是为了检查`**MemberTypes**`的默认数量。

这个数字用于检查 CLSID 是否包含与这个数量不同的任何内容。该脚本使用“快捷方式”的 CLSID(`**HKEY_CLASSES_ROOT\CLSID\{00021401-0000-0000-C000-000000000046}**`)来执行此操作，因为这是一个跨 Microsoft Windows 操作系统的共享 CLSID。

具有不同数量的`**MemberTypes**`的 CLSID 可能持有可以(ab)使用的`**Method**`或`**Property**`，并且将被添加到数组中。

正在检查数组中的 CLSID 在`**MemberTypes**`中的字符串，这些字符串可能指示使用它的方式，这个字符串列表可以在 [VulnerableSubset](https://github.com/sud0woodo/DCOMrade/blob/master/VulnerableSubset.txt) 文件中找到。

请注意，此列表绝不是查找每个易受攻击的 DCOM 应用程序的完整列表，但此列表是该过程的动态部分，它应该为脚本用户提供一种方法来查找可能指示 DCOM 应用程序功能的特定字符串，这些功能可能对他们的目的有用。

脚本的结果被输出到一个 HTML 报告中，应该可以作为一种预防措施用于审计系统。在进攻端，我创建了一个帝国模块，在写这篇文章的时候，它正在等待被添加到主分支的批准。

**先决条件**

该脚本虽然没有被用作 Empire 模块，但由于脚本的工作方式以及它与目标机器的连接方式不同，因此有一些限制。

*   要使此脚本工作，需要在 Windows 防火墙中允许 Windows 远程管理服务(5985)；
*   如果目标系统的网络配置文件设置为`**Public**`，则需要执行以下命令，以允许在目标系统上使用 Windows 远程管理服务:`**Enable-PSRemoting -SkipNetworkProfilecheck -Force**`
*   仅当用户拥有目标系统上本地管理员的凭据时，此脚本才有效。没有这些凭据，您将无法启动与目标计算机的远程会话，也无法激活 DCOM 应用程序。

**示例用法**

当在 Microsoft Windows 域中时:

**。\ dcomrade . PS1-计算机名[计算机名/IP]-用户[本地管理员]-OS[操作系统]-域[域名]**

不在 Microsoft Windows 域中时:

。\ dcomrade . PS1-计算机名[计算机名/IP]-用户[本地管理员]-OS[操作系统]

[**Download**](https://github.com/sud0woodo/DCOMrade)

**鸣谢:马特·纳尔逊**