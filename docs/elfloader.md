# Elfloader:一个与架构无关的外壳代码 ELF 文件展平器

> 原文：<https://kalilinuxtutorials.com/elfloader/>

[![](img/7bf06bed71e63876578bcc00ce333044.png)](https://blogger.googleusercontent.com/img/a/AVvXsEhheoRB0Hk2D4FNDwv03BDB7sraq9n7516Hp06GHZj5ASW_zSBCkbMzNYOdb5vjORsNGesxTCTtD37EOwWhcREZCTrhIWSv9TAD1Sb-wcj3_oFcFxxI2qGqBDyYSdvyYIa-EHMdrNcYtZLhNLs2xbvl7kwH2-m9QMTJO8fUAOhS2FAVs6eXUp2aLDQ7=s728)

`**Elfloader**`是一个超级简单的 ELF 文件加载器，可以生成 ELF 的平面内存表示。

将它与 Rust 结合起来，现在你就可以用一种合适的、安全的高级语言编写外壳代码了。LLVM 可以瞄准的任何目标都可以使用，包括为真正奇特的平台和 ABI 定制的目标规范。喜欢在 32 位系统上使用类似于`**u64**`的东西，边界检查数组，分配的丢弃处理等等🙂

它只是将所有的`**LOAD**`部分连接在一起，如果有间隙就用零填充，形成一个大的平面文件。

该文件包括`**.bss**`部分的零初始化，因此可以直接用作外壳代码有效载荷。

如果您不想在失效开放链接器脚本上浪费时间，这可能是一个很好的方法。

这并不处理任何重定位，而是由您来确保原始 ELF 是基于您希望它所在的地址。

# 用法

要使用该工具，只需:

**用法:elf loader[–perms][–binary][–base =]
–binary–不输出 FELF，输出不带
元数据的原始加载图像
–perms–创建一个包含权限数据的 FELF0002，覆盖
–binary
–base =–强制输出从`<addr>`开始，如果需要，从
基数到第一个加载段的开始处填充零。
`<addr>`为默认十六进制，可以用`0d`、`0b`、
、`0o`前缀替代。
警告:这不会*将*重新定位到基址，它只是在`<addr>`开始
输出(添加零字节，以便
输出图像可以在`<addr>`而不是
原始 ELF 基址加载)
–输入 ELF 的路径
–输出文件的路径**

要安装此工具，请运行:

`**cargo install --path** .`

现在您可以在 shell 的任何地方使用`**elfloader**`!

# 开发

这个项目是在这里实时开发的:

[https://www.youtube.com/embed/x0V-CEmXQCQ?feature=oembed](https://www.youtube.com/embed/x0V-CEmXQCQ?feature=oembed)

# 举例

在`**example_small_program**`中有一个例子，简单地运行`**make**`或`**nmake**`，这将生成一个 8 字节的`**example.bin**`。

**pleb @ gamey ~/elf loader/example _ small _ program $ make
cargo build–release
0.03s 内完成释放【优化】目标
elf loader–binary target/aarch 64-unknown-none/release/example _ small _ program example . bin
pleb @ gamey ~/elf loader/example _ small _ program $ ls-l ./example . bin
-rw-r–r–1 pleb 8 Nov 8 12:27。/example . bin
pleb @ gamey ~/elf loader/example _ small _ program $ objdump-d target/AAR ch 64-unknown-none/release/example _ small _ program
target/AAR ch 64-unknown-none/release/example _ small _ program:文件格式 elf64-littleaarch64
节的反汇编。text:
00000000133700 B0<_ start>:
133700 B0:8b 000020 add x0，x1，x0
133700 B4:d 65 f 03 c 0 ret**

现在你可以用 Rust 写你的 shellcode 了，不用担心你是否会发出**`.data``.rodata``.bss`**等。这将为你处理一切！

还有一个关于`**.bss**`和`**.rodata**`的例子

**pleb @ gamey ~/elf loader/example _ program _ with _ data $ make
cargo build–release
0.04s 内完成发布[优化]目标
elf loader–binary target/aarch 64-unknown-none/release/example _ program _ with _ data example . bin
pleb @ gamey ~/elf loader/example _ program _ with _ data $ ls-l ./example . bin
-rw-r–r–1 pleb 29 11 月 8 日/example . bin
pleb @ gamey ~/elf loader/example _ program _ with _ data $ objdump-d target/AAR ch 64-unknown-none/release/example _ program _ with _ data
target/AAR ch 64-unknown-none/release/example _ program _ with _ data:文件格式 elf64-littleaarch64
节的反汇编。正文:
0000000013370124<_ start>:
13370124:90000000 adrp x0，13370000<_ start-0x 124>
13370128:900000008 adrp x8，13370000 < _start-0x124 【T43 从偏移量 64 开始
程序头:
类型偏移量 virt addr phys addr
FileSiz MemSiz 标志对齐
LOAD 0x 0000000000000120 0x 00000000001370120 0x 000000000001370120
0x 0000000000000004 R 0x 1
rodata
01。正文
02。bss
03**

# 中间部分

这个工具不关心除了`**LOAD**`节以外的任何东西。它从 ELF 头中确定字节序(小对大)和位(32 对 64)，并从那里根据程序头虚拟地址(它被加载的位置)、文件大小(初始化的字节数)和 mem 大小(实际内存区域的大小)创建一个平面映像。字节根据偏移量和文件大小从文件中初始化，然后用零扩展直到 mem 大小(如果 mem 大小小于文件大小，则被截断)。

这些`**LOAD**`部分然后用零字节填充连接在一起，以填补空白。

这被设计得非常简单，并且与 ELF 输入无关。它可以是可执行文件、目标文件、共享对象、核心转储等，并不真正关心。它只会给出内存的平面表示，仅此而已。

这允许你将任何 ELF 转换成外壳代码，或者一种更简单的文件格式，更容易加载到难以到达的区域，比如嵌入式设备。就我个人而言，我为我的 MIPS NT 4.0 加载程序开发了这个，它允许我运行 Rust 代码。

# FELF0001 格式

默认情况下，此工具会生成 FELF 文件格式。这是一个福尔克精灵。这是一种简单的文件格式:

**felf 0001–魔头
入口–入口点地址的 64 位小端整数
基址–加载图像的基址的 64 位小端整数
–文件的其余部分是原始图像，在`base`加载，在`entry`** 跳转

# FELF0002 格式(当使用–perms 标志时)

默认情况下，此工具会生成 FELF 文件格式。这是一个福尔克精灵。这是一个带有权限的简单文件格式:

**felf 0002–魔头
入口–入口点地址的 64 位小端整数
基址–加载图像的基址的 64 位小端整数
–文件的其余部分是原始图像，将在`base`加载并在`entry`
跳转到
–权限，匹配其中字节包含
的字节以下标志按位“或”运算:
0x 01–可执行，0x 02–可写，0x 04–可读【T10**

[**Download**](https://github.com/gamozolabs/elfloader)