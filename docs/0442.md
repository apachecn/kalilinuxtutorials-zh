# Goca:用于查找元数据和隐藏信息的扫描仪

> 原文：<https://kalilinuxtutorials.com/goca-scanner-metadata/>

Goca 是一个用 Go 编写的 FOCA 分叉，这是一个工具，主要用于在它扫描的文档中找到元数据和隐藏信息。这些文档可能在网页上，可以下载并使用扫描仪进行分析。

它能够分析各种各样的文档，最常见的是 Microsoft Office、Open Office 或 PDF 文件，但它也分析 Adobe InDesign 或 SVG 文件等。

使用搜索引擎搜索这些文档，例如:

*   谷歌
*   堆
*   达克达克戈
*   美国 Yahoo 公司(提供互联网的信息检索服务)
*   要求

然后下载文档并从图形文件中提取 EXIF 信息，甚至在下载文件之前就对通过 URL 发现的信息进行完整的分析。

**也可阅读:[cute it——IP 混淆器使一个恶意的 IP 变得更可爱一点](https://kalilinuxtutorials.com/cuteit-ip-obfuscator/)**

**用途**

从 [**版本**](https://github.com/gocaio/goca/releases) 下载编译好的包

要从源代码构建，您需要安装 Go。

**$ export go 111 module = on
$ go get。/…
$ go run goca/goca.go -h**

要从 Docker 运行它:

**$ docker build-t gocaio/goca/path/to/goca
【docker run gocaio/goca-h】**

[**Download**](https://github.com/Gocaio/goca)