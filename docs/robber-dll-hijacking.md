# Robber:用于查找容易被 DLL 劫持的可执行文件的工具

> 原文：<https://kalilinuxtutorials.com/robber-dll-hijacking/>

Robber 是一个免费的开源工具，使用 Delphi XE2 开发，不依赖任何第三方。

## **那么什么是 DLL 劫持呢？**

Windows 在其基础架构中有一个 dll 搜索路径。如果您可以在没有绝对路径的情况下找出可执行文件请求的 DLL(触发此搜索过程)，那么您可以将您的恶意 DLL 放在搜索路径中更高的位置，这样它将在真实版本出现之前被发现，Windows 会很乐意将您的攻击代码提供给应用程序。

因此，让我们假设 Windows 的 DLL 搜索路径如下所示:

*   \Windows
*   \Windows\system32
*   \ Windows \ sys wow 64

而有些可执行文件“Foo.exe”请求“bar.dll”，恰好就住在 syswow64 (D)子目录中。这让你有机会把你的恶意版本放在 A)，B)或 C)中，它将被加载到可执行文件中。

如前所述，如果您可以用自己的版本替换 DLL，即使是绝对完整路径也无法防止这种情况。

Microsoft Windows 使用 Windows 文件保护机制保护系统路径，如 System32，但是在企业解决方案中保护可执行文件免受 DLL 劫持的最佳方法是:

*   使用绝对路径而不是相对路径
*   如果您有个人签名，请在将 DLL 加载到内存之前，签名您的 DLL 文件并检查您的应用程序中的签名。否则，使用原始 DLL 哈希检查 DLL 文件的哈希)

当然，这也不仅限于 Windows。任何允许外部库动态链接的操作系统理论上都容易受到这种攻击。

**也读作[ADModule——微软签名的 ActiveDirectory PowerShell 模块](https://kalilinuxtutorials.com/admodule-microsoft-signed-activedirectory/)**

**强盗**使用简单的机制找出容易被劫持的 dll:

1.  扫描可执行文件的导入表并找出链接到可执行文件的 dll
2.  搜索放置在可执行文件中与链接的 DLL 相匹配的 DLL 文件(如我之前所说，可执行文件的当前工作目录具有最高优先级)
3.  如果发现任何 DLL，扫描主题的导出表
4.  将可执行文件的导入表与 DLL 的导出表进行比较，如果发现任何匹配，则可执行文件和匹配的公共函数将标记为 DLL 劫持候选。

## **强盗特征**

*   能够选择扫描类型(签名/未签名的应用程序)
*   确定可执行签名人
*   确定哪个引用的 dll 可能会被劫持
*   确定候选 dll 的导出方法名
*   配置规则以确定哪种劫持是最好的选择，并以不同的颜色显示主题

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/MojtabaTajik/Robber)