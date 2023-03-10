# Heaptrace:帮助可视化 Pwn 和调试的堆操作

> 原文：<https://kalilinuxtutorials.com/heaptrace/>

[![](img/c8514ad4df264bb838294a3b821e84c9.png)](https://blogger.googleusercontent.com/img/a/AVvXsEgSmQkLmoj5oQc52CYMHhYxV8HUfsnogBsHDvHffe3am0ALl6uJdQa6iAuCRpkJM3Rln652hAirX3oUMf9C8F2LDRO3zj74Gd4lVxiXucpXFBFq3HzvX1quXjoccjfa2mZxwYqfDx-r5EJ0ZGgh5L7NM27OIUITpXyLvyJ5b93q-Nl-MNF0MxSqgTn2=s728)

**Heaptrace** 是一个堆调试器，用于跟踪 ELF64 (x86_64)二进制文件中的 glibc 堆操作。它的目的是在调试二进制文件或进行堆 pwn 时帮助可视化堆操作。

*   用易于理解的符号替换地址
*   检测堆损坏和内存泄漏问题
*   可以随时在 gdb 中调试(`**--break**`)
*   支持所有 ELF64 (x86_64)二进制文件，无论 ASLR 或编译器设置如何(包括剥离的二进制文件)

**安装**

**PPA 乌班图**

**$ sudo add-apt-repository PPA:arinerron/heap trace
$ sudo apt-get 更新
$ sudo apt-get 安装 heaptrace**

## Arch 用户存储库(PKGBUILD)

使用您首选的 AUR 助手安装以下两个软件包之一:

*   `**heaptrace-git**` —源包(PKGBUILD)
*   `**heaptrace**` —二进制包(PKGBUILD)

**$ trizen -S heaptrace-git
…或者……
$ trizen-S heap trace**

**从源代码编译**

**$ git 克隆 https://github.com/Arinerron/heaptrace.git&&CD heap trace
$ make
$ sudo make install
…
$ heap trace。/目标**

# 使用

您可以在指定二进制名称之前指定 heaptrace 的参数:

**用法:
heaptrace[Options…][args…]
heap trace[Options…]–attach
选项:
-p，–attach，–PID
告诉 heap trace 附加到指定的 pid
，而不是从`target`
参数运行二进制。请注意，如果指定此参数
，则不必指定`target`。
-b，–break =，–break-at =
当指定的
`expression`满足时，向进程发送 SIGSTOP，并将 GNU 调试器
(gdb)附加到进程。
此参数支持复杂表达式。更多信息请参见文档:
https://github . com/Arinerron/heap trace/wiki/How-to-Create-Breakpoints
-B，–break-after =
类似于`--break`。用 gdb 替换 tracer
进程，但是只在堆函数
返回之后。更多信息请参见文档:
https://github . com/Arinerron/heap trace/wiki/How-to-Create-Breakpoints
-e，–environ =，–environment =
设置单个环境变量。用于
设置目标的运行时设置，如
LD_PRELOAD=。/libc.so.6，而不会影响
heaptrace 的运行时配置。该选项
可以多次使用。
-s，–symbols =
覆盖 heaptrace 为
malloc/calloc/free/realloc/realloc array 符号检测的值。
如果 heaptrace 无法自动
识别剥离的二进制文件中的堆函数，则非常有用。更多信息见维基。
-F，–follow-fork，–follow
告诉 heaptrace 如果目标调用 fork()、vfork()或
clone()，则分离父对象并跟随
子对象。
默认行为是分离子节点，而
只跟踪父节点。
-G，–GD b-path
告诉 heaptrace 使用在`path`中指定的
到 gdb 的路径，而不是/usr/bin/gdb(默认)。
-w，–width =，–term-width=
强制一定的端子宽度。
-o，–output =
将 heaptrace 输出写入`file`而不是
/dev/stderr(默认输出路径)。
-v，–verbose
打印详细信息，如
源代码中的行号，因为 ELF 中存储了所需的调试信息
。
-V，–version
显示当前的 heaptrace 版本。
-h，–help 显示该帮助菜单。**

*   例如，如果您想在操作#3 中自动附加 gdb，您可以执行`**heaptrace --break=3 ./my-binary**`。有关如何使用该参数的更多信息，请参见 wiki 文档。
*   有关如何使用 **`-s` / `--symbol`** 参数调试 heaptrace 未能自动识别其中函数的剥离二进制文件的更多信息，请参见 wiki 文档。
*   设置`**$NO_COLOR**`参数，从输出中删除 ANSI 颜色代码。此选项仍在开发中，很快将转换为一个参数。

[**Download**](https://github.com/Arinerron/heaptrace#ubuntu-ppa)