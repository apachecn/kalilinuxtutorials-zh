# HeapInspect:在 Python 中检查堆

> 原文：<https://kalilinuxtutorials.com/heapinspect-inspect-heap-in-python/>

[![HeapInspect : Inspect Heap In Python](img/40546bc926e450899e5c6fa57009e01b.png "HeapInspect : Inspect Heap In Python")](https://1.bp.blogspot.com/-R_TzzgersV0/Xhzpy18BZCI/AAAAAAAAEbg/EfbHhZOvoLgc1hZPXwlC9rPYVHfZy4OzwCLcBGAsYHQ/s1600/Usage-1%25281%2529.png)

heap SPECT 的设计是为了让 heap 更漂亮。因此，让我们了解一下这个工具的一些特性，它将检查 python 中的堆；

*   无 gdb 和其他要求
*   多 glibc 支持
    *   2.19，2.23-2.27(目前正在测试)
    *   32 位和 64 位
*   显示堆的漂亮用户界面
    *   `**HeapShower**`(详细)
    *   `**PrettyPrinter**`(丰富多彩，概要)
*   Heapdiff(工作中)
*   腐败检测和利用分析(工作)
*   也支持 gdb(仅 python2)

**也可阅读-[Karonte:检测嵌入式固件多二进制漏洞的静态分析工具](https://kalilinuxtutorials.com/karonte-detect-vulnerabilities-embedded-firmware/)**

**用法**

这个工具的快速使用。

![](img/3596479c3d2364b591253bae669f623b.png)![](img/6e3586d283506008a82bd8b6398184a5.png)![](img/14937f0919a6945f4427eaafd341ffb4.png)![](img/43ec718ee792df959c728bfe0f28d091.png)

你也可以把它作为一个 gdb 插件，当 **`pwndbg`** 或者其他插件无法分析堆时非常有用。

**sed-I " 1i source ` pwd `/gdsubscript . py " ~/。gdbinit #或者，您可以手动添加该行**

**注**

它暂时不支持 gdb python3。任何能让它兼容 python3 的人都受欢迎。

![](img/ebad0de0a0c3ae39a8a8d48c6cba9866.png)![](img/2bb98685ce185b13c20792bf12c3e545.png)![](img/1d3f3edbdb4dcf8124e33417addf1fa2.png)[**Download**](https://github.com/matrix1001/heapinspect)