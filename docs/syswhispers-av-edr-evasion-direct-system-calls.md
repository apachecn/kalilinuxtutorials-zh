# 通过直接系统调用规避反病毒/EDR

> 原文：<https://kalilinuxtutorials.com/syswhispers-av-edr-evasion-direct-system-calls/>

[![SysWhispers  : AV/EDR Evasion Via Direct System Calls](img/871340c1c468a0ba4a09ea5a7740de00.png "SysWhispers  : AV/EDR Evasion Via Direct System Calls")](https://1.bp.blogspot.com/-GH8lP4lZ4HQ/XhHqwrcgmVI/AAAAAAAAEQo/uUybemNjmcQPttf5wgzobgCOCXH6GsN-gCLcBGAsYHQ/s1600/Malware%25281%2529.png)

**SysWhispers** 通过生成植入程序可以用来进行直接系统调用的头文件/ASM 文件来帮助规避。从 Windows XP 到 10 都支持所有核心系统调用。在`**example-output/**`中可以找到生成文件的例子。

各种安全产品在用户模式 API 中放置挂钩，允许它们将执行流重定向到它们的引擎，并检测可疑行为。`**ntdll.dll**`中进行系统调用的函数仅由几条汇编指令组成，因此在您自己的植入物中重新实现它们可以绕过那些安全产品挂钩的触发。这项技术由 [@Cn33liz](https://twitter.com/Cneelis) 推广，他的[博文](https://outflank.nl/blog/2019/06/19/red-team-tactics-combining-direct-system-calls-and-srdi-to-bypass-av-edr/)有更多技术细节值得一读。

SysWhispers 为 red teamers 提供了在从 XP 开始的任何 Windows 版本的核心内核映像(`**ntoskrnl.exe**`)中为任何系统调用生成 header/ASM 对的能力。标头还将包括必要的类型定义。

这与 [Dumpert](https://github.com/outflanknl/Dumpert) POC 的主要实现区别在于，它不调用`**RtlGetVersion**`来查询操作系统版本，而是在汇编中通过直接查询 PEB 来完成。好处是能够调用一个支持多个 Windows 版本的函数，而不是调用多个支持一个版本的函数。

**安装**

git 克隆 https://github.com/jthuraisamy/SysWhispers.git
CD SysWhispers
pip 3 install-r . \ requirements . txt
py。\ sys whispers . py–help

**用法&举例**

**#导出兼容所有支持的 Windows 版本的所有功能(参见示例-输出/)。**T2 py。\ sys whispers . py–预置 all-o syscalls _ all

**#只导出兼容 Windows 7、8、10 的常用函数。**
py。\ sys whispers . py–预置 common-o syscalls _ common

**#导出兼容所有版本的 NtProtectVirtualMemory 和 NtWriteVirtualMemory。**
py。\ sys whispers . py–functions NtProtectVirtualMemory，NtWriteVirtualMemory-o sys calls _ mem

**#导出兼容 Windows 7、8、10 的所有函数。**
py。\ sys whispers . py–版本 7、8、10 -o syscalls_78X

**常用功能**

使用`**--preset common**`开关将创建具有以下功能的集管/ASM 对:点击展开功能列表。

**导入到 Visual Studio 中**

*   将生成的 H/ASM 文件复制到项目文件夹中。
*   在 Visual Studio 中，转到“项目”→“生成自定义项”…,然后启用 MASM。
*   在解决方案资源管理器中，添加。h 和。asm 文件分别作为头文件和源文件添加到项目中。
*   转到 ASM 文件的属性，将项目类型设置为 Microsoft Macro Assembler。
*   确保项目平台设置为 x64。目前不支持 32 位项目。

**注意事项&限制**

*   目前仅支持 64 位 Windows。
*   不支持来自图形子系统(`win32k.sys`)的系统调用。
*   在装有 Windows 10 SDK 的 Visual Studio 2019 (v142)上测试。

**故障排除**

*   `**ModuleNotFoundError**`在 Python 脚本中。
    *   确保所需模块安装有 **`pip3 install -r requirements.txt`。**
*   类型重新定义错误:如果已经定义了`**syscalls.h**`中的类型定义，项目可能无法编译。
    *   确保只包含必需的功能(即`**--preset all**`很少是必需的)。
    *   如果一个 typedef 已经在另一个使用的头中定义，那么它可以从`**syscalls.h**`中删除。

[**Download**](https://github.com/jthuraisamy/SysWhispers)