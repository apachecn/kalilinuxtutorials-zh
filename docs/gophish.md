# gophish:开源钓鱼工具包

> 原文：<https://kalilinuxtutorials.com/gophish/>

[![](img/ecea864e2154218183c31bb05135e5d0.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhuFsf2GslLtvNzepjO3IHwxX17RbcnEZcSs2Erb2YhAtjYVm1daRQcofm8npETp5BAiRReelhRD681-mG06aYJo9-w1L0MbvOnIuHiuB-rebkHBSb_VW7OIAbusAjObyAJs8atyJtbUNpTeIl3xUluDCdjrh_Dp5Ul5nJETl2uD502d2uHtd-34FbD/s728/logo%20(1).png)

Gophish 是一个为企业和渗透测试者设计的开源钓鱼工具包。它能够快速轻松地设置和执行网络钓鱼服务和安全意识培训。

### 安装

Gophish 的安装非常简单——只需下载并解压包含您的系统版本的 zip 文件，然后运行二进制文件。Gophish 有针对 Windows、Mac 和 Linux 平台的二进制版本。

### 从源头构建

**如果你是从源码构建，请注意 Gophish 需要 Go v1.10 或以上版本！**

要从源代码构建 Gophish，只需将`**go install github.com/gophish/gophish@latest**`和`**cd**`运行到项目源代码目录中。然后，运行 **`go build`。在这之后，你应该在当前目录中有一个名为`**gophish**`的二进制文件。**

### 码头工人

你也可以通过官方 Docker 容器使用 Gophish。

### 设置

运行 Gophish 二进制文件后，打开 Internet 浏览器，打开 https://localhost:3333，使用日志输出中列出的默认用户名和密码登录。例如

**time = " 2020-07-29t 01:24:08Z " level = info msg = "请使用用户名 admin 和密码 4304d5255378177d 登录"**

Gophish v 0 . 10 . 1 之前的版本默认用户名为`**admin**`，密码为`**gophish**`。

[**Download**](https://github.com/gophish/gophish)