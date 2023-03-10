# IPC dump:Linux 上跟踪进程间通信(IPC)的工具

> 原文：<https://kalilinuxtutorials.com/ipcdump/>

[![IPCDump : Tool For Tracing Interprocess Communication (IPC) On Linux](img/bf349fd24e0b570dff6039e36868ac12.png "IPCDump : Tool For Tracing Interprocess Communication (IPC) On Linux")](https://1.bp.blogspot.com/-03ksFC_xw1M/YImpojhnZ8I/AAAAAAAAI5Q/zQADAp8b1Sw2Ks-cdVeHeY-r0KjOoT8AgCLcBGAsYHQ/s728/IPCDump%25281%2529.png)

**IPCDump** 是 Linux 上追踪进程间通信(IPC)的工具。它涵盖了大多数常见的 IPC 机制——管道、fifos、信号、UNIX 套接字、基于环回的网络和伪终端。它是调试多进程应用程序的有用工具，也是理解系统中不同移动部件如何相互通信的简单方法。我

t 可以跟踪这种通信的元数据和内容，它特别适合于跟踪短期进程之间的 IPC，这在使用传统的调试工具(如 strace 或 gdb)时会很困难。它还具有一些基本的过滤功能，可以帮助您筛选大量事件。

ipcdump 收集的大部分信息来自放置在 kprobes 上的 BPF 钩子和内核中关键函数的跟踪点，尽管它也填充了/proc 文件系统中的一些簿记。为此，ipcdump 大量使用了 [gobpf](https://github.com/iovisor/gobpf) ，它为 [bcc 框架](https://github.com/iovisor/bcc)提供 golang 绑定。

**要求&用途**

*   **戈朗> = 1.15.6**
*   **经过测试的操作系统和内核**

| Ubuntu 18.04 lt | Ubuntu 20.04 lt |
| --- | --- |
| 4.15.0 | 测验 | 未测试 |
| 5.4.0 | 未测试 | 测验 |
| 5.8.0 | 未测试 | 已测试*
 |

**注意:**需要从源构建 bcc

**大楼**

**依赖关系**

*   安装 golang

**snap install go–classic**

或者直接从 golang 网站

*   根据您选择的操作系统，使用 iovisor 的说明安装 BCC(通常较新的版本需要从源代码构建)

**建立 ipcdump**

**git 克隆 https://github.com/guardicore/IPCDump
CD IPC dump/cmd/IPC dump
去构建**

**用途**

。 **/ipcdump -h
用法。/ipcdump:
-B uint
每个事件要转储的最大字节数，或者 0 表示整个事件(可能很大)。仅当指定了-x 时才有意义。
-D 值
按目的通信过滤(可多次指定)
-L 不输出丢失事件信息
-P 值
按通信过滤(源或目的， 可多次指定)
-S 值
按源 comm 过滤(可多次指定)
-c uint
事件后退出
-d 值
按目的 pid 过滤(可多次指定)
-f 字符串
输出格式(默认为文本)(默认为“文本”)
-p 值
按 pid 过滤(源或目的，可多次指定)
-s 值【t24
可能值:a | all k | signal u | UNIX ud | UNIX-dgram us | UNIX-stream t | pty lo | loopback lt | loopback-TCP Lu | loopback-UDP | pipe
-x 转储相关的 IPC 字节(而不仅仅是事件详细信息)。**

**俏皮话**

以 root 用户身份运行:

**#转储系统**
上的所有 ipc。/IPC dump

**#任意两个进程之间发送的转储信号**
。/IPC dump-t kill

**# dump 环回 TCP 连接元数据到或来自 pid 1337**
。/IPC dump-t loopback-TCP-p 1337

**# dump UNIX socket IPC 元数据和内容来自 Xorg**
。/IPC dump-t UNIX-x-S Xorg

**# dump JSON 格式的管道 i/o 元数据和前 64 个字节的内容**
。/ipcdump -t pipe -x -B 64 -f json

**特性**

*   支持管道和 FIFOs
*   环回 IPC
*   信号(常规和实时)
*   Unix 流和数据报
*   基于伪终端的 IPC
*   基于进程 PID 或名称的事件过滤
*   友好的或 JSON 格式的输出

**设计**

ipcdump 由一系列收集器组成，每个收集器负责一种特定类型的 IPC 事件。例如，**T0 或者`IPC_EVENT_SIGNAL`。**

实际上，所有的收集器都是使用连接到 kprobes 和 tracepoints 的 bpf 挂钩构建的。但是，它们的实现是完全独立的——没有特别的理由假设我们的信息总是来自 bpf。也就是说，不同的收集器必须共享一个 bpf 模块，因为它们需要共享一些公共代码。为此，我们共享一个 BpfBuilder(本质上是一个连接 bcc 代码字符串的包装器),每个收集器都向该构建器注册自己的代码。然后用 gobpf 加载完整的 bcc 脚本，每个模块放置它需要的钩子。

目前有两种簿记在 IPC 收集器之间共享:

*   `**SocketIdentifier (internal/collection/sock_id.go)**` —内核`struct sock*`和使用它们的进程之间的映射。
*   `**CommIdentifier (internal/collection/comm_id.go)**`—PID 编号和相应的过程名称(`/proc/<pid>/comm`)之间的映射。在每一个这样的过程中所做的簿记对于短暂的过程尤其重要；虽然这些信息可以稍后在用户模式中通过解析`/proc`来填充，但是当事件遇到处理程序时，相关的进程通常已经消失了。也就是说，我们有时会填写来自`/proc`的信息。这种情况主要发生在 ipcdump 运行之前的进程中；在这种情况下，我们不会捕获像流程命名这样的事件。`SocketIdentifier`和`CommIdentifier`试图在一个 API 背后抽象 bcc 代码和`/proc`解析之间的这种二元性，尽管它不是非常干净。顺便说一下，在全新版本的 Linux (5.8)中，bpf 迭代器可以完全取代这种簿记，尽管为了向后兼容，我们现在可能应该坚持 hooks-and-procfs 范式。

事件输出通过通用的`EmitIpcEvent()`函数完成，该函数采用标准的事件格式(源进程、目标进程、元数据键值对和内容)并以统一的格式输出。为了节省事件带宽，如果没有指定`-x`标志，收集器通常不会输出 IPC 内容。这是在`internal/collection/ipc_bytes.go`中用一些奇特的预处理魔法完成的。

[**Download**](https://github.com/guardicore/IPCDump)