# FirmWire : b 全系统基带固件仿真平台

> 原文：<https://kalilinuxtutorials.com/firmwire/>

[![](img/bc28df3bea5e10623bfb4f5bd5d2ece9.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEioSZODw_a40Y807Z72wmquiKgih1oxIzF3sAGwlkQsq6pXv6sCQHDP7yLEJnQf9xtrcTHv2P3pcQzWn_l8iESBqlBx7dlmNJiGp94kx5JMtnJ7hHerXz0cT3IlhcrxqwFmwlBTahP6NtQxEx69SZNrDl-6lKg9AncfyIGl9gX8CBTK3cVBrH7SiTUA/s728/l9pemtcsp9s41.png)

**FirmWire** 是支持三星和联发科的全系统基带固件分析平台。它支持基带固件映像的模糊化、根本原因分析和调试。**见 FirmWire 文档开始！**

# 装置

使用 FirmWire 的推荐方法是使用提供的 Dockerfile 文件。要构建 docker 文件，请执行以下命令:

**git 克隆 https://github.com/FirmWire/FirmWire.git
CD 固件
git 克隆 https://github.com/FirmWire/panda.git
这需要一些时间
docker build -t 固件**。

然后，您可以通过执行以下命令获得安装了 FirmWire 的 docker 环境的交互式 shell:

**docker run–RM-it-v $(pwd):/firm wire firm wire**

从这里，您可以直接查看我们的快速入门文档来模拟您的第一个调制解调器！

## Visual Studio 代码

除了从命令行使用 docker 之外，您还可以通过使用`**devcontainer**`和`**docker**`扩展，使用 VScode 创建一个 FirmWire 环境。克隆完 FirmWire 和 FirmWire 的熊猫版本后，只需在代码中打开相应的目录，执行:`**> Remote-Containers: Add Development Container Configuration Files**`，然后选择`**From Dockerfile**`，应该会自动创建一个`**.devcontainer**`文件。之后，按照代码的提示进入 **`Reopen in container`。**

这将构建 docker 容器，并在 docker 环境中为您提供一个交互式 shell，文件透明地转发到主机目录。这是一些 FirmWire 开发人员最喜欢的开发设置！

## 手动安装

FirmWire 的手动安装有点繁琐。除了安装 FirmWire 及其要求，您还需要:

*   手动构建熊猫
*   安装 PyPanda
*   手动构建固件

有关如何执行这些单独步骤的信息，请参考文档。

# 快速启动

你已经安装了 FirmWire 并且渴望模仿你的调制解调器 FirmWire 吗？非常好！安装后您只需运行:

**$。/firmwire.py modem.bin**

这将自动识别固件，将其解包，并选择一个加载程序和机器来运行它。您也可以从 URL 加载固件来开始:

**$。/firm wire . py https://github . com/grant-h/Shannon firmware/raw/master/modem _ files/CP _ g 973 FX Xu 3 ASG 8 _ CP 13372649 _ cl 16487963 _ QB 24948473 _ rev 01 _ user _ low _ ship . tar . MD5 . lz4**

目前，FirmWire 支持联发科 MTK 和三星香农固件映像的子集。

请注意，FirmWire 需要几个不同的 TCP 端口才能运行。如果您对可以使用的端口有任何限制，请使用`**--consecutive-ports**`标志来指定可以使用的端口。例如，如果您的系统可以自由使用端口 10000-10005，请按如下方式调用 FirmWire:

**$。/firm wire . py–连续端口 10000 调制解调器. bin**

## 支持的图像

### 联发科

*   三星 A10s (MT6762)
*   三星 A41 (MT6768)

### 香农河

*   Galaxy S7、S7e 的大多数图像(S335)
*   Moto One Vision (S337)
*   银河 S8、S8+ (S355)
*   银河 S9 (S360)
*   银河 S10，S10e (S5000)

## 使用 Ghidra

如果您正在分析**联发科固件**，我们有 Ghidra 的定制补丁。有关设置说明，请参见 https://github.com/FirmWire/ghidra。关于**香农固件**见 https://github . com/grant-h/Shannon baseband #入门-香农固件。您将需要 ShannonLoader，它可以安装在联发科的定制 Ghidra 上(或者只使用上游 Ghidra)。

# 技术背景

FirmWire 是一个基带分析平台。作为输入，它获取一个基带固件映像，并尝试动态地为该映像创建一个仿真环境。

# 仿真核心

FirmWire 的仿真核心建立在 avatar2 和 PANDA 之上。核心仿真功能由 PANDA 提供，而 avatar2 被用作中间件来编排仿真器的执行状态，包括启动、断点注册和启动/停止仿真。此外，我们使用 avatar2 的 Python 外设来实现对内存映射 I/O 访问做出反应的外设。

在幕后，FirmWire 实现了供应商特定的*机器*，这些机器使用 avatar2 的 PyPanda 目标将 Panda 作为动态库嵌入到与 Python 解释器相同的进程空间中，从而将 FirmWire 所需的进程间通信保持在最低限度。

# 仿真器配置

PANDA 和 avatar2 使用所谓的`**configurable machine**`来模拟带有自定义内存映射的任意嵌入式系统。本质上，嵌入式系统的内存映射(包括 ROM、RAM 和外设)是在一个 JSON 文件中描述的，该文件由 avatar2 根据单独注册的内存范围自动生成。这个 JSON 文件然后被传递给 PANDA，PANDA 用它来注册和模拟相应的内存范围。

在 FirmWire 内部，我们使用可配置的机器动态创建目标基带镜像的仿真环境。更详细地说，我们的加载程序负责解析二进制固件文件，并自动提取所需的内存映射，例如通过在二进制映像中查找预定义的 MPU 表。

# 本手册

本手册的其余部分将从用户的角度指导您使用 FirmWire。如果你对开发或扩展 FirmWire 的核心功能感兴趣，请继续关注。或者，您可以深入研究源代码，或者联系我们——我们很乐意在任何需要的地方提供更多信息！

# 命令行界面参考

我们文档的这一部分是所有`**firmwire.py**`和`**firmwire_dev.py**` CLI 参数的快速参考，并提供了它们的相关链接。有关单个命令行标志的更多信息，您也可以运行带有`**--help**`标志的 FirmWire。

## firmwire.py 参数

| 争吵 | 覆盖着 | 描述 |
| --- | --- | --- |
| `**modem_file**` | 入门指南 | 调制解调器文件 FirmWire 应创建一个仿真环境。只有强制参数(！) |
| `**--consecutive-ports CONSECUTIVE_PORTS**` | 入门指南 | 从提供的端口开始，为任何监听套接字选择连续的端口(例如 QEMU 的 GDB & QMP)。 |
| `**-h/--help**` | CLI 参考 | 在命令行上显示不同 cli 标志的帮助 |
| `**-w/--workspace WORKSPACE**` | 工作区 | 要使用的工作空间的路径 |
| `**--snapshot-at SNAPSHOT_AT**` | 工作区 | 拍摄快照的地址和名称。(语法:地址，名称) |
| `**--restore-snapshot SNAPSHOT_NAME**` | 工作区 | 要恢复的快照的名称 |
| `**-t/--module INJECTED_TASK**` | 模块套件 | 要注入基带调制解调器的模块/任务 |
| `**-S/--stop**` | 互动探索 | 初始化机器后停止 CPU。对互动探索有用。 |
| `**-s/--gdb-server**` | 互动探索 | 在 TCP 端口上启动 GDB 服务器。默认值为 1234。注意:这是一个最小的 GDB 存根。 |
| `**--console**` | 互动探索 | 生成一个 ipython 远程内核，可以使用`**jupyter console --existing**`从另一个终端连接到该内核 |
| `**--fuzz FUZZ**` | 起毛 | 注入并调用传递的 AFL 模糊任务模块(headless)。 |
| `**--fuzz-input FUZZ_INPUT**` | 起毛 | AFL 测试用例的路径(@@应该足够了)或者只是一个测试文件的路径。 |
| `**--fuzz-triage FUZZ_TRIAGE**` | 起毛 | 调用 fuzzer，但是没有 AFL 前端。启用调试挂钩并保存代码覆盖率。 |
| `**--fuzz-persistent FUZZ_PERSISTENT**` | 起毛 | 使用循环计数作为参数启用持续模糊化。 |
| `**--fuzz-crashlog-dir FUZZ_CRASHLOG_DIR**` | 起毛 | 持久模式下崩溃运行的所有测试用例(长度测试用例)的日志所在的文件夹 |
| `**--fuzz-crashlog-replay FUZZ_CRASHLOG_REPLAY**` | 起毛 | 重放用 fuzz-crashcase-dir 编写的持久模式崩溃跟踪。 |
| `**--fuzz-state-addr-file FUZZ_STATE_ADDR_FILE**` | 起毛 | 包含状态变量十六进制地址的文本文件 |
| `**--full-coverage**` | 起毛 | 启用*完全*覆盖收集(记录每个执行的基本块) |
| `**--shannon-loader-nv_data NV_DATA**` | TBD | (仅 Shannon)指定要使用的 NV_DATA |
| `**--mtk-loader-nv_data NV_DATA**` | TBD | (仅限联发科)指定要使用的 NV_DATA |

## 开发者选项

注意:这些参数对于开发和调试非常有用。到目前为止，它们是`**firmwire.py**`的一部分，但是在 FirmWire 的未来版本中，它们将被转移到一个定制的`**firmwire_dev.py**`界面中，以清楚地区分开发者和用户的特性。

| 争吵 | 覆盖着 | 描述 |
| --- | --- | --- |
| `**--debug**` | TBD | 启用固件调试 |
| `**--debug-peripheral**` | TBD | 为指定的外围设备启用调试 |
| `**--avatar-debug**` | TBD | 启用 Avatar2 的调试日志记录 |
| `**--avatar-debug-memory**` | TBD | 启用 Avatar2 远程内存调试(外设崩溃时有用) |
| `**--unassigned-access-log**` | TBD | 当内存访问未定义的内存时，打印日志消息 |
| `**--raw-asm-logging**` | TBD | QEMU 执行汇编基本块时打印它们。用于确定无限循环。 |
| `**--trace-bb-translation**` | TBD | 打印每个新基本块的地址，对 fuzzing 期间到达的 eval BBs 有用。 |

# 工作区

FirmWire 使用与正在分析的特定固件文件相关的工作空间。这些工作区包含各种有用的文件，最显著的是 avatar2-orchestration 发出的日志、可配置的机器定义和用于 FirmWire 快照机制的 qcow2-image，以及特定于供应商的文件和目录。

默认情况下，FirmWire 在调制解调器文件所在的同一目录下创建一个工作区，但是这种行为可以通过`**-w/--workspace**`命令行标志来覆盖。

## 快照

FirmWire 的便利特性之一是快照，它是在 QEMU 之上实现的。FirmWire 除了以 QEMU 的`**qcow2**`镜像格式保存仿真机状态外，还将使用的 python 外设的状态保存在辅助**T1 f**文件中。

要拍摄快照，请使用`**--snapshot-at**`命令行参数或在交互式探索过程中调用`**snapshot()**`方法。假设您想要在地址`**0x464d5752**`拍摄名为`**my_first_snapshot**`的快照。要从命令行获取快照，只需运行`**./firmwire.py --snapshot-at 0x464d5752,my_first_snapshot modem_file**`。当使用交互式探索时，您可以通过`**self**`直接访问 python `**machine**`对象。确保在期望的地址停止执行(例如通过设置断点)，然后执行:`**self.snapshot("my_first_snapshot")**`。或者，如果不想手动转向执行，也可以使用 **`self.snapshot_state_at_address(0x464d5752, "my_first_snapshot")`。**

为了在 FirmWire 的下一次启动期间从该快照开始执行，您只需要`**./firmwire.py --restore-snapshot my_first_snapshot modem_file**`。如果您使用交互式探索，您甚至可以即时恢复快照，而无需重新启动模拟器！在这种情况下，您需要执行`**self.restore_snapshot("my_first_snapshot")**`

# 模式 b

PatternDB 是一种定义内存模式的方便方法，FirmWire 使用它在加载时扫描二进制基带固件。你可以把 FirmWire 内存模式看作是为固件分析任务定制的二进制正则表达式。一旦发现一个模式，FirmWire 就将一个符号与相应的模式相关联(在最简单的情况下)，并且可选地执行查找和后查找功能。模式本身在不同厂商插件中的`**pattern.py**`-文件中定义。

PatternDB 用在 FirmWire 内部的不同地方:在加载时查找 MPU 表，自动解析日志功能，或者将符号导出到 Modkit，这里仅提供几个例子。在 FirmWire 公开发布时，我们为基于 Shannon 的调制解调器提供了 18 种模式，为基于 MediaTek 的调制解调器提供了 9 种模式，并在各种固件映像上进行了测试。

## 模式语法

在我们的论文中，我们将模式的语法正式定义如下:

**模式:= {
名称:=字符串
模式:= [ PatternSyntax… ]
查找:= PatternFn？
post_lookup := PatternFn？
必选:= bool？
for := [ string… ]？
within := [ AddressSet… ]？
偏移量:=整数？
offset_end := integer？
align := integer？
}
pattern syntax:=
r "([a-fA-F0-9]{ 2 } |([？][?+*])+"
pattern fn:= code
address set:= symbol name | address range
symbol name:= string
address range:=[integer，integer]**

但这实际上意味着什么呢？让我们考虑一下来自香农`**pattern.py**`的以下模式:

**" boot _ setup _ memory ":{
" pattern ":[
" 00008004 200 c 0000 "，
"00000004？？？？0100 "、
、
、【偏移量】:-0x14、
、【align】:4、
、【post _ lookup】:handlers . parse _ memory _ table、
、【必选】:True、
}** 、

在这里，我们定义了两个模式，用于创建 PatternDB 符号`**boot_setup_memory**`，使用小端编码中搜索到的字节的十六进制符号。注意，第二种模式包括`**??**`符号——这些基本上是通配符，允许我们匹配任意字节。用`**??**`指定的通配符字节允许常规正则表达式中已知的修饰符(双关语！).`**?+**`要求存在一个或多个通配符字节，而`**?***`允许在给定位置存在零个或多个通配符字节以产生匹配。

回到我们的示例模式，如由`**offset**`参数所指定的，与`**boot_setup_memory**`符号相关联的实际地址将是在找到的模式的位置之前的 0x14 *。 **`Alignement`** 定义了搜索粒度应该是 4 字节对齐的，`**required**`将导致 FirmWire 在没有找到该模式的情况下立即退出，因为这对于仿真环境的生成至关重要。最后，post_lookup 函数引用一个在查找完成后要执行的 python 函数。这个特定后查找函数的函数签名如下:*

d **ef parse_memory_table(self，sym，data，offset):**

这里，`**self**`是对 ShannonMachine 的引用，`**sym**`是对 PatternDB 符号的引用，`**data**`是搜索的内存，`**offset**`是考虑到`**data**`块的*虚拟*位置的搜索的起始偏移量。另一方面，patternDB 符号`**sym**`包含关于地址、名称和符号类型的信息。

## 模式关键字详细信息

| 关键字 | 描述 |
| --- | --- |
| 名字 | 模式的名称和结果符号(字符串) |
| 模式 | 将产生匹配结果的一个或多个记忆模式。 |
| 检查 | 代替模式使用的函数。参数是要搜索的数据块和开始的偏移量。期望返回表示地址的`**None**`或整数。 |
| 后期查找 | 匹配成功后要执行的函数。参数在上面的示例中进行了描述。预期成功时返回`**True**`，否则返回 **`False`。** |
| 需要 | 当设置为`**True**`时，如果没有找到匹配，FirmWire 将不会继续执行。 |
| 为 | 指定 SoC 版本，以防仅针对特定 SoC 版本查找符号。 |
| 在…之内 | 在具有现有符号的图像上，指定在哪个函数中查找该模式。 |
| 抵消 | 匹配模式和创建符号的地址之间的偏移量。 |
| 偏移 _ 结束 | 与 offset 相同，但从匹配模式的结尾开始计算，而不是从开始计算。 |
| 排列 | 找到的匹配项需要内存对齐。 |

## 定义你自己的模式

你想定义你自己的模式？太好了！只需在相应的供应商插件中扩展`**pattern.py**`文件以包含您的模式，在 FirmWire 的下一次启动期间，应该会自动对其进行扫描。

# 模块套件

FirmWire 的核心特性之一是它的 modkit，它允许创建和编译自己的模块和任务，以注入到仿真基带镜像中。modkit 是我们 fuzzing 模块的基础，也是 GuestLink 交互式探索功能的基础。

简而言之，mod 是 C 程序，它使用 patternDB 创建的符号和供应商特定的加载程序来扩展现有基带固件映像的功能。这些 C 程序需要使用我们提供的 Makefiles 进行预编译。然后，FirmWire 可以在运行时注入这些任务，自动解析符号并将任务放在一个未使用的内存段中。

## 工具链和编译

为了编译任务，需要目标特定的编译工具链。对于 Ubuntu 20.04 系统，我们成功地使用了发行版的包存储库提供的以下工具链:`**gcc-9-mipsel-linux-gnu**`用于基于联发科的固件，而`**gcc-arm-none-eabi**`用于香农基带固件。

安装工具链后，可以通过浏览 modkit 目录并在供应商特定的子目录中运行`**make**`(即`**mtk**`和`**shannon**`)来编译模块。

如果您想扩展 modkit 并提供您自己的 mod，您将需要调整 Makefile。特别是，您需要修改`**MODS**`行，并提供到您的 mod 源代码的路径。为了举例说明这一点，让我们假设您想要将`**mymod**`添加到可用于仿真 Shannon 调制解调器的 mod 中。

在修改之前，Makefile 中的相关部分应该如下所示:

**MODS:= GSM _ mm GSM _ sm GSM _ cc LTE _ RRC glink〖t1〗GSM _ mm _ src:= fuzzers/GSM _ mm . c AFL . c〖T2〗GSM _ cc _ src:= fuzzors/GSM _ cc . c AFL . c〖T3〗GSM _ sm _ src:= fuzzers/GSM _ sm . c AFL . c〖T4〗LTE _ RRR**

# Modkit 格式

为了进一步举例说明如何使用 modkit，让我们看一个非常基本的任务:MTK 基带的`**hello_world**`任务。

该任务的源代码如下所示:

**include
include
include
mod kit _ FUNCTION _ SYMBOL(void，dhl_print_string，int，int，char *)
extern void real _ main(){
while(1){
DHL _ print _ string(2，0，0，" hello world \ n ")；
}
}**

代码并不多，不是吗？让我们过一遍台词。第一个包括导入 MediaTek 任务逻辑，这是确保我们的代码正确嵌入所必需的，遵循特定于基带的任务结构。类似地，第二行包括高级 modkit 功能。

这里唯一重要的一行是任务名称的说明，它被设置为 **`testtask`。**

回到`**hello_world.c**`，第五行是事情变得有趣的地方:

**MODKIT_FUNCTION_SYMBOL(void，dhl_print_string，int，int，int，char *)**

该指令用于建议 modkit“解决”属于原始调制解调器固件一部分的功能。它的一般语法是:

**mod kit _ FUNCTION _ SYMBOL(return _ type，function_name，type_argument1，type_argument2，…，type_argumentN)**

使用该指令后，C 程序可以使用所选的函数，因此在这种情况下，我们可以在代码的后面使用`**dhl_print_string**`，它用于提供日志输出。

代码的下一部分定义了`**real_main()**`函数，MediaTek modkit 使用该函数来评估该任务应该从哪里开始执行(在 Shannon mods 的情况下，对应的函数名应该是`**task_main**`)。这个主函数除了使用已解析的`**dhl_print_string**`函数将“Hello World”重复打印到控制台之外，什么也不做。整洁！

# 运行任务

为注入的任务提供代码只是第一步；当然，我们也想经营它。幸运的是，除了运行`**make**`，FirmWire 自动化了注入任务的全过程。一旦通过`**make**`构建，我们可以很容易地调用带有`**-t/--module**`标志的 FirmWire。

# 互动探索

FirmWire 有多种方式来促进仿真基带固件的交互探索。这种探索的原因是多方面的，从帮助静态逆向工程到观察接收自定义消息时基带的行为，再到崩溃输入的根本原因分析。

## 基因组数据库

与仿真基带交互的最经典方式是通过 GDB。只需用`**-s/--gdb-server**`标志启动 FirmWire，同时指定一个端口号来启动 gdb 服务器！然后，您可以启动您的本地 gdb 构建(对于 Ubuntu 20.04，我们推荐使用`**gdb-multiarch**`)并通过在 gdb 中执行以下命令连接到仿真基带:

**目标远程:端口**

或者，当 gdb 和 gef 一起使用时，我们建议运行以下代码以获得更好的可用性:

**全球环境基金-远程-QEMU-模式 127.0.0.1:端口**

一旦连接上，您应该能够设置断点、检查和修改内存，以及像往常一样控制执行。在幕后，FirmWire 产生了一个由相应的 avatar2 插件提供的 gdb 服务器。这允许透明地访问由 avatar 支持的内存范围提供的内存(如 python 外设的情况)，以及由 PANDA 提供的模拟内存。

此外，通过 gdb 的`**monitor**`命令，您可以直接访问 avatar2 gdb 服务器的 Python 上下文，并允许您执行简单的 Python 语句。您甚至可以通过执行以下命令从 gdb 访问全局头像对象:

**监控自己的头像**

# 起毛

FirmWire 的核心贡献之一是能够使用专门的模糊任务来模糊仿真基带镜像。这些任务是使用我们的 modkit 创建的，并使用 triforce-afl hypercalls 与 fuzzer、AFL++进行通信。

注入任务和虚拟化调用的结合允许透明的现代模糊化:模糊化任务将从模糊化器获得输入，然后将其作为*消息*发送给目标任务。对于目标任务，以这种方式接收的输入看起来像是通过通常的渠道到达的良性输入。

FirmWire 提供了一些模糊化任务的例子，在我们的论文评估中使用了这些例子。

首先，`**shannon.h**`被包括进来以提供香农特有的便利函数(例如`**uart_puts**`和 **`pal_MemAlloc` )** 。然后，包含了`**afl.h**`，它提供了 fuzzing 的主要功能和 API。该 API 是 TriforceAFL 提供的 API 的一个略微修改的版本，并提供以下四个功能:

| 功能 | 目的 |
| --- | --- |
| `**char * getWork(unsigned int *sizep)**` | 返回一个带有模糊输入的缓冲区，并将输入大小存储到`**sizep**`中。 |
| `**int startWork(unsigned int start, unsigned int end)**` | 开始模糊化执行，同时收集驻留在`**start**`和`**end**`之间的代码的覆盖率。 |
| `**int doneWork(int val)**` | 标记模糊化迭代的结束，将`**val**`作为返回代码提供给模糊化器。 |
| `**int startForkserver(int ticks)**` | 启动 AFL forkserver。`**ticks**`控制是否启用 qemu ticks。 |

正如我们所看到的，这个逻辑需要两个额外的函数:`**fuzz_single_setup**`和`**fuzz_single**`，这两个函数都需要由我们的线束提供。第一个函数负责所有特定于任务的设置。在`**gsm_cc**`的情况下，这意味着(1)解析 CC 的 queueID，(2)创建包含正确 msgGroup ID 的`q**item_cc**`内存块以启动任务初始化，以及(3)将内存块作为消息发送到相应的队列。

# 奖杯墙

FirmWire 旨在作为一种工具来发现安全关键缺陷，并简化基带特定的研究。因此，我们很乐意展示如何使用 FirmWire！在此页面上，您可以找到 FirmWire 漏洞的详细信息，讨论该框架，以及描述其用法的博客帖子。

## 脆弱点

到目前为止，FirmWire 参与发现了以下漏洞:

| CVE | 严重 | 探测器 | 描述 |
| --- | --- | --- | --- |
| CVE-2021-25479 | 7.2(高) | 团队固件 | SMR 2021 年 10 月 1 日之前的 Exynos CP 芯片组中可能存在一个基于堆的缓冲区溢出漏洞，允许任意内存写入和代码执行。 |
| CVE-2021-25478 | 7.2(高) | 团队固件 | SMR 2021 年 10 月 1 日之前的 Exynos CP 芯片组中可能存在一个基于堆栈的缓冲区溢出漏洞，允许任意内存写入和代码执行。 |
| CVE-2020-25279 | 9.8(关键) | 团队固件 | 在装有 O(8.x)、P(9.0)和 Q(10.0) (Exynos 芯片组)软件的三星移动设备上发现了一个问题。基带组件通过异常设置消息产生缓冲区溢出，从而导致执行任意代码。三星 ID 是 SVE-2020-18098(2020 年 9 月)。 |
| CVE-2021-25477 | 4.9(中等) | 团队固件 | SMR Oct-2021 Release 1 之前的联发科 RRC 协议栈中存在不正确的错误处理，使得调制解调器崩溃和远程拒绝服务成为可能。 |

## 会谈

| 标题 | 在哪里 | 谁 | 链接 | 描述 |
| --- | --- | --- | --- | --- |
| 模拟三星基带进行安全性测试 | 美国二十国集团 | 团队 FirmWire (Grant & Marius) | youtube 幻灯片 | 谈谈 FirmWire 的最初步骤(当时，它的工作名称是 ShannonEE)。讨论框架的基本架构。 |
| 逆转和模仿三星的香农基带 | Hardwaer.io NL’20 | 团队 FirmWire (Grant & Marius) | youtube 幻灯片 | 谈谈构建 FirmWire 所需的基于 Shannon 的调制解调器的逆向工程。 |
| FirmWire:蜂窝基带固件的透明动态分析 | NDSS 22 年 | 团队 FirmWire(赠款) | TBD | FirmWire 论文的学术报告。 |
| FirmWire:将基带安全性分析提升到新的水平 | 1922 年加拿大西部 | 团队 FirmWire(格兰特、马里乌斯和张秀坤 | TBD |  |

## 博客帖子

到目前为止，我们还不知道任何关于 FirmWire 的博客帖子，但这可能会在未来发生变化。😉

## 将你的脆弱、谈吐或博客添加到这面奖杯墙上

我们很高兴听到您使用 FirmWire！如果你想把它放在这个奖杯墙上，首先在 GitHub UI 上创建一个 FirmWire 库的分支。然后，克隆分叉的 FirmWire 库的`**docs**`分支:

**$ git clone-b docs git @ github . com:your _ username/firm wire . git**

[**Download**](https://github.com/FirmWire/FirmWire)