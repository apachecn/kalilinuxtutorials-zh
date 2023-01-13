# 广阔:跨越空间和时间的可见性

> 原文：<https://kalilinuxtutorials.com/vast/>

[![VAST : Visibility Across Space And Time](img/2559ff7da47124caf033cac8a3c1eb47.png "VAST : Visibility Across Space And Time")](https://1.bp.blogspot.com/-idVr5bTCrRk/YKUBJJ2t-XI/AAAAAAAAJJE/jQVU2U-83x0y3VGIsmnZila3frGCohnEQCLcBGAsYHQ/s728/vast-svg.png)

VAST 是网络遥测引擎的一个工具，用于数据驱动的安全调查。

**主要特征**

*   **高通量摄取**:导入超过 100k 事件/秒的众多日志格式，包括 [Zeek](https://www.zeek.org/) 、 [Suricata](https://suricata-ids.org/) 、JSON、CSV。
*   **低延迟查询**:由于多级位图索引和 actor 模型并发，整个数据湖的响应时间不到一秒。特别有助于对整个数据集进行即时指示器检查。
*   **灵活导出**:访问通用文本格式(ASCII、JSON、CSV)、二进制形式(MRT、PCAP)的数据，或通过 [Apache 箭头](https://arrow.apache.org/)经由零拷贝中继进行任意下游分析。
*   **强大的数据模型和查询语言**:通用的半结构化数据模型允许以类型化的方式表达复杂的数据。一种直观的查询语言，在规模上类似于 grep 和 awk，支持通过特定于域的操作对数据进行强大的子集化，例如 top- *k* 前缀搜索 IP 地址和子集关系。
*   **模式旋转**:在相关事件之间导航的缺失链接，例如，提取给定 IDS 警报的 PCAP，或者定位给定查询的所有相关日志。

**变得广阔**

Linux 用户可以通过浏览器或 cURL 下载我们最新的静态二进制版本。

**curl-L-O https://storage . Google APIs . com/tenzir-public-data/vast-static-builds/vast-static-latest . tar . gz**

打开归档文件。它包含三个文件夹**、`etc`、`**share**`。首先，直接调用`**bin**`目录中的二进制文件。**

tar xfz vast-static-latest.tar.gz
bin/vast-help

要为您的本地用户正确安装 VAST，只需将解压缩的文件夹放在`**/usr/local/**`中。

FreeBSD 和 macOS 用户必须从源代码开始构建。克隆`**master**`分支以获得 VAST 的最新版本。

**git 克隆–递归 https://github.com/tenzir/vast**

一旦所有依赖项就绪，使用以下命令构建 VAST:

**cmake-B build
cmake–build build
ctest–test-dir build
cmake–build build–目标集成
cmake–install build[–prefix/path/to/prefix]**

对于定制编译选项，您可以将`**-DCMAKE_OPTION=foo**`传递给 cmake 调用，或者在构建目录中使用`**ccmake**`。

[安装指南](https://github.com/tenzir/vast/blob/master/INSTALLATION.md)包含关于如何构建和安装 VAST 的更详细和特定于平台的说明。

**入门**

下面是一些命令，让你先睹为快。

**启动一个巨大的节点**:

**浩瀚开始**

**摄取 [Zeek](http://www.zeek.org/) 各种日志**:

**zcat * . log . gz | vast import zeek**

**运行过去一个小时的查询，呈现为 JSON**

**浩瀚导出 json ':时间戳> 1 小时前&&(6.6.6.6 | | 5353/UDP)'**

**摄取一个 [PCAP](https://en.wikipedia.org/wiki/Pcap) 跟踪，带有一个 1024 字节的流量中断**:

**浩瀚进口 pcap -c 1024 < trace.pcap**

**对 PCAP 数据进行查询，按时间对数据包进行排序，并将其送入** `tcpdump`:

**浩浩出口 pcap " sport>60000/TCP&&src！in 10 . 0 . 0 . 0/8 " \
| ipsumdump–collate-w-\
| tcpdump-r--nl**

[**Download**](https://github.com/tenzir/vast)