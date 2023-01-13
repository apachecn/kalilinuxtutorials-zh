# 海啸安全扫描仪 2020

> 原文：<https://kalilinuxtutorials.com/tsunami/>

[![Tsunami Security Scanner 2020](img/bc241e1ea8ab05d19cb2969c0b0e80fd.png "Tsunami Security Scanner 2020")](https://1.bp.blogspot.com/-XECeIGIXAo8/Xx3Ul16q0QI/AAAAAAAAHIk/WKC3awRQ45ASJjNltU2xne2MKHv2HFg-wCLcBGAsYHQ/s1600/SUNAMI%25282%2529.png)

**Tsunami** 是一款通用网络安全扫描程序，具有可扩展的插件系统，用于高度可靠地检测高严重性漏洞。

要了解更多信息，请访问我们的[文档](https://github.com/google/tsunami-security-scanner/blob/master/docs/index.md)。

它严重依赖其插件系统来提供基本的扫描功能。该插件的所有公开可用内容都托管在一个单独的[Google/tsunami-security-scanner-plugins](https://github.com/google/tsunami-security-scanner-plugins)存储库中。

**当前状态**

*   目前它是在“前阿尔法”版本的开发者预览。
*   该项目目前正在积极开发中。未来一定会有重大的 API 变化。

**快速启动**

为了快速开始扫描，

*   安装以下必需的依赖项:`**nmap >= 7.80 ncrack >= 0.7**`
*   启动 it 可以识别的易受攻击的应用程序，例如未经验证的 Jupyter 笔记本服务器。最简单的方法是使用 docker 镜像:docker run–name unauthenticated-jupyter-notebook-p 8888:8888-d jupyter/base-notebook start-notebook . sh–notebook app . token = "
*   执行以下命令:`**bash -c "$(curl -sfL https://raw.githubusercontent.com/google/tsunami-security-scanner/master/quick_start.sh)"**`

`**quick_start.sh**`脚本执行以下任务:

*   将[Google/tsunami-security-scanner](https://github.com/google/tsunami-security-scanner)和[Google/tsunami-security-scanner-plugins](https://github.com/google/tsunami-security-scanner-plugins)repos 克隆到`$HOME/tsunami/repos`目录中。
*   编译所有[谷歌海啸插件](https://github.com/google/tsunami-security-scanner-plugins/tree/master/google)，并将所有插件`jar`文件移动到`$HOME/tsunami/plugins`目录。
*   编译 it scanner Fat Jar 文件，并将其移动到`$HOME/tsunami`目录。
*   将`tsunami.yaml`示例配置移动到`$HOME/tsunami`目录中。
*   使用先前生成的工件命令扫描`127.0.0.1`的打印示例。

**投稿**

阅读如何[为海啸](https://github.com/google/tsunami-security-scanner/blob/master/docs/contributing.md)做贡献。

**免责声明**

它不是谷歌的官方产品。

[**Download**](https://github.com/google/tsunami-security-scanner)