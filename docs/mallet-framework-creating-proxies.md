# mallet——创建代理的框架

> 原文：<https://kalilinuxtutorials.com/mallet-framework-creating-proxies/>

Mallet 是一个为任意协议创建代理的工具，类似于我们熟悉的拦截 web 代理，只是更加通用。

它建立在 Netty 框架之上，并且非常依赖于 Netty 管道概念，它允许处理程序图形的图形化组装。在 Netty 世界中，处理程序实例提供帧定界(即消息在哪里开始和结束)、协议解码和编码(将字节流转换成 Java 对象，或者将字节流转换成不同的字节流——想想压缩和解压缩),以及更高级别的逻辑(实际上对那些对象做一些事情)。

通过仔细分离编解码器和实际操作消息的处理程序，Mallet 可以从现有编解码器的大型库中受益，并避免重复实现许多协议。这个难题的最后一部分由一个处理程序提供，该处理程序将一个管道上接收到的消息复制到另一个管道，将这些消息代理到它们的最终目的地。

**也读[PAC Vim——一个教你 Vim 命令](https://kalilinuxtutorials.com/pacvim-game/)** 的游戏

当然，虽然消息在 Mallet 中，但它们很容易被篡改，要么用 Java 或 JSR-223 兼容脚本语言编写的定制处理程序，要么使用提供的编辑器之一手动篡改。

## **建筑槌**

Mallet 使用 Maven，所以编译代码是一件简单的事情

```
mvn package
```

要运行它:

```
cd target/
java -jar mallet-1.0-SNAPSHOT-spring-boot.jar
```

在`examples/`目录中提供了一些示例图。JSON 图期望一个 JSON 客户机在 localhost:9998/tcp 上连接到 Mallet，而实际的服务器在 localhost:9999/tcp 上。只有最后一个 json 图(json5.mxe)对正在传递的 JSON 消息的结构做出任何假设，所以它们应该适用于任何发送 JSON 消息的 app。

demo.mxe 显示了一个复杂的图形，有两条管道，TCP 和 UDP。TCP 管道分别支持端口 80 和 443 上的 HTTP 和 HTTPS，以及 WebSockets，同时将任何其他流量直接转发到其目的地。构建 UDP 管道是为了处理 localhost:1053/udp 上的 DNS 请求，将对 google.com 的查询替换为对 www.sensepost.com 的查询，并将请求转发到 Google DNS 服务器。

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/sensepost/mallet)