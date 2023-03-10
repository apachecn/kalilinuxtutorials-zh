# NebulousAD:自动化凭证审计工具

> 原文：<https://kalilinuxtutorials.com/nebulousad-automated-credential-auditing-tool/>

[![NebulousAD : Automated Credential Auditing Tool](img/f6e67886298a9b5cbfc6f9b6ede89d2d.png "NebulousAD : Automated Credential Auditing Tool")](https://1.bp.blogspot.com/-GvP1kX66PYM/XWdJfCq5H_I/AAAAAAAACRA/BZuVZ_a-5BY8s5iRdjYszTMZ_STje-AYgCLcBGAs/s1600/NebulousAD%2B%25281%2529.png)

**NebulousAD** 自动化凭证审计工具。我将添加一个维基，文档等。很快。特点:

*   将增加按组编校的功能，该功能不会转储哈希值，也不会检查特定组(如域管理员)中帐户的 api。

**安装**

只需下载预编译版本(不需要 python 解释器)，或者从源代码编译:

需要 Python2.7(目前)

**运行** git 克隆 git @ github . com:NuID/nebulousad . git **接下来用** python setup.py 安装

然后初始化您的密钥。您可以通过访问获得您的密钥:[https://nebulous.nuid.io/#/register](https://nebulous.nuid.io/#/register)一旦注册，点击按钮生成您的 API 密钥并复制它。

现在你可以这样初始化它们:`**nebulousAD -init-key <api_key>**`

您现在可以运行该工具了。如果它找不到您的 API 密钥，您可能需要重新启动终端会话。API 密钥存储在环境变量中。注销并重新登录也可以。

**又读-[AIL 框架:分析信息泄露框架](https://kalilinuxtutorials.com/ail-framework-analysis-information-leak-framework/)**

**用法**

转储所有散列并根据 NuID 的 api 检查它们的示例:`**nebulousAD.exe -v -snap -check**`

**NuID 凭证审计工具。
可选参数:** -h，–帮助显示此帮助消息并退出
-ntds NTDS NTDS。DIT 文件解析
-system SYSTEM 系统注册表配置单元解析
-csv csv 输出结果到该路径的 CSV 文件。
-json json 输出结果到此路径下的 JSON 文件
-init-key INIT_KEY 将您的 Nu_I.D. API 密钥安装到当前用户路径下。
-c，-check 对照 Nu_I.D. API 检查是否有受损的
凭证。
-snap 使用 ntdsutil.exe 将系统注册表
配置单元和 ntds.dit 文件快照到:\NuID\
-shred 对文件执行删除操作时，使用 7 步
覆盖 sdelete.exe。在这里下载:
https://docs.microsoft.com/en-
us/sysinternals/downloads/s delete
-no-backup 不备份现有的快照，只覆盖
它们。
-CLEAN-OLD-SNAPS CLEAN _ OLD _ SNAPS 清理超过 N 天的备份。
**显示选项:** -用户状态显示用户是否被禁用
-pwd-last-set 显示在 NTDS 内发现的每个帐户的 pwdLastSet 属性。DIT 数据库。
-历史转储 NTLM 用户的哈希历史。
-v 启用详细模式。

**-抓拍**

*   如果您有权限的话，`**-snap**`参数将自动快照 Active Directory(使用`**ntdsutil.exe**`)，并转储 ntds.dit 文件以及系统注册表配置单元。你可以使用各种方法或者`**ntdsutil.exe**`工具来手动转储这个文件。
*   如果手动转储，可以指向带有`**-system path\to\SYSTEM**`和`**-ntds path\to\ntds.dit**`的文件。如果您想要审核旧快照，这很有用。

–**抓拍**

*   如果您有权限的话，`**-snap**`参数将自动快照 Active Directory(使用`**ntdsutil.exe**`)，并转储 ntds.dit 文件以及系统注册表配置单元。你可以使用各种方法或者`**ntdsutil.exe**`工具来手动转储这个文件。
*   如果手动转储，可以指向带有`**-system path\to\SYSTEM**`和`**-ntds path\to\ntds.dit**`的文件。如果您想要审核旧快照，这很有用。

**——检查**

这需要一个来自 https://nebulous.nuid.io/#/register[的 API 密匙。一旦你有了它并安装了`**-init-key**`，你就可以检查 NuID API 的散列。如果您指定了`**-history**`，它还会检查每个帐户的密码历史，以查看用户以前使用的密码是否被泄露。](https://nebulous.nuid.io/#/register)

**-用户状态**

添加指示帐户在 Active Directory 中是启用还是禁用的输出

**-pwd-最后一组**

添加指示帐户密码上次设置日期的输出。这对于检测违反 GPO 中定义的不会自动重置的帐户(如服务帐户)的安全策略非常有用。

**-历史**

还可以审核或转储帐户存储的密码历史记录

**-撕碎**

*   擦除快照时使用 DoD 7 遍覆盖。这需要 sdelete.exe 在你的道路上。您可以从这里获得:[https://docs . Microsoft . com/en-us/sys internals/downloads/s delete](https://docs.microsoft.com/en-us/sysinternals/downloads/sdelete)
*   只需下载并将其放在您的`**%SYSTEMDRIVE\Windows\System32\**`目录中，或者设置环境变量。

**-清洁-旧-快照**

当设置此应用程序与任务计划程序一起运行时，有助于清理备份。系统配置单元和。在较大的域中，dit 文件可能相当大，并占用大量磁盘空间。如果您使用任务计划程序进行每日审计，您可以像这样使用此选项:`**-clean-old-snaps 7**`只存储 1 周的快照。

**-无备份**

*   如果我们检测到旧快照，默认情况下我们会将其备份到`**%SYSTEMDRIVE%\Program Files\NuID\snapshot-backups**`。这是因为 ntdsutil.exe 需要一个空目录。如果您希望禁用此备份，而只是擦除当前快照，请使用此参数。
*   还有`**-ntds path\to\ntds.dit**`。如果您想要审核旧快照，这很有用。

**——检查**

这需要一个来自 https://nebulous.nuid.io/#/register[的 API 密匙。一旦你有了它并安装了`-init-key`，你就可以检查 NuID API 的散列。如果您指定了`-history`，它还会检查每个帐户的密码历史，以查看用户以前使用的密码是否被泄露。](https://nebulous.nuid.io/#/register)

**-用户状态**

添加指示帐户在 Active Directory 中是启用还是禁用的输出

**-pwd-最后一组**

添加指示帐户密码上次设置日期的输出。这对于检测违反 GPO 中定义的不会自动重置的帐户(如服务帐户)的安全策略非常有用。

**-历史**

还要审核或转储帐户存储的密码历史记录

**-撕碎**

*   擦除快照时使用 DoD 7 遍覆盖。这需要 sdelete.exe 在你的道路上。您可以从这里获得:[https://docs . Microsoft . com/en-us/sys internals/downloads/s delete](https://docs.microsoft.com/en-us/sysinternals/downloads/sdelete)
*   只需下载并将其放在您的`**%SYSTEMDRIVE\Windows\System32\**`目录中，或者设置环境变量。

**-清洁-旧-快照**

当设置此应用程序与任务计划程序一起运行时，有助于清理备份。系统配置单元和。在较大的域中，dit 文件可能相当大，并占用大量磁盘空间。如果您使用任务计划程序进行每日审计，您可以像这样使用此选项:`**-clean-old-snaps 7**`只存储 1 周的快照。

**-无备份**

如果我们检测到旧快照，默认情况下我们会将其备份到`**%SYSTEMDRIVE%\Program Files\NuID\snapshot-backups**`。这是因为 ntdsutil.exe 需要一个空目录。如果您希望禁用此备份，而只是擦除当前快照，请使用此参数。

[**Download**](https://github.com/NuID/nebulousAD)