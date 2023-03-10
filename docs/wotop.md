# 任何协议之上的网络

> 原文：<https://kalilinuxtutorials.com/wotop/>

[![Wotop : Web On Top Of Any Protocol](img/babea640e34a2d98296bc5ddbb25a353.png "Wotop : Web On Top Of Any Protocol")](https://1.bp.blogspot.com/-_QKtm72QOb4/XqUwD6re_3I/AAAAAAAAGFc/Ps4UWxooq0c4auXA_lDL5bds-sE4fim6ACLcBGAsYHQ/s1600/WOTOP%25281%2529.png)

WOTOP 是一个工具，用来在标准 HTTP 通道上传输任何类型的流量。适用于代理过滤除标准 HTTP(S)流量之外的所有流量的情况。

不像其他工具，要么要求您在代理之后，让您传递任意流量(可能在初始连接请求之后)，或者只适用于 SSH 的工具，它没有这样的限制。

**工作**

假设您想使用 SSH 连接到一台您没有 root 权限的远程机器。

*   将有 7 个实体:
    *   客户端(您的计算机，在代理后面)
    *   代理人(邪恶)
    *   目标服务器(您想要 SSH 到的远程机器，从客户端)
    *   客户端工作流程
    *   目标工作流程
    *   客户端 SSH 进程
    *   目标 SSH 进程

如果没有代理，通信将类似于:

**客户端- >客户端 SSH 进程- >目标服务器- >目标 SSH 进程**

在这种情况下，建议的方法如下:

**客户端- >客户端 SSH 进程- >客户端 WOTOP 进程- >代理- >目标 WOTOP 进程- >目标 SSH 进程- >目标服务器**

它简单地将所有数据包装在 HTTP 包中，并相应地缓冲它们。

另一个更复杂的场景是，如果您有一个外部实用服务器，并且需要从代理后面访问另一个服务器的资源。在这种情况下， ***wotop*** 仍将在您的外部服务器上运行，但是不要在第二个命令(用法部分)中使用`**localhost**`，而是使用拥有主机的目标机器的主机名。

**也可阅读-[Flux-key logger:带有 Web 面板的现代 Javascript 键盘记录器](https://kalilinuxtutorials.com/flux-keylogger/)**

**用途**

在客户端机器上:

**。/wotop <客户端-跳端口> <服务器-主机名> <服务器-跳端口>**

在目标计算机上:

**。/wotop<server-hop-port><SERVER-hop-port</server-hop-port>localhost<target-port>SERVER**

(**注意**结尾的关键字服务器)

对于 SSH，目标端口应该是 22。现在，一旦这两个都运行了，您就可以对 SSH 运行以下命令:

**ssh <目标-机器-用户名> @localhost -p <客户端-跳端口>**

**注意:**关键字 server 告诉 *wotop* 连接的哪一方必须通过 HTTP。

**计划功能**

*   更好的自适应缓冲
*   更好的 CLI 标志界面
*   可选的数据加密
*   的解析。主机的 ssh/配置文件
*   远程服务器管理的 Web 界面
*   本地主机的 Web 界面
*   某些配置的守护模式

**bug**

*   目前在每个发送/接收周期后使用 100ms 睡眠来绕过一些内存错误(尚未消除)。
*   HTTP 响应可能出现在 HTTP 请求之前。让我知道，如果你知道一些代理人阻止这种反应。
*   尽管有锁，日志记录器似乎不是线程安全的。导致内存错误，因此暂时禁用。

[**Download**](https://github.com/nishitm/wotop)