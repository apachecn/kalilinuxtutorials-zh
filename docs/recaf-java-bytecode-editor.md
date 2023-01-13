# recaf——一个现代的 Java 字节码编辑器

> 原文：<https://kalilinuxtutorials.com/recaf-java-bytecode-editor/>

Recaf 是一个易于使用的现代 Java 字节码编辑器，基于 Objectweb 的 ASM。不再需要不断的池或堆栈框架。查看文档了解更多信息。

#### 要求

你可以用 Java 8 或更高版本运行 Recaf】(建议你使用来自[jdk.java.net](https://jdk.java.net/8/)的最新 jdk8 版本)。使用 Java 9 和更高版本需要一个额外的步骤来使用。

Java 8: 不需要额外的步骤。
**Java 9+:** 更新 pom.xml 中的 controlsfx 依赖关系，使 8.40.14 版本变更为 9.0.0 版本。然后您可以用 maven *从源代码构建(打开一个终端并输入 mvn 包，假设您已经安装了 Maven)*。请注意 github 版本是基于 Java 8 的。

也可阅读: [Tyton:内核模式 Rootkit 猎人](https://kalilinuxtutorials.com/tyton-kernel-rootkit-hunter/)

### 运行和更新

要获得 Recaf 的最新版本，你可以下载源代码并用 maven 编译，或者从发布页面获取二进制文件。

作为一个 jar 文件，您可以双击它来运行 Recaf。但是，建议您通过命令行启动，以便您可以指定 JDK java 可执行文件。这样做将解锁依赖于 JDK 功能的附加特性 *(tools.jar)* 。例如，在 windows 上，您可以使用以下命令:

**" C:\ Program Files \ Java \ JDK 1 . 8 . 0 _ 202 \ bin \ Java . exe "-jar recaf . jar**

**注意:**为了确保类路径包含 **jdk\lib\tools.jar** 的内容，将其复制到您的 **jdk\jre\lib\ext 文件夹中。**

**注意:**您可以通过命令行自动打开文件:

**Java-jar recaf . jar-I myjar . jar-c com/example/my class**

**注意:**当启动 Recaf 时，您会在更新发布时得到通知。

### 使用的库:

*   [ASM](http://asm.ow2.org/)–*级编辑能力*
*   [CFR](http://www.benf.org/other/cfr/)–*反编译*
*   [简单内存编译器](https://github.com/Col-E/Simple-Memory-Compiler)–*反编译代码的重新编译*
*   [JIMFS](https://github.com/google/jimfs)–*虚拟文件系统*
*   [控件 sfx](http://fxexperience.com/controlsfx/)–*自定义控件(几乎用于所有东西)*
*   [RichTextFX](https://github.com/FXMisc/RichTextFX)–*反编译代码高亮*
*   [JRegex](http://jregex.sourceforge.net/)–*反编译代码高亮显示的模式匹配*
*   [minimal-Json](https://github.com/ralfstx/minimal-json)–*Json 读/写配置存储*
*   [普通标记](https://github.com/atlassian/commonmark-java)–*降价解析*
*   [pico CLI](http://picocli.info/)–*命令行参数解析*

[**Download**](https://github.com/Col-E/Recaf)