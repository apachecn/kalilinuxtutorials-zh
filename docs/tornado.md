# Tornado:使用隐藏服务匿名反转 Tor 网络上的外壳，无需端口转发

> 原文：<https://kalilinuxtutorials.com/tornado/>

[![](img/aeba7c2f43a8e2ad92501fb3890351ce.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj9fDMDQK3Rc4jRBnZ5jBdZEQC5aLijrQPq9fI1qjYEHZQXj7eJ7N019fx0Puk6gWhMawJsV-TjIgIxVx2r4-JyLxkXLJAKH3MQjyKa--9CwAopBdwqREuT6TVDN6OWFB4lLM6EiN2LzMFPwqsE-UKjYLoZFBGMEdrDWuSwkZyBAJ59jtVMiJnhjMll/s728/twister%20logo%20(1).png)

Tornado 是用 metasploit-framework 工具和 msfvenom 模块实现 tor 网络的，你可以很容易地为你的本地主机创建隐藏服务。没有端口转发的洋葱域。如果您体验过不同的远程管理工具，可能您知道您需要虚拟专用网络或 ngrok 的转发端口，但在这种意义上，tornado 网络提供了一种可能性，通过利用它提供的匿名性，从而防止机器的真实位置被暴露，使机器中的服务可以作为隐藏服务访问，而无需端口转发。

龙卷风能做什么

*   用 tor 网络创建隐藏服务
*   生成跨平台的 msfvenom 有效负载，外壳代码执行完全不可检测，而不是 shikata_ga_nai 的东西
*   隐藏服务在 tor 网络之外变得可用，并准备好反向外壳连接

小心 tor2web 甚至洋葱网，唯一的自杀任务就是戴眼罩。从受害者的角度来看，tornado 是不安全的:tor 的要点是用户可以在不被窃听的情况下使用 tor2web 通过 clearnet 进行连接，即使使用 https 也会严重削弱保护用户的努力。

### 建有

*   突岩
*   Metasploit
*   Tor2Web

## 开始使用

要启动并运行本地副本，请遵循以下简单步骤。

### 安装

*   克隆回购

**$ git 克隆 https://github . com/same at-g/tornado . git**

*   用需求包设置 tornado

**$ sudo python 3 setup . py install**

*   用 sudo 权限运行它

**$须藤龙卷风**

## 使用

*   使用 sudo 权限运行 tornado 启动标志

**$须藤龙卷风-开始**

[**Download**](https://github.com/samet-g/tornado)