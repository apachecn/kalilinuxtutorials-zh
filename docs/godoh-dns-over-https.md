# GoDoH:HTTPS C2 域名系统

> 原文：<https://kalilinuxtutorials.com/godoh-dns-over-https/>

[![GoDoH : A DNS-Over-HTTPS C2](img/bcdfd945a83da255dfecf03fd79c7178.png "GoDoH : A DNS-Over-HTTPS C2")](https://1.bp.blogspot.com/-3IeRZ0kFF40/XVwsVMZueBI/AAAAAAAACFM/jBLiukxVGv46wD-eTLgODHeK_rDETb48QCLcBGAs/s1600/images.png)

GoDoH 是一个概念验证的命令和控制框架，用 Golang 编写，使用 HTTPS 域名系统作为传输媒介。目前支持的提供商包括 Google、Cloudflare，但也包含使用传统 DNS 的能力。

**安装**

你所需要的只是`godoh`二进制文件本身。二进制文件可以从[发布](https://github.com/sensepost/goDoH/releases)页面下载，作为标记发布的一部分。

要从源代码构建`godoh`,请遵循以下步骤:

*   确保您已经安装了[dep](https://github.com/golang/dep)(`**go get -v -u github.com/golang/dep/cmd/dep**`)
*   将这个库克隆到您的`**$GOPATH**` **的** `**src/**`目录中，这样它就在`**sensepost/godoh**`中了
*   运行`**dep ensure**`来解决依赖性
*   运行`**make key**`生成用于通信的唯一加密密钥
*   使用`go`构建工具，或者运行`**make**`在`**build/**`目录中构建二进制文件

**也可阅读-[服务列表&如何声明带有悬空 DNS 记录的子域](https://kalilinuxtutorials.com/subdomain-dangling-dns-records/)**

**用途**

$ godoh-h
A DNS(over-HTTPS)C2
版本:dev
By @ leonjza from @ sense post
**用法:** godoh【命令】
**用法:** godoh【命令】
**可用命令:** 代理连接到 DoH C2
c2 启动 godoh C2 服务器
帮助帮助关于任何命令
接收 A(即:example.com)
-h，–帮助 godoh 的帮助
-p，–提供者字符串首选 DNS 提供者使用。[可能:google，cloudflare，raw](default)
使用“godoh[command]–help”获取关于命令的更多信息。

[**Download**](https://github.com/sensepost/goDoH)