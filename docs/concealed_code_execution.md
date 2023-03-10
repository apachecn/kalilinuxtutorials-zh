# 隐藏代码执行:描述攻击技术的工具和技术文章

> 原文：<https://kalilinuxtutorials.com/concealed_code_execution/>

[![](img/5233bf3316fe516261d798835ef55439.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjrqQBci4yg-hJMoDpDR4wXZl-7L0rl73GitSoUMqVnMR7Z0bBe1S0ezQIJfHd1SRFW90W-RDxz1VaPPXSIJ0s194TXsYLlW3uLEzIvBL72ZRmxZtKJgOdsHM_aWxShdPk2f10NIoSyYTLsShRZdusXNaE7SoE49fTx2bu-Z5U11vtBHwr670LeQ2Zc/s728/download%20(4).png)

**hidden _ Code _ Execution**是一套描述攻击技术的工具和技术文章，这些攻击技术依赖于隐藏 Windows 上的代码执行。在这里，您将找到这些技术如何工作的解释，接收关于检测的建议，并获得用于测试您的检测覆盖率的示例源代码。

## 内容

该库涵盖了两类广泛使用内部 Windows 机制的攻击技术，并提供了检测它们的建议和工具:

*   **流程篡改**–一套在整个流程范围内隐藏代码的技术。
*   **代码注入**–一组技巧，允许代码作为其他进程的一部分执行，而不干扰它们的功能。
*   **Detection**–针对各种隐藏代码执行的技术进行防御的建议汇编。

项目的核心价值:

*   **系统方法**。这个存储库不仅仅包括工具的集合或外部资源的链接。每一个主题都收到对基本概念的详细解释；每一个具体的案例都被归入一般的类别。
*   **概念验证工具**。文章附有用 C 语言编写的示例项目，展示了所描述的工具在实践中的使用。
*   **初级到专业**。你不需要成为网络安全专家来理解我们描述的概念。然而，由于对细节和陷阱的关注，即使是相应领域的专业人士也应该发现内容是有价值的和教育意义的。

## 实施

这个项目的最后一个与众不同的特点是在整个示例中广泛使用了**本地 API** 。做出这一选择的动机如下:

*   **功能**。一些最先进的技术所需的操作(比如进程篡改)没有通过其他 API 公开。
*   **控制**。作为与操作系统交互的最低级别，它提供了对其行为的最大控制。Win32 API 是在本机 API 的基础上实现的，所以用前者可以实现的东西用后者也是可以实现的。
*   **可用性**。由 ntdll.dll 公开，Native API 可用于所有进程，包括系统进程。
*   **一致性**。这个 API 公开的接口非常一致。在学习了基本的设计选择之后，仅仅从 API 的名字就可以正确地预测大多数的函数原型。
*   **挂钩阻力**。当使用本机 API 时，移除或绕过用户模式挂钩要容易得多，这部分蒙蔽了安全软件。没有需要修补的低级库，所以解除挂钩变得简单，只需加载第二个 ntdll.dll 实例，并将调用重定向到那里。

## 编制备注

示例代码使用 PHNT 项目提供的原生 API 头。确保使用`**git clone --recurse-submodules**`命令获取这个依赖项来克隆存储库。或者，您可以在克隆存储库之后使用`**git submodule update --init**`。

要构建存储库中包含的项目，您需要一个最新版本的 Windows SDK。如果使用 Visual Studio，请参考内置 SDK 安装。或者，您也可以使用 EWDK 的独立构建环境。要一次编译所有工具，使用`**MSBuild AllTools.sln /t:build /p:configuration=Release /p:platform=x64**`。

[**Download**](https://github.com/huntandhackett/concealed_code_execution)