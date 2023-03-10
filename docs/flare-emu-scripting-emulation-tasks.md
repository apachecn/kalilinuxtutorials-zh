# Flare-Emu:易于使用且灵活的界面，用于脚本仿真任务

> 原文：<https://kalilinuxtutorials.com/flare-emu-scripting-emulation-tasks/>

[![Flare-Emu : Easy To Use And Flexible Interface For Scripting Emulation Tasks](img/874163e419446065a62a6348a6f1df39.png "Flare-Emu : Easy To Use And Flexible Interface For Scripting Emulation Tasks")](https://1.bp.blogspot.com/-4KrqtG0XWx4/XY9n8cy3sXI/AAAAAAAACtM/9XYuq1JG9TA1fF1oZkFJw40G5QVdrawRwCLcBGAsYHQ/s1600/flare-emu_logo.png)

**Flare-emu** 将 IDA Pro 的二进制分析功能与 Unicorn 的仿真框架相结合，为用户提供一个易于使用且灵活的界面来编写仿真任务脚本。

它被设计来处理为其支持的架构建立一个灵活和健壮的仿真器的所有内务，以便您可以专注于解决您的代码分析问题。

目前，flare-emu 支持 x86、x86_64、ARM 和 ARM64 体系结构。

它目前提供了四种不同的接口来满足您的仿真需求，以及一系列相关的帮助器和实用程序功能。

**也可阅读-[Kirjuri:管理案件的网络应用程序&法医物证项目](https://kalilinuxtutorials.com/kirjuri-web-application-for-managing-cases/)**

**模拟器**

该 API 用于在用户指定的上下文中模拟一系列指令或函数。它为单个指令和遇到“调用”指令时的用户定义挂钩提供了选项。

用户可以决定模拟器是跳过，还是调用函数调用。该接口为用户指定给定寄存器和堆栈参数的值提供了一种简单的方法。

如果指定了字节字符串，它将被写入仿真器的内存，指针将被写入寄存器或堆栈变量。仿真后，用户可以利用 flare-emu 的实用程序功能从仿真内存或寄存器中读取数据，或者使用返回的 Unicorn 仿真对象进行直接探测。

一个名为 emulateSelection 的用于 emulateRange 的小包装器函数可用于模拟 IDA Pro 中当前突出显示的一系列指令。

**迭代**

该 API 用于强制模拟函数中的特定分支，以达到给定的目标。

用户可以指定一个目标地址列表，或者一个函数的地址，从该地址到该函数的交叉引用列表被用作目标，以及当到达目标时的回调。

不管在仿真期间可能导致采取不同分支的条件如何，都将达到目标。

像 emulateRange API 一样，为单个指令和遇到“调用”指令时的用户定义挂钩提供了选项。

iterate API 的一个例子是实现类似于 argtracker 工具的功能。

**迭代所有路径**

这个 API 很像 iterate，除了不是提供一个或多个目标地址，而是提供一个目标函数，它将试图找到所有路径并进行模拟。

这在您执行代码分析时非常有用，因为您希望分析到函数的每个基本块。

**EmulateBytes**

这个 API 提供了一种简单地模拟大量无关外壳代码的方法。所提供的字节不会添加到 IDB 中，而是简单地按原样模拟。这对于准备仿真环境非常有用。

例如，flare-emu 本身使用此 API 来操作 ARM64 CPU 的型号特定寄存器(MSR ),该寄存器不是由 Unicorn 公开的，以便启用向量浮点(VFP)指令和寄存器访问。

返回 Unicorn 仿真对象供用户进一步探查。

**EmulateBytes**

这个 API 提供了一种简单地模拟大量无关外壳代码的方法。所提供的字节不会添加到 IDB 中，而是简单地按原样模拟。这对于准备仿真环境非常有用。

例如，flare-emu 本身使用此 API 来操作 ARM64 CPU 的型号特定寄存器(MSR ),该寄存器不是由 Unicorn 公开的，以便启用向量浮点(VFP)指令和寄存器访问。

返回 Unicorn 仿真对象供用户进一步探查。

**来自**的仿真

这个 API 在函数边界没有明确定义的情况下很有用，这种情况在混淆的二进制文件或外壳代码中很常见。

您提供了一个起始地址，它会一直模拟下去，直到没有什么可模拟的了，或者您在您的一个钩子中停止了模拟。

这可以通过将 strict 参数设置为 False 来调用，以启用动态代码发现；flare-emu 将让 IDA Pro 在仿真过程中发出指令。

**安装**

要安装 flare-emu，只需将 flare_emu.py 和 flare_emu_hooks.py 放入 IDA Pro 的 python 目录中，并将其作为模块导入 IDApython 脚本中。flare-emu 依赖于 Unicorn 及其 Python 绑定。

**重要提示**

flare-emu 是使用新的 IDA Pro 7x API 编写的，它不向后兼容以前版本的 IDA Pro。

**用途**

虽然 flare-emu 可以用于解决许多不同的代码分析问题，但它更常见的用途之一是帮助解密恶意软件二进制文件中的字符串。

FLOSS 是一个很棒的工具，它可以通过尝试识别字符串解密函数并使用仿真来解密每个交叉引用中传递的字符串，来自动完成这项工作。

然而，FLOSS 不可能总是能够识别这些函数，并使用其通用方法正确地模拟它们。

有时候你需要做更多的工作，一旦你熟悉了 flare-emu，它会帮你节省很多时间。

让我们来看一个恶意软件分析师在处理加密字符串时遇到的常见场景。

**简单的字符串解密场景**

您已经确定了解密 x86_64 二进制文件中所有字符串的函数。这个函数到处被调用，解密许多不同的字符串。在 IDA Pro 中，您将此函数命名为 decryptString。

下面是您的 flare-emu 脚本，用于解密所有这些字符串，并在每次函数调用时使用解密的字符串放置注释，以及记录每个解密的字符串及其解密的地址。

**从未来导入 print_function
导入 idc
导入 idaapi
导入 idautils
导入 flare_emu

def 解密(argv):
myEH = flare_emu。emu helper()
myeh . emulator ange(IDC . get _ name _ ea _ simple(" decryptString ")，registers = {"arg1":argv[0]，" arg2":argv[1]，
"arg3":argv[2]，" arg 4 ":argv[3]})
return myeh . getemustring(argv[0])

def iterate callback(eh，address，argv，userData):
s = decrypt(argvemu helper()
eh . iterate(IDC . get _ name _ ea _ simple(" decryptString ")，iterateCallback)**

在 _ **main** 中，我们首先从 **flare-emu** 创建一个 **EmuHelper** 类的实例。这是我们用 flare-emu 做所有事情的类。

接下来，我们使用 iterate API，给它我们的 **decryptString** 函数的地址和我们的回调函数的名称， **EmuHelper** 将为每个模拟的交叉引用调用这个函数。

**iterateCallback** 函数接收 **EmuHelper** 实例，这里名为 eh，还有交叉引用的地址、传递给这个特定调用的参数，以及这里名为 **userData** 的特殊字典。

在这个简单的例子中没有使用 userData ,但是可以把它看作是模拟器的一个持久上下文，在这里你可以存储你自己的定制数据。

但是要小心，因为 flare-emu 本身也使用这个字典来存储执行任务所需的关键信息。其中一个这样的数据是 **EmuHelper** 实例本身，它存储在“ **EmuHelper** 键中。

如果您感兴趣，请搜索源代码以了解关于该词典的更多信息。

这个回调函数简单地调用 decrypt 函数，打印解密后的字符串，并在调用 decryptString 的地址为它创建一个注释。

**decrypt** 创建 **EmuHelper** 的第二个实例，用于模拟 **decryptString** 函数本身，它将**为我们解密**字符串。这个 **decryptString** 函数的原型如下:***char * decryptString(char * text，int textLength，char *key，int keyLength)*** 。

它只是就地解密字符串。我们的 decrypt 函数将 iterateCallback 函数收到的参数传递给我们对 EmuHelper 的 emulateRange API 的调用。

因为这是一个 x86_64 二进制文件，所以调用约定使用寄存器而不是堆栈来传递参数。flare-emu 根据 IDA Pro 确定的二进制文件的体系结构和文件格式，自动确定哪些寄存器代表哪些参数，从而允许您编写至少与体系结构无关的代码。

如果这是 32 位 x86，你会用 stack 实参来代替传递实参，像这样:***myeh . emulator ange(IDC . get _ name _ ea _ simple(" decryptString ")，stack = [0，argv[0]，argv[1]，argv[2]，argv[3]])*** 。第一个堆栈值是 x86 中的返回地址，所以我们在这里只使用 0 作为占位符值。

一旦仿真完成，我们调用 **getEmuString** API 来检索存储在由传递给函数的第一个参数所指向的内存位置中的以 null 结尾的字符串。

**仿真功能**

`**emulateRange(startAddr, endAddr=None, registers=None, stack=None, instructionHook=None, callHook=None, memAccessHook=None, hookData=None, skipCalls=True, hookApis=True, strict=True, count=0)**`–模拟从`**startAddress**`开始到`**endAddress**`结束的指令范围，不包括`**endAddress**`处的指令。如果 endAddress 是`None`，当在开始模拟的同一个函数中遇到“返回”类型指令时，模拟停止。

*   `**registers**`是一个字典，键是寄存器名，值是寄存器值。一些特殊的寄存器名是由`**flare-emu**`创建的，在这里可以使用，比如`**arg1**` **、** `**arg2**` **等。、**、`**ret**`和`**pc**`。
*   `**stack**`是一个以逆序推入堆栈的值数组，很像`x86`中函数的参数。在`**x86**`中，记住考虑数组中的第一个值作为函数调用的返回地址，而不是函数的第一个参数。`**flare-emu**`将根据`**registers**`和`**stack**`参数中指定的值初始化仿真线程的上下文和内存。如果为这些值中的任何一个指定了字符串，它将被写入内存中的某个位置，而指向该内存的指针将被写入指定的寄存器或堆栈位置。
*   `**instructionHook**`可以是您定义的在每个指令被仿真之前调用的函数。它有以下原型:`**instructionHook(unicornObject, address, instructionSize, userData)**`。
*   `**callHook**`可以是您定义的一个函数，当在仿真过程中遇到“call”类型的指令时将被调用。它有以下原型:`**callHook(address, arguments, functionName, userData)**`。
*   `**hookData**`是一个包含用户自定义数据的字典，可用于钩子函数。这是一种在整个仿真过程中持久保存数据的方法。`**flare-emu**`也为自己的目的使用这个字典，所以必须小心不要定义一个已经定义的键。由于在 Unicorn 中的命名，这个变量在用户定义的钩子函数中经常被命名为`**userData**`。
*   `**skipCalls**`将使仿真器跳过“调用”类型的指令，并相应地调整堆栈，默认为`True`。
*   `**hookApis**`使`**flare-emu**`执行一些在仿真过程中遇到的更常见的运行时和操作系统库函数的简单实现。这使您不必担心对诸如`**memcpy**` **、** `**strcat**` **、** `**malloc**`等函数的调用。，默认为`**True**`。
*   `**memAccessHook**`可以是一个你定义的函数，当内存被读写时调用。它有以下原型:`**memAccessHook(unicornObject, accessType, memAccessAddress, memAccessSize, memValue, userData)**`。
*   `**strict**`，当设置为`**True**` (默认)时，检查分支目的地以确保反汇编器期望指令。否则它跳过分支指令。如果设置为`**False**` **，** `**flare-emu**`将在 IDA Pro 中模拟指令**(小心禁用)**。
*   `**count**` 是要仿真的最大指令数，默认为`0`表示没有限制。

`**iterate(target, targetCallback, preEmuCallback=None, callHook=None, instructionHook=None, hookData=None, resetEmuMem=False, hookApis=True, memAccessHook=None)**`–对于由`**target**`指定的每个目标，从包含函数的开始直到目标地址，执行一个单独的仿真。仿真将被强制沿着到达每个目标所需的分支进行。`**target**` 可以是一个函数的地址，在这种情况下，目标列表中填充了指定函数的所有交叉引用。或者，`**target**` 可以是目标的显式列表。

*   `**targetCallback**`是您创建的一个函数，它将由`flare-emu`为仿真过程中到达的每个目标调用。它有以下原型:`**targetHook(emuHelper, address, arguments, userData)**`。
*   `**preEmuCallback**`是您创建的一个函数，它将在每个目标的仿真开始之前被调用。如果需要，您可以在这里实现一些设置代码。
*   `**resetEmuMem**`将使`**flare-emu**`在每个目标的仿真开始前重置仿真存储器，默认为`**False**`。

`**iterateAllPaths(target, targetCallback, preEmuCallback=None, callHook=None, instructionHook=None, hookData=None, resetEmuMem=False, hookApis=True, memAccessHook=None, maxPaths=MAXCODEPATHS, maxNodes=MAXNODESEARCH)**`–对于包含地址`**target**`的函数，通过它对每个发现的路径执行单独的仿真，直到`**maxPaths**`。

*   `**maxPaths**`–将被搜索和仿真的通过功能的最大路径数。一些更复杂的功能会导致图形搜索功能花费很长时间或永远无法完成；在合理的时间内调整该参数以满足您的需求。
*   `**maxNodes**`–通过目标函数查找路径时，将搜索的基本块的最大数量。这是防止不合理的搜索次数和挂起的安全措施，可能不需要更改。

`**emulateBytes(bytes, registers=None, stack=None, baseAddress=0x400000, instructionHook=None, hookData=None)**`–如果可能，将`**bytes**`中包含的代码写入`**baseAddress**`的仿真内存中，并从`**bytes**`的开始到结束仿真指令。

`**emulateFrom(startAddr, registers=None, stack=None, instructionHook=None, callHook=None, memAccessHook=None, hookData=None, skipCalls=True, hookApis=True, strict=True, count=0)**`–这个 API 在函数边界没有明确定义的情况下很有用，这种情况在二进制文件或外壳代码中很常见。您提供一个起始地址作为`**startAddr**`，它将一直模拟，直到没有什么需要模拟或者您在您的一个钩子中停止模拟。这可以通过将`**strict**`参数设置为`**False**`来调用，以启用动态代码发现；`**flare-emu**`将让 IDA Pro 在模拟过程中做出指示。

**效用函数**

下面是由`**EmuHelper**`类提供的一些有用的实用函数的不完整列表。

*   `**hexString(value)**`–返回该值的十六进制格式的字符串。用于记录和打印报表。
*   `**getIDBString(address)**`–返回位于 IDB 中某个地址的字符串，直到一个空终止符。字符不一定是可打印的。对于在没有仿真上下文的情况下检索字符串非常有用。
*   `**skipInstruction(userData, useIDA=False)**`–从仿真钩子调用这个函数，跳过当前指令，将程序计数器移到下一条指令。添加了`**useIDA**` 选项，用于处理 IDA Pro 将多条指令合并为一条伪指令，而您想要跳过所有指令的情况。不能从单个指令挂钩中多次调用此函数来跳过多条指令。为了跳过多个指令，如果您正在仿真 ARM 代码，建议不要直接写入程序计数器，因为这可能会导致 thumb 模式出现问题。相反，试试 EmuHelper 的`**changeProgramCounter**` API(如下所述)。
*   `**changeProgramCounter(userData, newAddress)**`–从仿真钩子中调用这个函数来改变程序计数器寄存器的值。这个 API 负责 ARM 架构的 thumb 模式跟踪。
*   `**getRegVal(registerName)**`–检索指定寄存器的值，对子寄存器寻址敏感。比如“ax”会返回`**x86**` **中 EAX/RAX 寄存器的低 16 位。**
*   `**stopEmulation(userData)**`–从仿真挂钩中调用这个函数来停止仿真。使用它而不是调用`**emu_stop**` Unicorn API，这样`**EmuHelper**`对象可以处理与`**iterate**`特性相关的簿记。
*   `**getEmuString(address)**`–返回位于仿真存储器中某个地址的字符串，直到一个空终止符。字符不一定是可打印的。
*   `**getEmuWideString(address)**`–返回位于仿真存储器中某个地址的“宽字符”字符串，最长为空终止符。“宽字符”在这里泛指每隔一个字节包含一个空字节的任何字节序列，就像用 UTF-16 LE 编码的 ASCII 字符串一样。字符不一定是可打印的。
*   `**getEmuBytes(address, length)**`–返回位于仿真存储器中某个地址的字节字符串。
*   `**getEmuPtr(address)**`–返回位于给定地址的指针值。
*   `**writeEmuPtr(address)**`–将指针值写入仿真存储器的给定地址。
*   `**loadBytes(bytes, address=None)**`–在仿真器中分配内存并将字节写入其中。
*   `**isValidEmuPtr(address)**`–如果提供的地址指向有效的仿真内存，则返回`**True**`。
*   `**getEmuMemRegion(address)**`–返回一个元组，该元组包含包含所提供地址的存储区的起始和结束地址，如果地址无效，则返回`None`。
*   `**getArgv()**`–在“Call”类型的指令中从仿真挂钩调用该函数，以接收函数的参数数组。
*   `**addApiHook(apiName, hook)**`–为`**EmuHelper**`的这个实例添加一个新的 API 钩子。每当仿真过程中遇到对`**apiName**`的调用指令，`**EmuHelper**`就会调用`**hook**`指定的函数。如果`**hook**`是一个字符串，那么它应该是一个已经被`**EmuHelper**`挂钩的 API 的名称，在这种情况下，它将调用其现有的挂钩函数。如果`hook`是一个函数，它会调用那个函数。
*   `**allocEmuMem(size, addr=None**)`–分配足够的仿真器内存来容纳`**size**`字节。它试图接受所请求的`**addres**s`，但是如果它与现有的内存区域重叠，它将分配一个未使用的内存区域并返回新的地址。如果`**address**` 不是页对齐的，它将返回一个地址，在新区域内保持相同的页对齐偏移量。例如，当`**0x1000**`已经被分配时，请求地址`**0x1234**`可以在`**0x2000**`分配并返回`**0x2234**`。

[Download](https://github.com/fireeye/flare-emu)