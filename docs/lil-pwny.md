# Lil PWNY:使用 Python 中的多重处理审计 Active Directory 密码

> 原文：<https://kalilinuxtutorials.com/lil-pwny/>

[![Lil PWNY : Auditing Active Directory Passwords Using Multiprocessing In Python](img/7e6e8043d508ba0ed46d816ed12cb3ac.png "Lil PWNY : Auditing Active Directory Passwords Using Multiprocessing In Python")](https://1.bp.blogspot.com/-jjCZlg9nfvw/X3h6JMCvzbI/AAAAAAAAHt8/O6735_-MXSkP2SEuHhhlDhHaBaDM2NE6QCLcBGAsYHQ/s728/ad%25281%2529.png)

**Lil Pwny** 是一个 Python 应用程序，用于对从 Active Directory 中恢复的用户密码的 NTLM 哈希进行离线审计，并与来自 wave I was Pwned 的已知受损密码进行比较。匹配 HIBP 的任何帐户的用户名将在一个. txt 文件中返回

还有其他功能:

*   能够提供一个自己的密码列表，以检查广告用户。这使您可以将用户密码与您怀疑人们可能正在使用的与您的组织相关的密码进行核对。这些是 NTLM 哈希，然后将 AD 哈希与此哈希以及 HIBP 哈希进行比较。
*   返回使用相同密码的帐户列表。有助于查找使用相同密码作为管理帐户和标准帐户的用户。

更多关于 Lil Pwny 的信息可以在我的博客上找到

**建议**

开发这个应用程序是为了在高资源基础设施上运行，以充分利用 Python 多处理。它将在桌面级硬件上运行，但是您使用的内核越多，审计运行的速度就越快。

**安装**

通过 pip 安装

**pip 安装 lil-pwny**

**用途**

Lil-pwny 将作为全局命令安装，使用如下:

**用法:**lil-pwny[-h]-HIBP HIBP[-A A]-AD AD _ HASHES[-d][-m][-o OUTPUT]
**可选参数:**
-hibp，–HIBP-path HIBP。NTLM 哈希的 txt 文件
-a，–包含附加密码的. txt 文件，用于检查
-ad，–ad-哈希来自 AD 用户的 NTLM 哈希
-d，–find-duplicates 输出重复密码用户的列表
-m，–memory 将 HIBP 哈希列表加载到内存中(需要超过 24GB RAM
)
-o，–out-path 设置输出路径。未设置时使用工作目录

**举例:**

**lil-pwny-hibp ~/hibp _ hashes . txt-ad ~/ad _ NTLM _ hashes . txt-a ~/additional _ passwords . txt-o ~/Desktop/Output-m-d**

使用`-m`标志将把 HIBP 散列加载到内存中，这将允许更快的搜索。注意这将需要至少 24GB 的可用内存。

**获取输入文件**

*   **步骤 1:获取 IFM 广告数据库转储**

在域控制器上，使用`ntdsutil`生成 AD 域的 IFM 转储。在提升的 PowerShell 窗口中运行以下命令:

ntdsutil
激活实例 ntds
ifm
创建完整**输出路径* *

*   **步骤 2:从这个输出中恢复 NTLM 哈希**

要从 AD IFM 数据中恢复 NTLM 哈希，需要 Powershell 模块 [DSInternals](https://github.com/MichaelGrafnetter/DSInternals) 。

安装后，使用 IFM 数据中的系统配置单元来恢复格式为`usernme:hash`的散列，并将它们保存到文件`ad_ntlm_hashes.txt`

$ boot key = Get-boot key-system hive path '。\ registry \ SYSTEM ' Get-addb count-All-DBPath '。\ Active Directory \ NTDs . dit '-boot key $ boot key | Format-Custom-View hash catnt | Out-File ad _ NTLM _ hashes . txt-编码 ASCII

*   **第三步:下载最新的 HIBP 哈希文件**

该文件可以被下载

从[加载到这里](https://downloads.pwnedpasswords.com/passwords/pwned-passwords-ntlm-ordered-by-count-v5.7z)

最新版本的散列文件包含大约 5.51 亿个散列。