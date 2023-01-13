# VuCSA:易受攻击的客户端-服务器应用程序——为学习/演示而设计

> 原文：<https://kalilinuxtutorials.com/vucsa/>

[![](img/fdeca8da51f9369c4762f5ce6673070b.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiGq6aYsQKHazcPcwgAv2FizkpCqndFtbOkeRBzTVBfDMGsvAPNjztzfMYjv8ClqIc1wIcTN72goePbYeKAIVRVYt6yE8JzKkjhV_F2jgZRdL2zJCqtKuTRKgaObx5luS0PerQDHvieZ0ei3A-l9mYUKg9YOh3noFTASRTdb_3Oudy_V7_ymUHel4Yj/s728/vucsa.png)

**易受攻击的客户端-服务器应用程序(VuCSA)** 用于学习/演示如何对非 http 胖客户端执行渗透测试。它是用 Java 编写的(带有 JavaFX 图形用户界面)。

目前，易受攻击的应用程序包含以下挑战:

1.  缓冲区过度读取(模拟)
2.  命令执行
3.  SQL 注入
4.  列举
5.  可扩展标记语言
6.  水平访问控制
7.  垂直访问控制

如果你想知道如何解决这些挑战，看看 [PETEP 网站](http://petep.warxim.com/methodology/)，它描述了如何使用开源工具 PETEP 来利用它们。

**提示:**在开始黑客攻击之前，不要忘记检查下面消息的数据结构。

## 怎么跑？

为了运行易受攻击的服务器和客户端，您可以使用 GitHub 上的某个版本或运行 gradle assemble，它会创建分发包(适用于 Windows 和 Unix)。这些包包含将使用 JVM 运行服务器和客户机的 sh/bat 脚本。

## 项目结构

项目分为三个模块:

*   **vucsa-common**–客户端和服务器的通用功能(包括协议处理实用程序)
*   **vucsa-client**–带有 JavaFX GUI 的易受攻击客户端
*   **vu CsA-服务器**–终端使用的易受攻击的服务器

## 数据结构

服务器和客户端之间传输的消息具有以下简单格式:

```
[type][target][length][payload]
  32b    32b     32b     ???
```

这四个部分具有以下含义:

*   **type**–消息的类型(用于序列化/反序列化)
*   **目标**–将接收消息的目标处理程序
*   **长度**–有效载荷的长度
*   **有效载荷**–序列化为字节的数据

[Click Here To Download](https://github.com/Warxim/vucsa)