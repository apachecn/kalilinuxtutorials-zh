# Bore:用于创建到本地主机的隧道的简单 CLI 工具

> 原文：<https://kalilinuxtutorials.com/bore/>

[![](img/a2e883ace0678a7de8575e7ffb65ab9b.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgdywkC1XqZrrQOBjAXVtIfKnjyhKA-lyt6k_YtC2lzSH5nJHsqpOoOvGkEXMNx8fdeSQY1bD1lxgDo2P5jp4pNTnWoUTukiybadJtFw7ZczHrEho16uhWwXjbJD-6147N3prsLWeeQ4iFUG8RUPOfBONI2dOqWzfljLLiSnNHnN5-DvVXB2xqk_53K/s728/logo%20(2)%20(1).png)

**Bore** ，Rust 中的现代简单 TCP 隧道，将本地端口暴露给远程服务器，绕过标准 NAT 连接防火墙。**这就是它所做的一切:不多也不少。**

这将把您在`**localhost:8000**`的本地端口暴露给在`**bore.pub:<PORT>**`的公共互联网，端口号是随机分配的。

类似于本地隧道和 ngrok，除了`**bore**`旨在成为一个高效、非个人化的工具，用于转发 TCP 流量，安装简单，易于自托管，没有任何附加的装饰。

(`**bore**`总共不到 400 行安全的异步 Rust 代码，设置起来很简单——只需为客户端和服务器运行一个二进制文件。)

## 安装

安装 bore 最简单的方法是通过预构建的二进制文件。这些在 macOS、Windows 和 Linux 的发布页面上提供。只需解压缩适合您的平台的文件，并将 bore 可执行文件移动到您的路径上的一个文件夹中。

你也可以使用 Cargo——Rust package manager——从源代码构建`**bore**`。该命令将`**bore**`二进制文件安装在用户可访问的路径上。

货物安装孔-cli

我们还为每个版本发布版本化的 Docker 映像。每个映像都是为 AMD 64 位和 Arm 64 位架构构建的。它们标有特定的版本，允许你从一个最小的“暂存”容器中运行静态链接的`**bore**`二进制文件。

**docker run-it–init–RM–网络主机 ekzhang/bore**

## 详细用法

本节描述了`**bore**` CLI 命令的详细用法。

### 本地转发

您可以使用`**bore local**`命令转发本地机器上的端口。这需要一个位置参数、要转发的本地端口以及一个强制的`**--to**`选项，该选项指定了远程服务器的地址。

**bore local 5000–to bore . pub**

您可以有选择地传入一个`**--port**`选项来选择要公开的遥控器上的特定端口，尽管如果该端口不可用，该命令将会失败。此外，除了环回地址`**localhost**`之外，传递`**--local-host**`还允许您暴露局域网上的不同主机。

完整的选项如下所示。

**bore-local 0.4.0
启动本地代理到远程服务器
用法:
bore local【选项】–到
:
本地端口公开
选项:
-h，–帮助打印帮助信息
-l，–local-host 本地主机公开【默认值:localhost】
-p，–port 远程服务器上可选端口选择【默认值:0】
-s，–secret 可选 SECRET 进行身份验证[env:env**

### 自托管

正如启动指令中提到的，有一个`**bore**`服务器的公共实例在`**bore.pub**`运行。但是，如果您想在自己的网络上自托管`**bore**`，可以使用以下命令:

**无聊服务器**

这就够了！在服务器在给定的地址开始运行后，您可以使用选项`**--to <ADDRESS>**`更新`**bore local**`命令，将本地端口转发到这个远程服务器。

`**bore server**`命令的全部选项如下所示。

**bore-server 0.4.0
运行远程代理服务器
用法:
bore server【选项】
选项:
-h，–help 打印帮助信息
–min-port 接受的最小 TCP 端口号【默认值:1024】
-s，–secret 可选 SECRET 进行认证【env:BORE _ SECRET】
-V，–version 打印版本信息**

## 草案

在`**7835**`处有一个隐式的*控制端口*，用于按需创建新的连接。初始化时，客户端在 TCP 控制端口上向服务器发送“Hello”消息，请求代理选定的远程端口。然后，服务器以确认响应，并开始监听外部 TCP 连接。

每当服务器在远程端口上获得连接时，它都会为该连接生成一个安全的 UUID，并将其发送回客户端。然后，客户端向服务器打开一个单独的 TCP 流，并发送一个包含该流的 UUID 的“接受”消息。然后，服务器代理这两个连接。

出于正确性和避免内存泄漏的原因，传入的连接最多只由服务器存储 10 秒钟，如果客户机不接受它们，就被丢弃。

## 认证

在定制部署`**bore server**`时，您可以选择要求一个*秘密*来防止服务器被其他人使用。该协议要求客户端通过回答 HMAC 码形式的随机询问来验证每个 TCP 连接上的秘密的拥有。(此秘密仅用于初始握手，默认情况下不会对进一步的流量进行加密。)如果参数中不存在秘密，`**bore**`也将尝试从`**BORE_SECRET**`环境变量中读取。

[Download](https://github.com/ekzhang/bore)