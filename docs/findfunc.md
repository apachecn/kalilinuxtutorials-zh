# find func:IDA Pro 中函数的高级过滤/查找

> 原文：<https://kalilinuxtutorials.com/findfunc/>

[![](img/859e5a487f31f07e589b32204959d2d4.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjsDCRDQBtgVDH6D1155BgH2gvziJhj9pMmhqi5wY-U63vDi_Fw3uFKG1pxfsqbtxppT4YDZCzqa-ExNmFdX1vA543X71UG0YjvyHk2cbc3nHxx4KnSwJkpKv_a_hxXCNZ5SYrqnajuyJitc_HuzBKSxTyNPqdCIXvBldJTVcJnpAVh1uFh4W9XrHEk/s728/Storm-Breaker-Social-engineering-tool%20(1).png)

**FindFunc** 是一个 IDA Pro 插件，用于查找包含某个汇编或字节模式，引用某个名称或字符串，或者符合各种其他约束的代码函数。这并不是 Diaphora 或 BinNavi 等工具的竞争对手，但对于经典 bindiffing 失败的情况，在新的二进制文件中找到已知函数是理想的。

## 使用规则过滤

FindFunc 的主要功能是让用户指定 IDA Pro 中的代码函数必须满足的一组“规则”或约束。FF 然后会找到并列出满足所有规则的所有函数(所以目前所有规则都在 AND-connection 中)。例外:规则可以“反转”为负匹配。这样的规则因而符合“而不”。

FF 将按照智能顺序安排规则，以最小化处理时间。功能概述:

*   目前有 6 条规则可用，见下文
*   代码匹配考虑寻址大小前缀和操作数大小前缀
*   意识到功能块
*   性能规则的智能调度
*   以简单 ascii 格式将规则从文件中保存/加载到文件中
*   用于实验的几个独立选项卡
*   通过剪贴板在选项卡之间复制规则(与文件格式相同)
*   将整个会话(所有选项卡)保存到文件
*   指令字节的高级复制(所有、仅操作码、除立即数之外的所有)

按钮“搜索功能”清除现有结果并开始新的搜索，“优化结果”仅考虑先前搜索的结果。

### 高级二进制复制

FF 的第二个特性是可以使用以下选项复制指令的二进制表示:

*   全部复制->将所有字节复制到剪贴板
*   不立即复制->空白(AA？？BB)指令字节中的任何立即值
*   仅操作码->除了指令的实际操作码(和前缀)之外，将清空所有内容

有关详细信息，请参见下面的“高级复印”部分。这个特性很好地补充了字节模式规则！

## 建筑和安装

FindFunc 是一个没有外部包依赖的 IDA Pro python 插件。它可以通过下载存储库并将文件 findfuncmain.py 和文件夹 findfunc 复制到您的 IDA Pro 插件目录来安装。不需要建筑。

要求:使用 python3 环境的 IDA Pro 7.x (7.6+)。FindFunc 仅适用于 x86/x64 架构。已经在 Windows 10 上用 IDA 7.6/7.7，python 3.9，IDAPython 7.4.0 测试过。

# 可用规则

目前有以下六条规则可用。这里按照对性能的影响从大到小对它们进行了排序。对于大型数据库，在通过例如代码规则进行大量匹配之前，首先用廉价的规则削减候选函数是一个好主意。FF 会以智能的方式自动调度规则。

### 代码模式

基于包含给定汇编代码片段的函数来过滤函数的规则。这不是 IDAs 文本反汇编表示的文本搜索，而是执行底层指令的高级匹配。该代码片段可能包含许多连续的指令，每行一条。支持函数块。除了文字汇编之外，还支持特殊通配符匹配:

*   “传递”->匹配带有任何操作数的任何指令
*   “mov* any，any”-->将指令与助记符“mov*”(例如 mov，movzx，…)和任意两个参数进行匹配。
*   “mov eax，R32”-->用助记符“mov”匹配任何指令，第一个操作数寄存器 eax，第二个操作数匹配任何 32 位寄存器。
    *   模拟:r 代表任何寄存器，r8/r16/r32/r64 代表特定宽度的寄存器，“imm”代表任何立即数
*   " mov r64，imm" ->将常量的任何移动匹配到 64 位寄存器
*   " any r64，r64" ->匹配两个 64 位寄存器之间的任何操作
*   mov ->匹配 mov 助记符的任何指令

更多示例:

**mov r64、【R32 * 8+0x 100】
mov r、【r * 8–0x 100】
mov r64、【R32 * 8+IMM】
pass
mov r、word【eax+R32 * 8–0x 100】
any r64、r64
push imm
push any**

**问题:**从 IDA 复制汇编时要小心。IDA 将局部变量名称和其他信息混合到指令中，导致匹配失败。此外，不支持标签(“call sub_123456”)。

注意，代码模式是最昂贵的规则，如果只有代码规则，FF 别无选择，只能分解整个数据库。对于非常大的二进制文件，这可能需要几分钟的时间。请参见下面的性能说明。

### 即时值(常量)

该函数必须在任何位置至少包含一次给定的立即数。立即值是固定在指令的二进制表示中的值。匹配立即值 0x100 的指令示例:

**mov eax，0x100
mov eax，【0x 100】
和 al，【eax+ebx * 8+0x 100】
推 0x100**

注意:IDA 对任何大小和任何位置的立即数执行广泛的匹配。如果你知道它有 4 或 8 个字节的特定宽度，字节模式可以快一点。

### 字节模式

该函数必须至少包含一次给定的字节模式。该模式与 IDAs 二分搜索法的格式相同，因此支持通配符——这是高级复制特性的完美匹配！

示例:

**11 22 33 44 aa bb cc
11 22 33？？？？bb cc - >？？可以是任何字节**

### 字符串引用

该函数必须引用给定的字符串至少一次。该字符串根据 pythons 的“fnmatch”模块进行匹配，因此支持类似通配符的匹配。匹配是不区分大小写的。考虑以下格式的字符串:[idaapi。STRTYPE_C，idaapi。STRTYPE_C_16](这可以在 Config 类中更改)。

示例:

*   " TestString" ->函数必须至少引用一次准确的字符串(忽略大小写)
*   " TestStr * "-->函数必须至少引用一次以" TestStr "开头的字符串(例如 TestString、TestStrong)(忽略大小写)

注意:字符串匹配速度快，是快速削减候选项的好选择！

### 姓名参考

该函数必须引用给定的名称/标签至少一次。名称/标签根据 pythons 的“fnmatch”模块进行匹配，因此支持类似通配符的匹配。匹配是不区分大小写的。

示例:

*   " memset" ->函数必须至少引用一次名为" memset "的位置
*   " mem * "-->函数必须至少引用一次以" mem" (memset，memcpy，memcmp)开头的位置

注意:名字匹配非常快，是快速削减候选人的理想选择！

### 功能大小

函数的大小必须在给定的限制范围内:“min <= functionsize <= max”。数据以“最小值，最大值”形式的字符串输入。函数的大小包括它的所有块。

注意:函数大小匹配非常快，是快速削减候选对象的理想选择！

## 键盘快捷键& GUI

为了便于使用，可以通过以下键盘快捷键使用 FF:

*   Ctrl+Alt+F ->启动/显示 TabWidget(主 GUI)
    *   或者查看->FindFunc
*   Ctrl+F ->用当前启用的规则开始搜索
*   Ctrl+R ->使用当前启用的规则优化现有结果
*   规则
    *   Ctrl+C ->将选定的规则复制到剪贴板
    *   Ctrl+V ->将剪贴板中的规则粘贴到当前选项卡中(追加)
    *   Ctrl+S ->将选定的规则保存到文件
    *   Ctrl+L ->从文件中加载选定的规则(追加)
    *   Ctrl+A ->选择所有规则
    *   删除->删除选定的规则
*   保存会话
    *   Ctrl+Shift+S ->将会话保存到文件
    *   Ctrl+Shift+L ->从文件加载会话

进一步使用 GUI

*   双击数据列可以编辑规则
*   通过双击反转匹配列，可以反转规则(负匹配)
*   双击“已启用”列可以启用/禁用规则
*   双击选项卡可以对其进行重命名
*   规则列表和结果列表都支持排序
*   双击结果项，在 IDA 中跳转到它
    *   函数名:跳转到函数开始
    *   任何其他列:跳转到最后匹配规则的匹配项
*   复选框配置文件:输出搜索的配置信息
*   Checkbox Debug:转储代码规则匹配的详细调试输出——只有在很少函数符合代码检查规则时才使用它，否则可能需要很长时间！

## 高级二进制复制

我们经常想要搜索汇编的二进制模式，但是没有硬编码的地址和值(立即数)，或者甚至只有指令的实际操作码。FindFunc 通过向反汇编弹出菜单添加三个复制选项使这变得简单:

### 复制所有字节

将所有指令字节作为十六进制字符串复制到剪贴板，用于字节模式规则(或 IDAs 二分搜索法)。

**B8 44332211 mov eax，11223344
68 00000001 推送 1000000
66:894424 70 mov word ptr ss:[esp+70]，ax**

### 仅复制非立即字节

复制给定指令的指令字节，屏蔽掉任何立即值。示例:

**B8 44332211 mov eax，11223344
68 00000001 推送 1000000
66:894424 70 mov word ptr ss:[esp+70]，ax**

[**Download**](https://github.com/FelixBer/FindFunc)