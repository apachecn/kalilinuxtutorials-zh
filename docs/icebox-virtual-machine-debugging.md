# Icebox:虚拟机自检、跟踪和调试

> 原文：<https://kalilinuxtutorials.com/icebox-virtual-machine-debugging/>

[![Icebox : Virtual Machine Introspection, Tracing & Debugging](img/a476f02a26404ced30f22830260aa747.png "Icebox : Virtual Machine Introspection, Tracing & Debugging")](https://1.bp.blogspot.com/-DuuNKAB2hew/XR1khRnMLhI/AAAAAAAABMg/WcxID-1bxzMq1T3uEais5daN8B9s4EfdACLcBGAs/s1600/wireshark_icebox.gif)

Icebox 是一个虚拟机自省解决方案，可以让你悄悄地跟踪和调试任何进程(内核或用户)。这是基于项目[胜算](https://github.com/Winbagility/Winbagility)。

可能有帮助的文件:

*   [INSTALL.md](https://github.com/thalium/icebox/blob/master/doc/INSTALL.md) :如何安装 icebox。
*   [BUILD.md](https://github.com/thalium/icebox/blob/master/doc/BUILD.md) :如何搭建 icebox。

**项目组织**

*   [fdp](https://github.com/thalium/icebox/blob/master/src/FDP) :快速调试协议源
*   [冰箱](https://github.com/thalium/icebox/blob/master/src/icebox):冰箱来源
    *   icebox : Icebox 库(核心，操作系统助手，插件…)
    *   icebox_cmd :测试几个特性的程序
    *   [样本](https://github.com/thalium/icebox/blob/master/src/icebox/samples):一堆例子
*   [winbagibility](https://github.com/thalium/icebox/blob/master/src/Winbagility):将 WinDBG 连接到 FDP 的存根
*   [virtualbox](https://github.com/thalium/icebox/blob/master/third_party/virtualbox) :为 FDP 打补丁的 virtualbox 源码。

**也可理解为-[lst 2x 64 dbg:从 IDA 中提取标签。lst 或 Ghidra。csv 文件&导出 x64dbg 数据库](https://kalilinuxtutorials.com/lst2x64dbg-extract-labels/)**

**入门**

一些样品已经被写入[样品文件夹](https://github.com/thalium/icebox/blob/master/src/icebox/samples)。

在你安装了[需求](https://github.com/thalium/icebox/blob/master/doc/BUILD.md#requirements-to-compile-icebox)之后，你可以用这些[指令](https://github.com/thalium/icebox/blob/master/doc/BUILD.gen.md#stage-build)来构建它们。

如果您使用的是 Windows guest 虚拟机，您可能希望将环境变量 **_NT_SYMBOL_PATH** 设置为包含 guest 虚拟机 pdb 的文件夹。**请注意，如果 icebox 安装程序没有找到你的客户的内核的 pdb，它将会失败。**

```
**vm_resume:**
vm_resume 只需暂停然后恢复你的 vm。

**cd icebox/bin/$ARCH/
。/VM _ resume**<vm_name></vm_name>****VM _ name>****

 ****nt _ writefile:**
nt _ writefile 在一个进程调用 ntdll 时中断！NtWriteFile，并将写入文件的内容转储到您主机上的当前目录中。

**cd icebox/bin/$ARCH/。
/nt _ writefile**<vm_name><process_name></process_name></vm_name>**VM _ name><process _ name>**

**heapsan:**
heapsan 中断进程的 ntdll 内存分配，并在每个指针之后的&之前添加填充。它仍然是不完整的，不做任何检查。

**cd icebox/bin/$ARCH/
。/heap San**<vm_name>**<process_name></process_name>**</vm_name>******<VM _ name><process _ name>******

 ******wireshark:**
当 ndis 驱动程序读取或发送网络数据包并创建 wireshark 跟踪时，wireshark 会中断。pcapng)。如果需要，发送的每个包都与从内核到用户的调用栈相关联。

**cd icebox/bin/$ARCH/
。/wireshark**<name>**<path_to_capture_file></path_to_capture_file>**</name>******<名称> <路径 _ 到 _ 捕获 _ 文件>******
```

****[**Download**](https://github.com/thalium/icebox)**********