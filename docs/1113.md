# Gophish:开源钓鱼工具包

> 原文：<https://kalilinuxtutorials.com/gophish-open-source-phishing-toolkit/>

[![Gophish : Open-Source Phishing Toolkit](img/8c3457f628bfe137f7ae8439335af4c8.png "Gophish : Open-Source Phishing Toolkit")](https://1.bp.blogspot.com/-bxuBbc3wnHw/Xii2v9pp20I/AAAAAAAAEiA/ezSeNti-uwY3khGGu1VXT9BMrcM0jEXiQCLcBGAsYHQ/s1600/Gophish%25281%2529.png)

Gophish 是一个为企业和渗透测试者设计的开源钓鱼工具包。它能够快速轻松地设置和执行网络钓鱼服务和安全意识培训。

**安装**

Gophish 的安装非常简单——只需下载并解压包含您的系统的[版本的 zip 文件，然后运行二进制文件。Gophish 有针对 Windows、Mac 和 Linux 平台的二进制版本。](https://github.com/gophish/gophish/releases/)

**也可阅读-[blue wall:专为进攻型&防御型网络专家](https://kalilinuxtutorials.com/bluewall/)设计的防火墙框架**

**从源构建**

**如果你是从源码构建，请注意 Gophish 需要 Go v1.10 或以上版本！**

要从源代码构建 Gophish，只需在项目源代码目录中运行`**go get github.com/gophish/gophish**`和 **`cd`** 。然后，运行`**go build**`。在这之后，在当前目录中应该有一个名为`**gophish**`的二进制文件。

**码头工人**

你也可以通过一个非官方的 Docker 容器[在这里](https://hub.docker.com/r/matteoggl/gophish/)使用 Gophish。

**设置**

运行 gophish 二进制文件后，打开互联网浏览器进入 [https://localhost:3333](https://localhost:3333) ，使用默认用户名(admin)和密码(Gophish)登录。

[**Download**](https://github.com/gophish/gophish)