# SharpHide:创建隐藏注册表项的工具

> 原文：<https://kalilinuxtutorials.com/sharphide/>

[![SharpHide : Tool To Create Hidden Registry Keys](img/8cec977f03b668645ee4fb739d870434.png "SharpHide : Tool To Create Hidden Registry Keys")](https://1.bp.blogspot.com/-06xC4w30GpE/XeovGk67q3I/AAAAAAAAD0U/OGeYpWWDMCIRN72sBkE673VGPf8uk0RHgCLcBGAsYHQ/s1600/Capture%25281%2529.png)

SharpHide 只是迷惑 DFIR 调查的一个漂亮的持续伎俩。使用 NtSetValueKey 本机 API 创建一个隐藏的(空终止的)注册表项。这是通过在 UNICODE_STRING 键值 name 前面添加一个空字节来实现的。

该工具使用以下注册表路径创建隐藏的运行键:**(如果是用户，则为 HKCU，否则为 HKLM)\ SOFTWARE \ Microsoft \ Windows \ current version \ Run**

**也可以理解为-[burp suite:Secret Finder 扩展，用于从 HTTP 响应](https://kalilinuxtutorials.com/burpsuite-secret-finder/)中发现 API keys/token**

**用途**

要创建隐藏的注册表(运行)项:

**SharpHide.exe action = create key value = " C:\ Windows \ Temp \ bla . exe "**

要使用参数创建隐藏的注册表(运行)项，请执行以下操作:

**SharpHide.exe action = create key value = " C:\ Windows \ Temp \ bla . exe " args = " arg 1 arg 2"**

删除隐藏的注册表(运行)项:

**SharpHide.exe 行动=删除**

这个工具也可以和 Cobalt Strike 的执行装配一起使用。

**演职员表:**科内利斯·德·普拉(@Cneelis) /包抄

[**Download**](https://github.com/ewhitehats/InvisiblePersistence/blob/master/InvisibleRegValues_Whitepaper.pdf)