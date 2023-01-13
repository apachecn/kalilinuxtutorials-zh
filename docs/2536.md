# DDexec:一种在 Linux 上无文件地、秘密地运行二进制文件的技术，使用 Dd 将 Shell 替换为另一个进程

> 原文：<https://kalilinuxtutorials.com/ddexec/>

[![](img/45e26ccca289707e81ceebbfd92c7b63.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEii9h7GJRrVn_AaOxjEwxRFRsmUl3vFcyqaGDHkBnLiHN3Z3upggY96_xmThNI5tPNz1ipwelRFCCPS9zxWqP48NhwkWhT4JUbauYHO8tTaoT2kW6i6geGMmeMhO5BRae3fiXhJdb2K_D2-5MeKtg_ln4FRpnBfvbjABc8_knz49x335cmVEGIYThp1/s728/christian-lue-o0WKbszSw_A-unsplash.png)

**DDexec** 是一种在 Linux 上无文件地、秘密地运行二进制文件的技术，使用 Dd 用另一个进程替换 Shell。在 Linux 中，为了运行一个程序，它必须作为一个文件存在，它必须以某种方式通过文件系统层次结构可访问(这就是`**execve()**`的工作方式)。该文件可能位于磁盘或 ram (tmpfs、memfd)中，但您需要一个文件路径。这使得控制 Linux 系统上运行的内容变得非常容易，它使得检测威胁和攻击者的工具变得容易，或者阻止他们试图执行他们的任何东西(例如*不允许无特权的用户在任何地方放置可执行文件)。*

 *但是这项技术将改变这一切。如果你不能启动你想要的进程…那么你就劫持了一个已经存在的进程。

## 用法

将您想要运行的二进制文件的 base64 通过管道输入到`**ddexec.sh**`脚本中(**不带**换行符)。脚本的参数就是程序的参数(从`**argv[0]**`开始)。

来，试试这个:

**base64-w0/bin/ls | bash ddexec . sh/bin/ls-lA**

还有一个`**ddsc.sh**`脚本，可以让你直接运行二进制代码。以下是一个“Hello world”外壳代码。

**bash ddsc.sh -x <**

或者

**bash ddsc . sh<(xxd-PS-r<T5<" 4831 c 0 FEC 089 c 7488d 3510000000 ba 0 c 0000000 f 054831 c 089 c 7 b 03 c 0 f 0548656 c 6 c 6 f 20776 f 726 c 640 a 00 ")**

是的。它与 meterpreter 一起工作。

测试的 Linux 发行版有 Debian、Alpine 和 Arch。支持的 shells 有 bash、zsh 和 ash over x86_64 和 aarch64 (arm64)架构。

## 依赖关系

这个脚本依赖于以下工具来工作。

**DD
bash | zsh | ash(busybox)
头
尾
切
grep
od
read link
WC
tr
base 64**

## 这项技术

如果你能够任意修改一个进程的内存，那么你就可以接管它。这可以用来劫持一个已经存在的进程，并用另一个程序替换它。我们可以通过使用`**ptrace()**` syscall(这要求您有能力执行 syscall 或者在系统上有可用的 gdb)或者更有趣的是，写入`**/proc/$pid/mem**`来实现这一点。

文件`**/proc/$pid/mem**`是一个进程的整个地址空间的一对一映射(例如 x86-64 中从`**0x0000000000000000**`到`**0x7ffffffffffff000**`的*)。这意味着在偏移量`**x**`读取或写入该文件与在虚拟地址`**x**`读取或修改内容是一样的。*

现在，我们面临四个基本问题:

*   通常，只有 root 用户和文件的程序所有者可以修改它。
*   ASLR。
*   如果我们试图读取或写入一个没有映射到程序地址空间的地址，我们将会得到一个 I/O 错误。

这些问题有解决方案，尽管它们并不完美，但都是好的:

*   大多数 shell 解释器允许创建文件描述符，然后由子进程继承。我们可以创建一个指向具有写权限的 sell 的`**mem**`文件的 fd…这样使用该 FD 的子进程将能够修改 shell 的内存。
*   ASLR 甚至不是问题，我们可以检查 shell 的`**maps**`文件或 procfs 中的任何其他文件，以便获得关于进程地址空间的信息。
*   所以我们需要查看文件。在 shell 中，除非使用臭名昭著的`**dd**`，否则无法做到这一点。

### 更详细地

这些步骤相对容易，不需要任何专业知识就能理解:

*   解析我们想要运行的二进制文件和加载程序，找出它们需要什么映射。然后编写一个“外壳”代码，概括地说，它将执行内核在每次调用`**execve()**`时执行的相同步骤:
    *   创建所述映射。
    *   将二进制文件读入其中。
    *   设置权限。
    *   最后，用程序的参数初始化堆栈，并放置辅助向量(加载程序需要的)。
    *   跳到加载程序中，让它完成剩下的工作(加载程序所需的库)。
*   从 **`syscall`** 文件中获取进程在执行系统调用后将返回的地址。
*   用我们的外壳代码覆盖那个可执行的地方(通过`**mem**`我们可以修改不可写的页面)。
*   将我们要运行的程序传递给进程的 stdin(将由`**read()**`表示的“shell”代码)。
*   在这一点上，它是由加载程序来加载我们的程序所必需的库，并跳转到其中。

哦，所有这些都必须在 s **hell** 脚本中完成，否则还有什么意义呢？

[**Download**](https://github.com/arget13/DDexec)*