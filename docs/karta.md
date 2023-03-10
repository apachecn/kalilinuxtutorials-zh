# karta:IDA 的源代码辅助快速二进制匹配插件

> 原文：<https://kalilinuxtutorials.com/karta/>

[![](img/630df36427d409d6a5e6ba1798c8a002.png)](https://1.bp.blogspot.com/-MHZ0YZ_pCCY/YT7BF8eOovI/AAAAAAAAKzo/lUrjg_GK2sI9nvovNj0gnNpyHoAvjkU9ACLcBGAsYHQ/s668/KartaTool.png)

**“Karta”**(俄语为“Map”)是一个 IDA Python 插件，可以识别和匹配给定二进制文件中的开源库。该插件使用一种独特的技术，使其能够支持巨大的二进制文件(> 200，000 个函数)，而对整体性能几乎没有影响。

匹配算法是位置驱动的。这意味着它的主要焦点是定位不同的编译文件，并根据它们在文件中的原始顺序匹配每个文件的函数。这样，匹配依赖于 K(开放源代码中函数的数量)而不是 N(二进制文件的大小)，从而获得显著的性能提升，因为通常 N >> K。

我们认为这个 IDA 插件有 3 个主要的用例:

*   当搜索有用的 1 天时，确定使用的开放源代码(及其版本)的列表
*   匹配受支持的开放源代码的符号，以帮助对恶意软件进行反向工程
*   匹配受支持的开源代码的符号，以帮助在专有代码中搜索 0-Days 时对二进制文件/固件进行逆向工程

**安装(Python 3 & IDA > = 7.4)**

对于最新版本，使用 Python 3，只需 git 克隆存储库并运行`setup.py install`脚本。从版本 2.0.0 及更高版本开始支持 Python 3。

**安装(Python 2 & IDA < 7.4**

截至 IDA 7.4 发布时，Karta 仅针对 IDA 7.4 或更新版本以及 Python 3 进行了积极开发。Python 2 和更早的 IDA 版本仍然支持 v1.2.0 发行版，由于 python 2，这很可能是最后一个受支持的版本。x 生命终结。

**标识符**

Karta 的标识符是一个较小的插件，用于识别二进制文件中现有(受支持的)开源库的存在和版本。不再需要一次又一次地对同一个开源库进行逆向工程，只需运行标识符插件，就可以获得所用开源的详细列表。Karta 目前支持 10 多个开源库，包括:

*   OpenSSL
*   Libpng
*   Libjpeg
*   网络 snmp
*   zlib
*   等等。

与的匹配

在确定了所使用的开放源码之后，可以为特定的库(例如 libpng 版本 1.2.29)编译一个. JSON 配置文件。一旦编译完成，Karta 将自动尝试在加载的二进制文件中匹配开源的函数(符号)。此外，如果您的开源使用了外部函数(memcpy、fread 或 zlib_inflate)，Karta 也会尝试匹配这些外部函数。

**文件夹结构**

*   **src:** 插件的源目录
*   **配置:**预供应*。JSON 配置文件(希望社区贡献更多)
*   **编译:**生成配置文件的编译技巧，以及从过去的开放源代码中获得的经验
*   **docs:** sphinx 文档目录

[**Download**](https://github.com/CheckPointSW/Karta)