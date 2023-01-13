# Gadgetinspector:用于查找反序列化小工具的代码分析器

> 原文：<https://kalilinuxtutorials.com/gadgetinspector/>

[![Gadgetinspector : Code Analyzer For Finding Deserialization Gadget](img/8156d9248d8ee0d550eb8ee87dab483f.png "Gadgetinspector : Code Analyzer For Finding Deserialization Gadget")](https://1.bp.blogspot.com/-26ZnQCqxHKY/XlWMDdMJtqI/AAAAAAAAFGc/nqpbz3kqwgIAvlSALfbQpLjXhbMuI_RjwCLcBGAsYHQ/s1600/analyze_code.png)

**Gadgetinspector** 是一个字节码分析器，用于在 Java 应用程序中查找反序列化小工具链。

这个项目检查小工具链的 Java 库和类路径。小工具链用于构建反序列化漏洞的利用。

通过自动发现应用程序类路径中可能的小工具链，渗透测试人员可以快速构建漏洞，应用程序安全工程师可以评估反序列化漏洞的影响，并确定其补救的优先级。

**免责声明**:这个项目充其量是 alpha。它需要测试和文档添加。

**大楼**

假设您的系统上安装了 JDK，您应该能够运行`**./gradlew shadowJar**`。然后你可以用**运行应用程序。**

**怎么用？**

这个应用程序期望作为参数的或者是一个 war 文件的路径(在这种情况下，war 将被展开，它的所有类和库被用作类路径),或者是任意数量的 jar。

请注意，分析可能会占用大量内存(到目前为止，gadget inspector 还没有进行任何优化，以减少对内存的占用)。对于小型库，您可能希望分配至少 2GB 的堆大小(即使用`-Xmx2G`标志)。对于较大的应用程序，您会希望使用尽可能多的内存。

该工具包将经历几个阶段的类路径检查，以建立数据集供后面的阶段使用。这些数据集被写入到扩展名为`.dat`的文件中，并可以在运行后被丢弃(编写它们主要是为了在开发过程中跳过早期阶段)。

分析运行后，文件`**gadget-chains.txt**`将被写入。

**也可阅读-[0l4bs:面向 Web 应用安全爱好者的跨站点脚本实验室](https://kalilinuxtutorials.com/0l4bs/)**

**例子**

以下是针对`**commons-collections-3.2.1.jar**`运行的示例，例如

**wget http://central . maven . org/maven 2/commons-collections/commons-collections/3 . 2 . 1/commons-collections-3 . 2 . 1 . jar
Java-Xmx2G-jar build/libs/gadget-inspector-all . jar commons-collections-3 . 2 . 1 . jar**

在 gadget-chains.txt 中有以下链:

**com/sun/CORBA/se/SPI/orb util/proxy/compositeinvocationhandlerimpl . invoke(Ljava/lang/Object；ljava/lang/reflect/Method；【Ljava/lang/Object；)Ljava/lang/Object；(-1)
com/sun/CORBA/se/SPI/orb util/proxy/compositeinvocationhandlerimpl . invoke(Ljava/lang/Object；ljava/lang/reflect/Method；【Ljava/lang/Object；)Ljava/lang/Object；0)
org/Apache/commons/collections/map/defaultedmap . get(Ljava/lang/Object；)Ljava/lang/Object；0)
org/Apache/commons/collections/functors/invoker transformer . transform(Ljava/lang/Object；)Ljava/lang/Object；0)
Java/lang/reflect/method . invoke(Ljava/lang/Object；【Ljava/lang/Object；)Ljava/lang/Object；**(0)

这个链的入口点是 JDK `**InvocationHandler**`类的一个实现。

使用与原始 commons-collections 小工具链中相同的技巧，该类的任何可序列化实现都可以在小工具链中到达，因此发现的链从这里开始。

这个方法调用`**classToInvocationHandler.get()**`。发现的小工具链表明`**classToInvocationHandler**`可以被序列化为`**DefaultedMap**`，这样这个调用就会跳转到`**DefaultedMap.get()**`。

链中的下一步从这个方法调用`**value.transform()**`。这个类中的参数`**value**`可以序列化为一个`**InvokerTransformer**`。

在这个类的`**transform**`方法中，我们看到我们调用了`**cls.getMethodName(iMethodName, ...).invoke(...)**`。Gadget inspector 确定`**iMethodName**`是攻击者可控制的序列化成员，因此攻击者可以在该类上执行任意方法。

这个小工具链是 Frohoff 发现的完整 commons-collections 小工具链的构建块。在上面的案例中，gadget inspector 碰巧通过`**CompositeInvocationHandlerImpl**`和`**DefaultedMap**`而不是`**AnnotationInvocationHandler**`和`**LazyMap**`发现条目，但大体相同。

**其他例子**

如果您正在寻找此工具可以找到哪种链的更多示例，以下库也有一些有趣的结果:

*   [http://central . maven . org/maven 2/org/clo jure/clo jure/1 . 8 . 0/clo jure-1 . 8 . 0 . jar](http://central.maven.org/maven2/org/clojure/clojure/1.8.0/clojure-1.8.0.jar)
*   [https://mvn repository . com/artifact/org . Scala-lang/Scala-library/2 . 12 . 5](https://mvnrepository.com/artifact/org.scala-lang/scala-library/2.12.5)
*   [http://central . maven . org/maven 2/org/python/jython-standalone/2 . 5 . 3/jython-standalone-2 . 5 . 3 . jar](http://central.maven.org/maven2/org/python/jython-standalone/2.5.3/jython-standalone-2.5.3.jar)

不要忘记，您还可以将 gadget inspector 指向一个完整的应用程序(打包为一个 JAR 或 WAR)。例如，当分析 [Zksample2](https://sourceforge.net/projects/zksample2/) 应用程序的 war 时，我们得到以下小工具链:

**net/SF/jasper reports/charts/design/jrdesignpiedataset . read object(Ljava/io/object inputstream；)V(1)
org/Apache/commons/collections/fastarraylist . add(Ljava/lang/Object；)Z(0)
Java/util/ArrayList . clone()Ljava/lang/Object；(0)
org/jfree/data/keytogroupmap . clone()Ljava/lang/Object；(0)
org/jfree/data/keytogroupmap . clone(Ljava/lang/Object；)Ljava/lang/Object；(0)
Java/lang/reflect/method . invoke(Ljava/lang/Object；【Ljava/lang/Object；)Ljava/lang/Object；**(0)

如您所见，这利用了应用程序中包含的几个不同的库来构建链。

**常见问题解答**

问:如果 gadget inspector 发现了一个小工具链，可以利用它吗？

答:不总是这样。该分析使用一些简化的假设，并且可以报告误报(实际上并不存在的小工具链)。作为一个简单的例子，它不试图解决分支条件的可满足性。因此，它将以小工具链的形式报告以下内容:

**公共类 MySerializableClass 实现 Serializable {
公共 void read object(ObjectInputStream ois){
if(false)system . exit(0)；
ois . default read object()；
}
}**

此外，gadget inspector 在它认为有趣的功能上有相当广泛的条件。

例如，它认为反射是有趣的(例如，对 Method.invoke()的调用，攻击者可以控制该方法)，但是经常被忽略的断言意味着攻击者可以影响被调用的方法，但是没有完全的控制权。

例如，攻击者可以调用任何类中的“getError()”方法，但不能调用任何其他方法名。

问:如果没有发现小工具链，这是否意味着我的应用程序不会被利用？

答:没有！首先，gadget inspector 有一组非常狭窄的“sink”功能，它认为这些功能有“有趣”的副作用。

这当然不意味着没有其他有趣或危险的行为不在列表中。

此外，静态分析有许多限制，这意味着 gadget inspector 总是会有盲点。

举例来说，gadget inspector 目前会错过这一点，因为它不遵循反射调用。

**公共类 MySerializableClass 实现 Serializable {
公共 void read object(ObjectInputStream ois){
system . class . get method(" exit "，int.class)。invoke(null，0)；
}** 

[**Download**](https://github.com/JackOfMostTrades/gadgetinspector)