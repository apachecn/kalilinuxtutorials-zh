# xmap:执行互联网范围的 IPv6 和 IPv4 网络研究扫描

> 原文：<https://kalilinuxtutorials.com/xmap-2/>

[![](img/12aa2aedaae709cf4c928bed172a9013.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgAe_VrXKSx1oSBxnOiibeEy59uOqpxmDYkWv-bKI5VlNMZuu1W4cL68ZAw_9cV-SmEpij_4MaRhDm801aj7E7FjGyZowx2ON_uY1LLNFmE3HgATZA2VCs_B5fRFz4O4ZcAnb_HvdV4XEr2sOoA8SFeMqq7pP8gtwzohd-WMb71zwXMsFwHYUxu8pFw/s676/ggalle990.png)

xmap 是一种工具，用于执行互联网范围的 IPv6 & IPv4 网络研究扫描

# 安装和构建 XMap

## 通过软件包管理器安装

XMap 在 GNU/Linux、macOS 和 BSD 上运行。

与大多数操作系统软件包管理器一起安装尚未集成。

| 操作系统（Operating System） |  |
| --- | --- |
| Fedora 19+或 EPEL 6+ | `-` |
| Debian 8+或 Ubuntu 14.04+ | `-` |
| 巴布亚企鹅 | `-` |
| macOS(使用自制软件) | `-` |
| Arch Linux | `-` |

## 从源头构建

### 安装 XMap 依赖项

XMap 具有以下依赖关系:

*   CMake–跨平台、开源的构建系统
*   GMP 用于任意精度算法的免费库
*   gen getop–C 程序的命令行选项解析
*   libpcap——著名的用户级数据包捕获库
*   flex 和 by ACC–输出过滤器词法分析器和解析器生成器
*   json-C——用 C 语言实现 JSON
*   libunistring–C 语言的 Unicode 字符串库
*   libnet

此外，以下可选软件包支持可选的 XMap 功能:

*   hire dis–C 中的 RedisDB 支持

使用以下命令安装所需的依赖项。

*   在基于 Debian 的系统上(包括 Ubuntu):

*   **sudo apt-get install build-essential cmake libg MP 3-dev genge topt libpcap-dev flex by ACC libjson-c-dev pkg-config libunistring-dev**

在基于 RHEL 和 Fedora 的系统上(包括 CentOS):

**sudo yum 安装 cmake GMP-devel gengetpt libpcap-devel flex by ACC JSON-c-devel libunistring-devel**

### 发展笔记

*   启用开发会打开调试符号，并关闭优化。发布版本应该用`**-DENABLE_DEVELOPMENT=OFF**`构建。
*   启用`**log_trace**`会对性能产生重大影响，除非在早期开发阶段，否则不应使用。发布版本应该用`**-DENABLE_LOG_TRACE=OFF**`构建。
*   默认情况下，不启用 Redis 支持。如果你想在 Redis 中使用 XMap，你首先需要安装 hiredis。然后用`**-DWITH_REDIS=ON**`运行 cmake。Debian/Ubuntu 已经把 hiredis 打包成`**libhiredis-dev**`；Fedora 和 RHEL/CentOS 将其包装为`hiredis-**devel**`。
*   为像 Fedora 和 RHEL 这样的系统构建包需要一个用户可定义的目录(buildroot)来存放文件。尊重这个前缀的方法是用`**-DRESPECT_INSTALL_PREFIX_CONFIG=ON**`运行 cmake。
*   使用 ronn 工具，从存储库中的`**.ronn**`源文件生成联机帮助页(及其 HTML 表示)。这不会作为构建过程的一部分自动发生；要重新生成手册页，您需要运行`**make manpages**`。这个目标假设`**ronn**`在你的路径上。
*   使用某些版本的 CMake 构建可能会因`**unable to find parser.h**`而失败。如果发生这种情况，请尝试更新 CMake。如果仍然失败，不要将 XMap 克隆到包含字符串`**.com**`的路径中，然后重试。
*   XMap 可以用`**CMAKE_INSTALL_PREFIX**`选项安装到另一个目录。例如，在`**$HOME/opt**`运行中安装它

**cmake-DC make _ INSTALL _ PREFIX = $ HOME/opt。
制造-j4
制造安装**

[**Download**](https://github.com/idealeer/xmap/blob/master/INSTALL.md)