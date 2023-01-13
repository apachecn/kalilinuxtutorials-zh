# KnockOutlook:一个玩 Outlook 的小工具

> 原文：<https://kalilinuxtutorials.com/knockoutlook/>

[![](img/ed0622fee0e95cc0512191093a0fe0ce.png)](https://1.bp.blogspot.com/-foEBsfxAkGE/YTHxYk7GIHI/AAAAAAAAKqg/1WyDkTUn-rcaFFGBGKX0HdBoFA505deJgCLcBGAsYHQ/s856/Outlook.png)

**KnockOutlook** 是一个 C#项目，它与 Outlook 的 COM 对象交互，以执行许多在红队约定中有用的操作。

**命令行用法**

****_*_ _*_///*///*/////*//*_/_/_/，</_ \/_ \///*///////*_ \////*//
///|////// *<//*///*///*////*////*//，<//*/|*/*/_ _/_ _ _/*/_ \ _ _ _ _ _ _*/_ _，*/_*/*/_ _ _*/_ _ _ _/_/_/_ \\\
参数:
–操作:指定要运行的操作
–关键字:为“搜索”操作指定关键字
–id:为“保存”操作指定 EntryID
–绕过:绕过编程访问安全设置(需要管理员)
操作:
检查:执行多次检查以确保操作安全
联系人:提取每个帐户的所有联系人
邮件:提取每个帐户的邮箱元数据
搜索:在每个邮箱中搜索提供的关键字
保存:按其 EntryID 保存指定的邮件
示例:
KnockOutlook.exe–操作检查
KnockOutlook.exe–操作联系人
KnockOutlook.exe–操作邮件–旁路
KnockOutlook.exe–操作搜索–关键字密码
KnockOutlook.exe–操作保存–id******

**操作**

*   **check** 枚举 Outlook 安装详细信息，以构建正确的注册表项并检索编程访问安全设置。如果该值被设置为`**Warn when antivirus is inactive or out-of-date**`，它将向 WMI 查询任何已安装的防病毒产品，并解析它们的当前状态。
*   **联系人**列举每个已配置账户的联系人，并提取以下信息:
    *   全名
    *   电子邮件地址
*   **邮件**枚举每个已配置账户的邮件，提取如下元数据:
    *   身份证明
    *   时间戳
    *   科目
    *   从
    *   到
    *   附件
*   **搜索**使用 Outlook 内置的搜索引擎在每个已配置帐户的邮箱中进行搜索，并返回正文中包含所提供关键字的邮件的`**EntryID**`。
*   **保存**使用 Outlook 内置的`**Save As**`机制导出其`**EntryID**`引用的邮件。

**物体模型护卫绕过**

`**--byp**a**ss**`开关可与**`contacts``mails``search`**和`**save**`操作结合使用，因为当前过程以高完整性级别运行。

它将尝试快照 Outlook 的当前安全策略，以自动允许编程访问安全提示的方式修补它，并在操作完成后最终将其恢复到初始状态。

**输出**

所有操作都会在屏幕上输出基本信息。

`**contacts**`和`**mails**`操作将以 JSON 格式将结果输出到 Gzip 压缩文件中。

`**save**`操作将以`**.MSG**`格式导出请求的邮件。

所有文件名都是在运行时随机生成的。

默认情况下，Outlook 的安全临时文件夹用作所有导出文件的目的地。

[**Download**](https://github.com/eksperience/KnockOutlook)