# Qiling:高级二进制仿真框架

> 原文：<https://kalilinuxtutorials.com/qiling/>

[![Qiling : Advanced Binary Emulation Framework](img/bd85cc273c2d168d6958125e50b07afa.png "Qiling : Advanced Binary Emulation Framework")](https://1.bp.blogspot.com/-YRAZsApCwGk/XjyPGRsWvqI/AAAAAAAAEwQ/J4uaJ2DSn3QupVqTkyNE0ArIFLLSmKc7wCLcBGAsYHQ/s1600/Qiling%25281%2529.png)

**Qiling** 是一个高级二进制仿真框架，具有以下特性:

*   跨平台:Windows，MacOS，Linux，BSD
*   跨架构:X86、X86_64、Arm、Arm64、Mips
*   多种文件格式:PE，MachO，ELF
*   在隔离的环境中模拟和沙盒化机器代码
*   提供高级 API 来设置和配置沙箱
*   细粒度的插装:允许不同级别的挂钩(指令/基本块/内存访问/异常/系统调用/IO/等等)
*   允许动态热补丁即时运行代码，包括加载的库
*   Python 中的真正框架，使得在其上构建定制的安全分析工具变得容易

**棋灵 vs 其他模拟器**

开源模拟器很多，但最接近麒麟的两个项目是[独角兽](http://www.unicorn-engine.org) & [Qemu usermode](https://qemu.org) 。这一部分解释了与它们的主要区别。

**麒麟 vs 独角兽发动机**

建立在独角兽之上，但是麒麟和独角兽是两种不同的动物。

*   Unicorn 只是一个 CPU 模拟器，所以它专注于模拟 CPU 指令，可以理解模拟器内存。除此之外，Unicorn 不知道更高层次的概念，例如动态库、系统调用、I/O 处理或可执行格式，如 PE、MachO 或 ELF。因此，Unicorn 只能模拟原始机器指令，而没有操作系统(OS)上下文。
*   Qiling 被设计为一个更高级的框架，它利用 Unicorn 来模拟 CPU 指令，但可以理解 OS:它有可执行格式加载器(目前用于 PE、MachO 和 ELF)、动态链接器(因此我们可以加载和重定位共享库)、syscall 和 IO 处理程序。由于这个原因，Qiling 可以运行可执行二进制文件，而不需要其本机操作系统。

**也可阅读-[Obfuscapk:安卓应用的黑盒混淆工具](https://kalilinuxtutorials.com/obfuscapk/)**

**奇灵 vs Qemu 用户模式**

Qemu usermode 做的事情与我们的模拟器类似，即以跨架构的方式模拟整个可执行二进制文件。然而，Qiling 提供了一些与 Qemu 用户模式的重要区别。

*   Qiling 是一个真正的分析框架，它允许你在上面建立你自己的动态分析工具(用友好的 Python 语言)。同时，Qemu 只是一个工具，而不是一个框架。
*   Qiling 可以执行动态插装，甚至可以在运行时热修补代码。Qemu 两者都不做。
*   不仅跨架构工作，Qiling 也是跨平台的，所以例如你可以在 Windows 上运行 Linux ELF 文件。相比之下，Qemu usermode 只运行相同操作系统的二进制文件，例如 Linux 上的 Linux ELF，这是由于它将 syscall 从仿真代码转发到本地操作系统的方式。
*   Qiling 支持更多平台，包括 Windows、MacOS、Linux & BSD。Qemu 用户模式只能处理 Linux & BSD。

**安装**

运行下面的命令行来安装 Qiling (Python3 是必需的)。

**python3 setup.py 安装**

**例题**

*   下面的例子展示了如何使用 Qiling 框架在 Linux 机器上模拟 Windows EXE。

从 qiling 导入*

**#沙盒仿真 EXE**
def my_sandbox(path，rootfs):
#设置 Qiling 引擎
ql = Qiling(path，rootfs)
#现在仿真 EXE
QL . run()

if**name**= "**main**":
#在我们的 rootfs
my_sandbox([.

*   下面的例子展示了如何使用 Qiling 框架动态地修补一个 Windows crackme，使它总是显示“祝贺”对话框。

从 qiling 导入*

def force _ call _ dialog _ func(QL):
# get DialogFunc 地址
lpDialogFunc = QL . un pack 32(QL . mem _ read(QL . sp–0x 8，4))
#为 dialog func 设置堆栈内存
QL . stack _ push(0)
QL . stack _ push(1001)
QL . stack _ push(273)
QL b ' \ x90 \ x90 ')
#在一个地址用回调钩子
ql.hook_address(0x00401016，force _ call _ dialog _ func)
QL . run()

if**name**= = "**main**":
my _ sandbox([" rootfs/x86_windows/bin/Easy _ crack me . exe "]，" rootfs/x86 _ windows ")

下面的 Youtube 视频展示了上面的例子是如何工作的。

[https://www.youtube.com/embed/p17ONUbCnUU?feature=oembed&enablejsapi=1](https://www.youtube.com/embed/p17ONUbCnUU?feature=oembed&enablejsapi=1)

**Wannacry 演示**

*   下面的 Youtube 视频显示了 Qiling 如何分析 Wannacry 恶意软件。

[https://www.youtube.com/embed/gVtpcXBxwE8?feature=oembed&enablejsapi=1](https://www.youtube.com/embed/gVtpcXBxwE8?feature=oembed&enablejsapi=1)

**Qltool**

Qiling 还提供了一个名为`**qltool**`的友好工具来快速模拟 shellcode &可执行二进制文件。

要模拟二进制文件，请运行:

**$。/QL tool run-f examples/rootfs/arm _ Linux/bin/arm 32-hello–rootfs examples/rootfs/arm _ Linux/**

要运行外壳代码，请运行:

**$。/QL tool shellcode–OS Linux–arch x86–ASM-f 示例/shellcodes/Lin 32 _ exec ve . ASM**

[**Download**](https://github.com/qilingframework/qiling)