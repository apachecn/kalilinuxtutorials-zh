# dex 2 jar——用于 Android 的工具。dex 和 Java。类别文件

> 原文：<https://kalilinuxtutorials.com/dex2jar-android-java/>

Dex2jar 是一个与 android 协同工作的工具。dex 和 java。类文件。

*   读/写:读/写 Dalvik 可执行文件(。dex)文件。它有一个类似于 ASM 的轻量级 API。
*   d2j-dex2jar:转换。dex 文件到。类文件(压缩为 jar)
*   smali/baksmali:将 dex 反汇编成 smali 文件，从 smali 文件组装 dex。与 smali/baksmali 的实现不同，语法相同，但我们支持 desc 类型中的转义
*   其他工具:d2j-解密-字符串

**也可理解为[Malwoverview–对包含恶意软件样本的目录执行初始&快速分类的工具](https://kalilinuxtutorials.com/malwoverview/)**

## **dex 2 jar Utilization**

```
sh d2j-dex2jar.sh -f ~/path/to/apk_to_decompile.apk
```

并且输出的文件会是 **`apk_to_decompile-dex2jar.jar`** 。

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/pxb1988/dex2jar)