# HandleKatz:使用克隆句柄的 PIC Lsass 转储程序

> 原文：<https://kalilinuxtutorials.com/handlekatz/>

[![](img/b975ba89651d57edaf35f83d1c909d2e.png)](https://blogger.googleusercontent.com/img/a/AVvXsEi_no5Uqs-ICZ9HMik4ryvrHrO416lIdEg2e9pjLBezw7vzaIn6OlZJpOWP6bQ4rAVJGn9bn6ruvG0vDkjflgRM_jOZzWzh6rbnKRKqXhohfrgi2Rp90FH1xQaTPxPwIFXSo47zODau597MLhLcjBu70S5XV3fqp-_7rjja-VflEqENZgi7GHUmpHyR=s728)

HandleKatz 工具是作为我们 Brucon2021 会议演讲的一部分实现的，它演示了 Lsass 的**克隆句柄的用法，以便创建相同的混淆内存转储。**

它编译成一个可执行文件**，完全位于它的文本段**中。因此，提取的。PE 文件的文本段是完全独立于位置的代码(=PIC)，这意味着它可以像任何外壳代码一样被处理。

HandleKatz 在内存中的执行占用的内存非常少，因为它本身不会分配任何更多的可执行内存，因此可以有效地与@_ForrestOrr 描述的(幻影)DLL 中空化等概念相结合。这与 PIC PE 加载器形成对比，例如 Donut、SRDI 或反射加载器，它们在 PE 加载期间分配更多可执行内存。此外，它利用 ReactOS MiniDumpWriteDumpA 的修改版本，通过直接系统调用将模糊转储写入磁盘。

有关详细信息，请参考该库中的 PDF 文件**PICYourMalware.pdf**。

**用途**

*   **全力**建设 HandleKatz.bin、汉德卡兹宾和 loader.exe

**请注意**不同的编译器(版本)产生不同的结果。这可能会产生一个带有重定位的 PE 文件。

所有测试都是使用`**x86_64-w64-mingw32-gcc mingw-gcc version 11.2.0 (GCC)**`进行的。制作的 PIC 在:Windows 10 Pro 10.0.17763 上测试成功。在其他版本的 windows 上，API 哈希可能会有所不同。

要使用 PIC，将一个指针指向可执行内存中的外壳代码，并根据定义调用它:

```
DWORD handleKatz(BOOL b_only_recon, char* ptr_output_path, uint32_t pid, char* ptr_buf_output);
```

*   如果该位置位，HandleKatz 将仅枚举合适的句柄而不进行转储
*   **ptr_output_path** 确定模糊转储将被写入的位置
*   从哪个 pid 克隆一个句柄
*   ptr_buf_output 一个字符指针，HandleKatz 将其内部输出写入该指针

对于转储文件的去模糊，可以使用脚本 **Decoder.py** 。

**加载器**为 HandleKatz 实现一个样本加载器:

**loader.exe–PID:7331–outfile:C:\ Temp \ dump . obfuscated**

![](img/6bac024cfe6981f01cd88dd13009cc5f.png)

**检测**

由于克隆的句柄与修改后的 ReactOS 代码一起使用，因此在 Lsass 上观察不到 ProcessAccess 事件。但是，可以观察到持有 Lsass 句柄的程序上的 ProcessAccess 事件。

防御者可以通过设置**Process _ DUP _ HANDLE(0x 0040)**来监控进程访问掩码，以识别该工具的使用情况。

[**Download**](https://github.com/codewhitesec/HandleKatz)