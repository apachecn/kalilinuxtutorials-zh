# Nray:分布式端口扫描器

> 原文：<https://kalilinuxtutorials.com/nray/>

[![Nray : Distributed Port Scanner](img/2964497b76d6f2da265a7f9e6fc28365.png "Nray : Distributed Port Scanner")](https://1.bp.blogspot.com/-IQUL45p14WM/Xkxv618Ih0I/AAAAAAAAFAo/qVw4gaJLbuQpnvtIzXTRpbYlVWXBUxxvwCLcBGAsYHQ/s1600/scan.png)

**Nray** 是一款免费的、平台和架构独立的端口和应用层扫描器。除了常规目标(主机/网络列表)，它还支持基于证书透明性日志或 LDAP 等来源的动态目标选择。

此外，nray 允许以分布式方式运行，以加速扫描并从不同的有利位置执行扫描。基于事件的结果允许在扫描期间进一步处理信息，例如使用 jq 等工具或 elasticsearch 或 Splunk 等成熟的数据分析平台。

Nray 是用纯 Go 编写的，它的版本控制遵循语义版本控制模型。开发遵循 Vincent Driessen 的“一个成功的 git 分支”模型，因此我们试图保持主分支稳定并与发布保持一致，而开发发生在开发分支以及从那里派生的分支上。

**大楼**

我们注意到大部分都与 go 的构建系统保持一致，这意味着项目可以用普通的 Go 构建来构建。Nray 是用纯 Go 编写的，并且注意只选择满足这个要求的依赖项，因此一个标准的 Go 安装(加上 git)足以在任何支持的平台上构建 nray。

**也可阅读-[OpenRelayMagic:用于查找易受开放中继](https://kalilinuxtutorials.com/openrelaymagic/)攻击的 SMTP 服务器的工具**

**用 makefile**

然而，有一个 makefile 被认为是用于构建生产版本(`make release`)——它确保没有 C 依赖项被链接进来，并且符号从二进制文件中被去除以节省空间。

此外，大多数常见操作系统的二进制文件是自动创建的。调用`make`将构建一个本地开发版本，为你当前的操作系统和架构定制，并链接 C 库和 Go 的 race 检测器。

**无 makefile**

只需运行`go build`-如果需要交叉编译，`GOOS`和`GOARCH`参数控制目标操作系统和架构。对于节点，可以将服务器位置和端口直接注入二进制:`go build -ldflags "-X main.server=10.0.0.1 -X main.port=8601"`。

为了获得更小的二进制文件，在调用`go build`时通过`-ldflags="-s -w"`去掉不必要的东西。

如果您需要重新构建 protobuf 模式(这不是必需的，除非您更改了网络协议！)，运行`make create-schemas`(这需要您的系统上有 protobuf 编译器)。

**贡献与发展**

只需抓取代码并修复让你烦恼的东西，或者加入新的强大功能！欢迎每一个贡献，我们的目标是让 nray 成为用户和贡献者的优秀项目！

您的代码应该通过由 go vet 和 go lint 执行的标准检查。我推荐使用启用了 Go 支持的 Visual Studio 代码，它是一个很好的 IDE，可以很早就提出这样的问题。

Nray 总是针对最新的 go 版本开发的，所以如果您在构建 nray 时遇到问题，请检查您是否安装了最新的 Go 版本。

**制造问题**

在打开问题之前，请检查

*   你看过文档了吗？
*   已经有类似的问题了吗？
*   提供尽可能多的环境信息:架构、操作系统、Go 版本、使用的配置等。
*   尝试给出重现错误的步骤
*   **请使用适当的格式，尤其是日志(代码标签)**。这大大增加了可读性和有人照顾你的问题的机会。

[**Download**](https://github.com/nray-scanner/nray)