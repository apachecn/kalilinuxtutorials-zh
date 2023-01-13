# dollands:一种颤振/飞镖逆向工程工具

> 原文：<https://kalilinuxtutorials.com/doldrums-a-flutter-dart-reverse-engineering-tool/>

[![Bandit : Tool Designed To Find Common Security Issues In Python Code](img/91e4d2f273f5c711ee2236db07f8c776.png "Bandit : Tool Designed To Find Common Security Issues In Python Code")](https://2.bp.blogspot.com/-NiszWLqhz_A/XORMc6fw3NI/AAAAAAAAAaQ/eNGYQYNixrw3ZDsqU3Pib0_wXXImqB7UACLcBGAs/s1600/logotype-sm%25281%2529.png)

**dollands**是针对 Android 的 Flutter 应用的逆向工程工具。具体地说，它是 Flutter/Dart Android 二进制文件的解析器和信息提取器，通常命名为`**libapp.so**`，适用于所有 Dart 2.10 版本。运行时，它输出隔离快照中存在的所有类的完整转储。

该工具目前处于 **beta** 版本，缺少一些反序列化例程和类信息。如果它不能开箱即用，请让我知道。

**依赖关系**

dollands 需要 pyelftools 来解析 ELF 格式。您可以安装它

**pip3 安装 pyelftools**

**用途**

要使用，只需运行下面的命令，用 **`libapp.so`** 替换适当的二进制文件，用`**output**`替换所需的输出文件。请注意，详细选项仅适用于 Dart 快照 2.12 版

**python 3 src/main . py[-v]libapp . so 输出**

预期的输出是所有类的转储，格式如下:

**类 MyApp 扩展 StatelessWidget {
Widget build(dynamic type，DynamicType) {
绝对偏移量代码:0x EC 85 c
}
String my print(dynamic type，DynamicType) {
绝对偏移量代码:0xeca80
}
}**

绝对代码偏移量表示在`**libapp.so**`文件中可以找到本地函数的偏移量。

[**Download**](https://github.com/rscloura/Doldrums)