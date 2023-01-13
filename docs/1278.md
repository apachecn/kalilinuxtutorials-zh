# AngrgDB:在 gDB 境内使用 Angr

> 原文：<https://kalilinuxtutorials.com/angrgdb/>

[![AngrgDB : Use Angr Inside GDB](img/133d5212928b9baedbf512c8a58375a1.png "AngrgDB : Use Angr Inside GDB")](https://1.bp.blogspot.com/-MoGDhw-R6Pk/XpMgIGVeyDI/AAAAAAAAF3k/NTJ8TlFLF30Q0TFfIfj0RV4YlDJ6wfhRQCLcBGAsYHQ/s1600/Angr%25281%2529.png)

在 gDB 境内使用 angr。从当前调试器状态创建一个 angr 状态。

**安装**

**pip 安装 angrgdb
echo "python 导入 angrgdb.commands" > > ~/。gdbinit**

**用途**

AngrgDB 在 gDB 实现了 [angrdbg](https://github.com/andreafioraldi/angrdbg) API。

您可以在如下脚本中使用它:

from angrgdb import *

gdb . execute(" b * 0x 004005 F9 ")
gdb . execute(" r aaaaaaaaaa ")

sm = state manager()
sm . sim(sm[" rax "]，100)

m = sm . simulation _ manager()
m . explore(find = 0x 004000607，avoid = 0x 004000613)

sm . to _ dbg(m . found[m 那是秘密钥匙！

您也可以在 gdb 直接使用 angrgdb 命令进行简单的操作:

*   象征一个寄存器
*   `**angrgdb sim <address> [size]**`象征一个记忆区域
*   列出你设定为象征性的所有项目
*   `**angrgdb find <address0> <address1> ... <addressN>**`设置查找目标的列表
*   `**angrgdb avoid <address0> <address1> ... <addressN>**`设置避开目标的列表
*   `**angrgdb reset**`重置上下文(符号值和目标)
*   `**angrgdb run**`从调试器状态生成一个状态并运行探索
*   使用从当前 GDB 状态创建的 StateManager 实例打开一个 shell
*   从调试器状态生成一个状态，并使用修改后的 [angr-cli](https://github.com/fmagin/angr-cli) 手动探索

使用 angrgdb+GEF+ [idb2gdb](https://github.com/andreafioraldi/idb2gdb) 的示例 crackme solve:

[![](img/8cae0a800ccb97aac1a8f4773ea3851c.png)](https://asciinema.org/a/207571)

**在 GDB 加载脚本**

如果您不想从 cli 使用 angrgdb，但想使用 python 脚本，这是一个提示。要在 GDB 加载脚本，请使用 **`source script.py`。**

**待办事项**

*   像在 IDAngr 中一样添加远程 angrdbg