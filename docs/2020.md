# CThreadHijack:通过线程劫持进行远程进程注入的信标对象文件(BOF)

> 原文：<https://kalilinuxtutorials.com/cthreadhijack/>

[![Objection : Runtime Mobile Exploration](img/97d6cd69f3d4ed779934ae6cc3c6d6de.png "Objection : Runtime Mobile Exploration")](https://1.bp.blogspot.com/-JAQ9YhZKHIc/XSvuGuda9dI/AAAAAAAABV0/W0c1HfCGOloUp5rmRDttaCP9hg41P6uLwCLcBGAs/s1600/objection%25281%2529.png)

cThreadHijack 是一个信标对象文件(BOF ),用于通过线程劫持进行远程进程注入，而不会产生远程线程。附带的博客可以在这里找到。cThreadHijack 通过`**VirtualAllocEx**`和`**WriteProcessMemory**`将通过用户提供的监听器参数生成的原始信标外壳代码注入到由用户提供的 PID 参数定义的远程进程中。然后，cThreadHijack 识别目标进程中的第一个枚举线程，挂起它，并通过一个`CONTEXT`结构检索线程 CPU 状态的内容，而不是通过`**CreateRemoteThread**`或其他 API 生成一个新的远程线程。然后，`CONTEXT`结构的 RIP 寄存器成员(在 64 位系统上)被操作指向前面提到的远程有效载荷的地址。在执行之前，添加了一个例程，将 Beacon 外壳代码封装在对`**CreateThread**`的调用中——让 Beacon 拥有自己的线程，这个线程是本地产生的，而不是远程产生的。`**CreateThread**`例程还被包装在`**NtContinue**`函数调用例程中，允许恢复之前被劫持的线程，而不会使远程进程崩溃。cThreadHijack 的信标有效负载由一个“线程”退出函数生成，允许在信标退出后继续处理。包含空格的信标侦听器名称必须用引号括起来。

**大楼**

*   在 Windows 机器上，打开一个`**x64 Native Tools Command Prompt for VS**`提示符。这可以通过按 Windows 键并键入`x64 Native Tools`并选择提示符来完成。
*   将目录改为 **`C:\path\to\cThreadHijack`。**
*   `**nmake -f Makefile.msvc build**`
*   用`**load /path/to/cThreadHijack.cna**`通过钴击`**Script Console**`加载 cThreadHijack.cna

**用法**

**cThreadHijack PID LISTENER _ NAME**

**beacon>cThreadHijack 7340 测试
[+]主机调用 home，发送:268433 字节
[+]接收输出:
[+]目标进程 PID: 7340
[+]接收输出:
[+]打开一个句柄给 PID 7340
[+]接收输出:
[+]在目标进程中发现一个线程！线程 ID: 10212
[+]接收到的输出:
[+]挂起目标线程…
[+]接收到的输出:
[+]向远程进程写入信标外壳代码！
[+]接收到的输出:
[+]远程进程内部分配在 0x201f4ab0000 的 CreateThread 和 NtContinue 例程的虚拟内存！
[+]接收到的输出:
[+]nt continue 例程的大小:64 字节
[+]上下文结构的大小:1232 字节
[+]堆栈对齐例程的大小:4
[+]create thread 例程的大小:64
[+]shellcode 的大小:261632 字节
[+]接收到的输出:
[+]将缓冲区的有效载荷写入之前在中分配的缓冲区！
[+]接收输出:
[+]当前 RIP: 0x7ffa55df69a4
[+]接收输出:
[+]成功将目标线程的 RIP 寄存器指向 shellcode！
[+]接收输出:
[+]当前 RIP: 0x201f4ab0000
[+]接收输出:
[+]恢复线程！请稍等片刻，信标有效负载将执行…**

[**Download**](https://github.com/connormcgarr/cThreadHijack)