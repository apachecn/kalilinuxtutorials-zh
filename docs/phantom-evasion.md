# 幻影闪避:Python AV 闪避工具，即使使用最常见的 32 位 Metasploit 有效负载，也能生成 FUD 可执行文件

> 原文：<https://kalilinuxtutorials.com/phantom-evasion/>

phantom-escalation 是一个用 python 编写的交互式防病毒规避工具，即使使用最常见的 32 位 msfvenom 有效负载(64 位有效负载的检测率较低)，也能生成(几乎)FUD 可执行文件。

该工具的目的是通过使用专注于多态代码和防病毒沙箱检测技术的模块，使 pentesters 轻松规避防病毒。

从 1.0 版本开始，幻影规避还包括一个专门用于持久性和辅助模块的后开发部分。

以下操作系统正式支持自动设置:

1.  Kali Linux Rolling 2018.1+ (64 位)
2.  Parrot 安全性(64 位)

以下操作系统可能能够通过手动设置运行幻影规避:

1.  Arch Linux (64 位)
2.  BlackArch Linux (64 位)
3.  基本(64 位)
4.  Linux Mint (64 位)
5.  Ubuntu 15.10+ (64 位)
6.  Windows 7/8/10 (64 位)

**也可阅读-[R3 con 1 z 3 r:一款具有直观特性的轻量级网络信息收集工具](https://kalilinuxtutorials.com/r3con1z3r/)**

**入门**

简单地 git 克隆或下载和解压缩幻影-规避文件夹

**卡莉 Linux:**

官方支持自动设置，打开终端并执行幻影规避:

**s**Udo python phantom-escape . py
或者:
sudo chmod+x ./phantom-escape . py
sudo。/phantom-escalation . py

**依赖关系(仅用于手动设置)**

1.  metasploit 框架
2.  mingw-w64(windows 上的 cygwin)
3.  （同 groundcontrolcenter）地面控制中心
4.  apktool
5.  剥夺
6.  葡萄酒(窗户上不需要)
7.  阿普西纳
8.  pyinstaller(安装程序)

需要 libc6-dev-i386(仅限 linux)

**WINDOWS 有效负载**

**Windows 外壳代码注入模块(C)**

支持 Msfvenom windows 有效负载和自定义外壳代码
( >)随机化垃圾代码和 windows 防病毒规避技术
( >)多字节 Xor 编码器可用(请参见多字节 Xor 编码器自述文件部分)
( >)诱骗进程 Spawner 可用(请参见诱骗进程 Spawner 部分)
( >)剥离可执行文件可用([https://en . Wikipedia . org/wiki/Strip _(Unix)](https://en.wikipedia.org/wiki/Strip_(Unix)))【T6(>)执行时间范围:35-35

1.  Windows 外壳代码注入 VirtualAlloc:使用 VirtualAlloc、CreateThread、WaitForSingleObject API 在内存中注入并执行外壳代码。
2.  Windows 外壳代码注入 VirtualAlloc NoDirectCall LL/GPA:使用 VirtualAlloc、CreateThread、WaitForSingleObject API 在内存中注入并执行外壳代码。使用 LoadLibrary 和 GetProcAddress API 动态加载(不直接调用)关键 API。
3.  Windows 外壳代码注入 VirtualAlloc NoDirectCall GPA/GMH:使用 VirtualAlloc、CreateThread、WaitForSingleObject API 在内存中注入并执行外壳代码。使用 GetModuleHandle 和 GetProcAddress API 动态加载(不直接调用)关键 API。
4.  Windows 外壳代码注入 HeapAlloc:使用 HeapAlloc、HeapCreate、CreateThread、WaitForSingleObject API 在内存中注入并执行外壳代码。
5.  Windows 外壳代码注入 HeapAlloc NoDirectCall LL/GPA:使用 HeapCreate、HeapAlloc、CreateThread、WaitForSingleObject API 在内存中注入并执行外壳代码。使用 LoadLibrary 和 GetProcAddress API 动态加载(不直接调用)关键 API。
6.  Windows 外壳代码注入 HeapAlloc NoDirectCall GPA/GMH:使用 HeapCreate、HeapAlloc、CreateThread、WaitForSingleObject API 在内存中注入并执行外壳代码。使用 GetModuleHandle 和 GetProcAddress API 动态加载(不直接调用)关键 API。
7.  Windows 外壳代码注入进程注入:使用 VirtualAllocEx、WriteProcessMemory、CreateRemoteThread、WaitForSingleObject API 将外壳代码注入并执行到远程进程内存(默认:OneDrive.exe(x86)、explorer.exe(x64))。
8.  Windows 外壳代码注入进程 inject NoDirectCall LL/GPA:使用 VirtualAllocEx、WriteProcessMemory、CreateRemoteThread、WaitForSingleObject API 将外壳代码注入并执行到远程进程内存(默认:OneDrive.exe(x86)、explorer.exe(x64))。使用 LoadLibrary 和 GetProcAddress API 动态加载(不直接调用)关键 API。
9.  Windows 外壳代码注入进程注入 NoDirectCall GPA/GMH:使用 VirtualAllocEx、WriteProcessMemory、CreateRemoteThread、WaitForSingleObject API 将外壳代码注入并执行到远程进程内存(默认:OneDrive.exe(x86)、explorer.exe(x64))。使用 GetModuleHandle 和 GetProcAddress API 动态加载(不直接调用)关键 API。
10.  Windows 外壳代码注入线程劫持:将外壳代码注入远程进程内存并执行执行线程执行劫持(默认:OneDrive.exe(x86)，explorer.exe(x64))使用 VirtualAllocEx，WriteProcessMemory，Get/SetThreadContext，Suspend/ResumeThread API。
11.  Windows 外壳代码注入线程劫持 LL/GPA:将外壳代码注入远程进程内存并执行它使用 VirtualAllocEx、WriteProcessMemory、Get/SetThreadContext、Suspend/ResumeThread API 执行线程执行劫持(默认:OneDrive.exe(x86)、explorer.exe(x64))。使用 LoadLibrary 和 GetProcAddress API 动态加载(不直接调用)关键 API。
12.  Windows 外壳代码注入线程劫持 GPA/GMH:将外壳代码注入远程进程内存并执行使用 VirtualAllocEx、WriteProcessMemory、Get/SetThreadContext、Suspend/ResumeThread API 执行线程执行劫持(默认:OneDrive.exe(x86)、explorer.exe(x64))。使用 GetModuleHandle 和 GetProcAddress API 动态加载(不直接调用)关键 API。

**Windows 纯 C meterpreter stager**

与 msfconsole 和 cobalt strike beacon 兼容的纯 C 多态仪表中继站。(反向 TCP/反向 http)

(>)随机垃圾代码和 windows 防病毒规避技术(>)幻影规避诱饵进程可用(请参见幻影规避诱饵进程生成器部分) (>)剥离可执行文件可用([https://en . Wikipedia . org/wiki/Strip _(Unix)](https://en.wikipedia.org/wiki/Strip_(Unix)))(>)执行时间范围:35-60 秒

1.  c meter preter/reverse _ TCP VirtualAlloc(x86/x64):用 c 编写的 32/64 位 windows/meter preter/reverse _ TCP 多态 stager(需要负载设置为 windows/meter preter/reverse _ TCP 的 multi/handler 侦听器(如果 x86)—windows/x64/meter preter/reverse _ TCP(如果 x64)，内存:虚拟)
2.  c meter preter/reverse _ TCP Heap alloc(x86/x64):用 c 编写的 32/64 位 windows/meter preter/reverse _ TCP 多态 stager(需要负载设置为 windows/meter preter/reverse _ TCP 的 multi/handler 侦听器(如果 x86)—windows/x64/meter preter/reverse _ TCP(如果 x64)，内存:堆)
3.  c meter preter/reverse _ TCP VirtualAlloc NoDirectCall GPAGMH(x86/x64):用 c 编写的 32/64 位 windows/meter preter/reverse _ TCP 多态 stager(r require multi/handler listener，有效负载设置为 windows/meter preter/reverse _ TCP(如果 x86)—windows/x64/meter preter/reverse _ TCP(如果 x64)，内存:虚拟，API 在运行时加载)
4.  c meter preter/reverse _ TCP HeapAlloc NoDirectCall GPAGMH(x86/x64):用 c 编写的 32/64 位 windows/meter preter/reverse _ TCP 多态 stager(需要负载设置为 windows/meter preter/reverse _ TCP(如果 x86)—windows/x64/meter preter/reverse _ TCP(如果 x64)，内存:堆，运行时加载的 API)
5.  c meter preter/reverse _ HTTP VirtualAlloc(x86/x64):用 c 编写的 32/64 位 windows/meter preter/reverse _ HTTP 多态 stager(需要负载设置为 windows/meter preter/reverse _ HTTP(如果 x86)-windows/x64/meter preter/reverse _ HTTP(如果 x64)，内存:虚拟)
6.  c meter preter/reverse _ HTTP Heap alloc(x86/x64):用 c 编写的 32/64 位 windows/meter preter/reverse _ HTTP 多态 stager(需要负载设置为 windows/meter preter/reverse _ HTTP(如果 x86)-windows/x64/meter preter/reverse _ HTTP(如果 x64)，内存:堆)
7.  c meter preter/reverse _ HTTP VirtualAlloc NoDirectCall GPAGMH(x86/x64):用 c 编写的 32/64 位 windows/meter preter/reverse _ HTTP 多态 stager(需要负载设置为 windows/meter preter/reverse _ HTTP 的 multi/handler 侦听器(如果 x86)—windows/x64/meter preter/reverse _ HTTP(如果 x64)，在运行时加载 API)
8.  c meter preter/reverse _ HTTP HeapAlloc NoDirectCall GPAGMH(x86/x64):用 c 编写的 32/64 位 windows/meter preter/reverse _ HTTP 多态 stager(需要负载设置为 windows/meter preter/reverse _ HTTP(如果 x86)—windows/x64/meter preter/reverse _ HTTP(如果 x64)，内存:堆，运行时加载的 API)
9.  c meter preter/reverse _ HTTPS VirtualAlloc(x86/x64):用 c 编写的 32/64 位 windows/meter preter/reverse _ http 多态 stager(需要负载设置为 windows/meter preter/reverse _ https 的 multi/handler 侦听器(如果 x86)—windows/x64/meter preter/reverse _ https(如果 x64)，内存:虚拟)
10.  c meter preter/reverse _ HTTPS Heap alloc(x86/x64):用 c 编写的 32/64 位 windows/meter preter/reverse _ http 多态 stager(需要负载设置为 windows/meter preter/reverse _ https 的 multi/handler 侦听器(如果 x86)—windows/x64/meter preter/reverse _ https(如果 x64)，内存:堆)
11.  c meter preter/reverse _ HTTPS VirtualAlloc NoDirectCall GPAGMH(x86/x64):用 c 编写的 32/64 位 windows/meter preter/reverse _ http 多态 stager(需要负载设置为 windows/meter preter/reverse _ https(如果 x86)-windows/x64/meter preter/reverse _ https(如果 x64)的 multi/handler 侦听器，在运行时加载 API)
12.  c meter preter/reverse _ HTTPS HeapAlloc NoDirectCall GPAGMH(x86/x64):用 c 编写的 32/64 位 windows/meter preter/reverse _ http 多态 stager(需要负载设置为 windows/meter preter/reverse _ https 的 multi/handler 侦听器(如果 x86)—windows/x64/meter preter/reverse _ https(如果 x64)，内存:堆，运行时加载的 API)

**Powershell / Wine-Pyinstaller 模块**

**Powershell 模块:**

(>)随机垃圾代码和 windows 防病毒规避技术(>)诱骗进程可用(请参见幻影规避诱骗进程可用部分) (>)剥离可执行文件可用([https://en . Wikipedia . org/wiki/Strip _(Unix)](https://en.wikipedia.org/wiki/Strip_(Unix)))(>)执行时间范围:35-60 秒

1.  Windows Powershell/Cmd Oneliner 下载程序:需要用户提供的 Powershell/Cmd Oneliner 有效负载(例如 Empire oneliner 有效负载)。生成用 c 编写的 Windows powershell/Cmd oneliner dropper，Powershell/Cmd oneliner 有效载荷是使用 system()函数执行的。
2.  Windows Powershell 脚本下载程序:支持 msfvenom 和自定义 Powershell 有效负载。(32 位 powershell 有效负载与 64 位 powershell 目标不兼容，反之亦然。)生成用 c 编写的 Windows powershell 脚本(. PS1)dropper . Powershell 脚本有效负载使用 system()函数执行(Powershell-execution policy bypass-window style Hidden-no exit-File " pathtops 1 script ")。

**Wine-Pyinstaller 模块:**

(>)随机化垃圾代码和 windows 防病毒规避技术(>)执行时间范围:5-25 秒(>)需要在 wine 中安装 python 和 pyinstaller。

1.  windows winepy installer Python meter preter

纯 python meterpreter 有效负载。

1.  WinePyinstaller 单线有效载荷滴管

纯 python powershell/cmd oneliner 滴管。

使用 os.system()执行 Powershell/cmd 负载。

**LINUX 有效负载**

**Linux 外壳代码注入模块(C)**

支持 Msfvenom linux 有效负载和自定义外壳代码。

(>)随机化垃圾代码和 C 防病毒规避技术(>)多字节 Xor 编码器可用(请参见多字节 Xor 编码器自述文件部分)(>)Strip 可执行文件可用([https://en . Wikipedia . org/wiki/Strip _(Unix)](https://en.wikipedia.org/wiki/Strip_(Unix)))(>)执行时间范围:20-45 秒

1.  Linux 外壳代码注入 HeapAlloc:使用 mmap 和 memcpy 在内存中注入并执行外壳代码。
2.  Linux Bash Oneliner Dropper:使用 system()函数执行定制的 Oneliner 负载。

**OSX 有效载荷**

1.  OSX 32 位多编码:

纯 msfvenom 多编码 OSX 有效载荷。

**安卓有效载荷**

1.  Android MSF venom Apk smali/baks Mali:

(>)伪循环注入(>)Goto 循环

Android msfvenom 有效负载修改了一个用 apktool 重建的(也能进行 apk 后门注入)。

**通用有效载荷**

生成与用于运行幻影规避的操作系统兼容的可执行文件。

1.  通用仪表读数增量-技巧
2.  通用多态仪表
3.  通用多态单线滴管

**后期开发模块**

1.  这个模块生成需要上传到目标机器的可执行文件，并指定文件的完整路径作为参数添加到启动中。
2.  windows Persistence REG Add Registry Key(CMD)此模块生成持久性 cmdline 有效负载(通过 REG.exe 添加注册表项)。
3.  这个模块生成需要上传到目标机器并执行的可执行文件。使用 CreateToolSnapshoot ProcessFirst 和 ProcessNext 每 X 秒检查一次指定的进程是否处于活动状态。与 Persistence N.1 或 N.2 结合使用(Persistence start Keep process alive 文件，该文件随后启动并保持指定进程的活动状态)
4.  Windows 持久性 Schtasks 命令行

这个模块生成持久 cmdline 有效负载(使用 Schtasks.exe)。

1.  Windows 设置文件属性隐藏

通过命令行或编译的可执行文件隐藏文件(SetFileAttributes API)

**警告**

PYTHON3 兼容性暂时中止！

**诱饵处理产卵者:**

在目标端执行期间，这将导致产生(使用 WinExec 或 CreateProcess API)最多 4 个进程。最后产生的进程将到达代码的恶意部分，而之前产生的其他诱饵进程将只执行随机垃圾代码。

赞成:执行时间越长，检出率越低。CONS:更高的资源消耗。

**多字节异或编码器:**

带有三个纯 c 解码存根的 C xor 编码器可用于外壳代码注入模块。

1.  多字节异或:

外壳代码与一个多字节(可变长度)随机密钥异或。多态 C 解码器存根。

1.  双多字节密钥 xor:

外壳代码与两个多字节(可变长度)随机密钥多态 C 解码器存根之间的 xor 结果进行 xor。

1.  三重多字节密钥 xor:

外壳代码与两个多字节(可变长度)随机密钥和第三个多字节随机密钥的 xor 结果进行 xor 运算。多态 C 解码器存根。

[**Download**](https://github.com/oddcod3/Phantom-Evasion)