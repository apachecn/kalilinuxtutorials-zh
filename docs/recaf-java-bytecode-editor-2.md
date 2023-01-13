# Recaf:一个现代 Java 字节码编辑器

> 原文：<https://kalilinuxtutorials.com/recaf-java-bytecode-editor-2/>

Recaf 是一个易于使用的现代 Java 字节码编辑器，基于 Objectweb 的 ASM。不再需要不断的池或堆栈框架。

**也可阅读:** [IP 混淆器——社交工程师和绕过防火墙的简单工具](https://kalilinuxtutorials.com/ip-obfuscator-bypass-firewall/)

**要求**

您可以使用 Java 8 或更高版本运行 Recaf(建议您使用 jdk.java.net 发布的最新 jdk8 版本)。使用 Java 9 和更高版本需要一个额外的步骤来使用。

*   Java 8:不需要额外的步骤。
*   Java 9+:更新 pom.xml 中的 controlsfx 依赖项，以便将 8.40.14 版本更改为 9.0.0 版本。然后，您可以使用 maven 从源代码构建(打开一个终端并输入 mvn 包，假设您已经安装了 Maven)。请注意 github 版本是基于 Java 8 的。

**运行&更新**

要获得 Recaf 的最新版本，你可以下载源代码并用 maven 编译，或者从 releases [页面](https://github.com/Col-E/Recaf/releases)获取二进制文件。

作为一个 jar 文件，您可以双击它来运行 Recaf。但是，建议您通过命令行启动，以便您可以指定 JDK java 可执行文件。

这样做将解锁依赖于 JDK 功能的附加特性(tools.jar)。例如，在 windows 上，您可以使用以下命令:

**" C:\ Program Files \ Java \ JDK 1 . 8 . 0 _ 202 \ bin \ Java . exe "-jar recaf . jar**

*   **注意:**为了确保类路径包含 jdk\lib\tools.jar 的内容，请将其复制到您的 jdk\jre\lib\ext 文件夹中。
*   **注意:**您可以通过命令行自动打开文件:Java-jar recaf . jar-I myjar . jar-c com/example/my class

[**Download**](https://github.com/Col-E/Recaf)