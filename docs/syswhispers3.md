# SysWhispers3:通过直接系统调用进行反病毒/EDR 规避

> 原文：<https://kalilinuxtutorials.com/syswhispers3/>

[![](img/6edb6232413cc20d750cdf61f3228ad0.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjsqFVTUF8smclFjw9VWXuTCSKANSKOcCslMPUMyPYvi9Dyj-v5-i7wi4RIlUyQ-X9g6s990GUl9lsZSXFJmc1ogQTagzP594c-ttRWyEjJtG0cxscfzQqB_Ye6xtcPVF5c1rZw2KvU-1-DyMUzNQOHj2asFvAMdrFAPXTtjpzbBvki6FHbHBym-o9W/s728/av%20(1).png)

SysWhispers 通过生成植入程序可以用来进行直接系统调用的头文件/ASM 文件来帮助规避。

### 我到底为什么没有给 SysWhispers2 创建一个 PR？

SysWhispers3 成为独立版本的原因有很多，但最重要的是:

*   SysWhispers3 是 Inceptor 使用的事实上的“fork ”,它实现了一些与工具原始版本无关的 utils 类。
*   SysWhispers2 正朝着支持 NASM 编译(用于 gcc/mingw)的方向发展，而这个版本是专门为支持 MSVC 而设计和测试的(因为 Inceptor 在不久的将来仍将是一个仅支持 Windows 的框架)。
*   SysWhispers3 包含了部分实现的特性(比如寻蛋),在这个工具的原始版本中包含这些特性是不明智的。

## 与 SysWhispers 的区别 2

用法与 SysWhispers2 非常相似，但有以下例外:

*   它还支持 x86/WoW64
*   它支持用 EGG 替换 syscalls 指令(被动态替换)
*   它支持直接跳转到 x86/x64 模式的系统调用(在 WOW64 中这几乎是标准的)
*   它支持直接跳转到随机的系统调用(借用@ElephantSeal 的想法)

如果博客文章《系统低语死了，系统低语万岁》能更好地解释这些特性。

## 简介

安全产品，如 AVs 和 EDRs，通常在用户模式 API 函数中放置钩子来分析程序执行流，以便检测潜在的恶意活动。

SysWhispers2 是一个工具，旨在为核心内核映像(`**ntoskrnl.exe**`)中的任何系统调用生成 header/ASM 对，然后可以集成并直接从 C/C++代码中调用，从而避开用户登陆挂钩。

然而，该工具生成一些可以包含在签名中的模式，或者可以在运行时检测到的行为。

SysWhispers3 构建于 SysWhispers2 之上，集成了一些有用的功能来绕过这些形式的检测。

## 安装

**C: > git 克隆 https://github.com/klezVirus/SysWhispers3.git
C:>CD syswhispers 3
C:>python。\ sys whispers . py–help**

## 用法和示例

帮助显示了该工具的所有可用命令和功能:

**C:>python sys whispers . py-h
用法:sys whispers . py[-h][-p PRESET][-a { x86，x64}] [-m {embedded，egg_hunter，jumper，jumper _ randomized }][-f FUNCTIONS]-o OUT _ FILE[–int2eh][–wow 64][-v][-d]
SysWhispers 3–SysWhispers on steroids
可选参数:
-h，–help 显示此帮助信息并退出
–FUNCTIONS 函数
逗号分隔函数
-o OUT_FILE，–OUT-FILE OUT _ FILE
输出 basename(不带扩展名)
–int2eh 使用旧的`int 2eh`指令代替`syscall`
–wow64 使用 wow 64 在 x64 上运行 x86(仅可用于 x86 架构)
-v，–详细启用调试输出
-d，–debug 启用 syscall 调试(插入软件断点)**

### 命令行

#### 标准 SysWhispers，嵌入式系统调用(x64)

**导出兼容所有支持的 Windows 版本的所有功能(参见示例-输出/)。
py。\ sys whispers . py–预置 all -o syscalls_all
只导出常用函数(列表见下)。
py。\ sys whispers . py–预置 common -o syscalls_common
导出兼容所有版本的 NtProtectVirtualMemory 和 NtWriteVirtualMemory。
py。\ sys whispers . py–函数 NtProtectVirtualMemory，NtWriteVirtualMemory-o syscalls _ mem**

## 仅限 SysWhispers3 的示例

**正常 SysWhispers，32 位模式
py。\ syswhispers . py–预置 all -o syscalls_all -m 跳线–arch x86
正常 sys whispers，使用 32 位模式 WOW64(仅限特定函数)
py。\ sys whispers . py–函数 NtProtectVirtualMemory，NtWriteVirtualMemory-o sys calls _ mem–arch x86–wow 64
寻蛋 syswhispers，绕过“sycall 的标记”(常用函数)
py。\ syswhispers . py–预设 common-o sys calls _ common-m jumper
跳转/跳转随机化的 sys whispers，使用 MinGW 作为编译器
py 来绕过动态 RIP 验证(所有函数)。\ sys whispers . py–预置 all-o syscalls _ all-m jumper-c mingw**

## 脚本输出

**PS C:\ Projects \ syswhispers 2>py。\ sys whispers . py–预置 common–out-file temp \ sys calls _ common-v .，–
，-。。。,-.。, , |-.哦，-。,-.,-.,-.,-. *_/ `-. | |` -。|/|/| |`-. | | |-' |`-。。\`-'`-|`-' ' ' ' ' '`-' |-'`-' '`-' " '/| | @ Jackson _ T `-' ' @ modexpblog，2021 编辑 by @klezVirus，2022 SysWhispers3:能小声说话为什么要调用内核？已选择常用功能。完整！文件写入:temp \ syscalls _ common . h temp \ syscalls _ common . c temp \ syscalls _ common*。asm
按键继续…**

## 导入到 Visual Studio

*   将生成的 H/C/ASM 文件复制到项目文件夹中。
*   在 Visual Studio 中，转到*项目* → *构建定制…* 并启用 MASM。
*   在*解决方案浏览器*中，添加。h 和。c/。asm 文件分别作为头文件和源文件添加到项目中。
*   转到 ASM 文件的属性，将*项类型*设置为*微软宏汇编器*。

## 在 Visual Studio 之外编译

### Windows

64 位的 Makefile:

`**Makefile.msvc**`

**OPTIONS =-Zp8-c-no logo-Gy-Os-O1-GR--EHa-Oi-GS-
LIBS = libvcruntime . lib libc mt . lib ucrt . lib kernel 32 . lib 程序:
ML64/c syscalls-ASM . X64 . ASM/link/NODEFAULTLIB/RELEASE/MACHINE:X64
cl.exe $(OPTIONS)syscalls . c program . c
link.exe/OUT:program . X64 . exe-no logo $。**

用 nmake 编译:

**nmake****-f makefile . msvc**

### Linux 操作系统

64 位和 32 位的 Makefile:

`**Makefile.mingw**`

**CC _ x64:= x86 _ 64-w64-mingw 32-gcc
CC _ x86:= i686-w64-mingw 32-gcc
选项:= -masm=intel -Wall
程序:
$(CC_x64) syscalls.c 程序. c-o program.x64.exe $(选项)
$(CC_x86) syscalls.c 程序. c-o program.x86.exe $(选项)**

## 警告和限制

*   Egg-Hunter 功能没有在这个工具中实现，它在 Inceptor 中。
*   不支持来自图形子系统(`**win32k.sys**`)的系统调用。
*   在装有 Windows 10 SDK 的 Visual Studio 2019/2022 上测试。
*   对 NASM 的支持没有保证。
*   对海湾合作委员会和 MinGW 的支持没有保证。

[**Download**](https://github.com/klezVirus/SysWhispers3#importing-into-visual-studio)