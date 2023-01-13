# 丽塔:真正的情报威胁分析

> 原文：<https://kalilinuxtutorials.com/rita-real-intelligence-threat-analytics/>

[![RITA : Real Intelligence Threat Analytics](img/fd7b29c784e35b131ffed86cc35c2831.png "RITA : Real Intelligence Threat Analytics")](https://1.bp.blogspot.com/-BMPCxf482Lo/XagJYdtSbEI/AAAAAAAAC_0/lCONZknz2mQmIUM_Vs1cuPaotnBczej1wCLcBGAsYHQ/s1600/rita-logo%2B%25281%2529.png)

**丽塔**是一个真正的情报威胁分析。RITA 是一个用于网络流量分析的开源框架。

该框架吸收 TSV 格式的 Bro/Zeek 日志，目前支持以下主要特性:

*   信标检测:搜索网络内外的信标行为迹象
*   DNS 隧道检测搜索基于 DNS 的隐蔽通道的迹象
*   黑名单检查:查询黑名单以搜索可疑的域和主机

**自动安装**

**Ubuntu 16.04 LTS、Security Onion*和 CentOS 7** 正式支持自动安装程序

*   从发布页面下载最新的`**install.sh**`文件
*   使安装程序可执行:`**chmod +x ./install.sh**`
*   运行安装程序:`**sudo ./install.sh**`

**入门**

**系统要求:**

*   **操作系统**——首选平台是 64 位 Ubuntu 16.04 LTS。应该使用 apt-get 对系统进行修补并使其保持最新。
*   **处理器**(当与 Bro/Zeek 一起安装时)–两个内核加上一个额外的内核，用于捕获每 100 Mb 的流量。(至少三个内核)。这应该是专用硬件，因为其他虚拟机的资源拥塞可能会导致数据包被丢弃或丢失。
*   **内存**–最低 16GB。如果监控 100Mb 或更多的网络流量，则为 64GB。128GB，如果监控 1Gb 或更多的网络流量。
*   **存储**–最低 300GB。建议使用 1TB 或更大容量，以减少日志维护。
*   **网络**–为了使用 Bro/Zeek 捕获流量，您至少需要 2 个网络接口卡(NIC)。一个用于系统管理，另一个是专用捕获端口。英特尔网卡性能良好，值得推荐。

**也可阅读-[Mosca:手动搜索工具，像 Grep Unix 命令](https://kalilinuxtutorials.com/mosca-search-tool-bugs-grep-unix-command/)一样查找 Bugs】**

**配置文件**

RITA 的配置文件位于`**/etc/rita/config.yaml**`位置，尽管您可以使用`**-c**`命令行标志在单个命令上指定自定义路径。

**注:**

*   必须对`**Filtering: InternalSubnets**`部分*进行*配置，否则您将无法在某些模块中看到任何结果(例如信标、长连接)。如果您的网络使用标准 RFC1918 内部 IP 范围(10.0.0.0/8、172.16.0.0/12、192.168.0.0/16 ),您只需取消配置文件中已有的默认`**InternalSubnets**`部分的注释即可。否则，请根据您的环境调整这一部分。RITA 的主要目的是发现与外部系统通信的受损内部系统的迹象，并将自动从部分分析中排除内部到内部的连接和外部到外部的连接。

您可能还希望更改以下选项的默认值:

*   `**Filtering: AlwaysInclude**`–此处列出的范围不受`**InternalSubnets**`设置的过滤。其主要用途是包含内部 DNS 服务器，以便您可以看到任何 DNS 查询的来源。

请注意，`**Filtering**`部分中列出的任何值都应采用 CIDR 格式。因此，`**192.168.1.1**`的单个 IP 将被写成`**192.168.1.1/32**`。

**获取数据(生成 Bro/Zeek 日志):**

*   **选项 1** :在 Bro/Zeek 之外生成 PCAPs
    *   使用数据包嗅探器(tcpdump、wireshark 等)生成 PCAP 文件。)
    *   (可选)将多个 PCAP 文件合并为一个 PCAP 文件
        *   `**mergecap -w outFile.pcap inFile1.pcap inFile2.pcap**`
    *   从 PCAP 文件生成 Bro/Zeek 日志
        *   `**bro -r pcap_to_log.pcap local "Log::default_rotation_interval = 1 day"**`
*   **选项 2** :安装 Bro/Zeek，让它直接监控一个界面【说明】
    *   出于性能原因，您可能希望从源代码编译 Bro/Zeek。这个脚本可以帮助自动化这个过程。
    *   默认情况下，RITA 的自动安装程序会安装预编译的 Bro/Zeek 二进制文件
        *   如果您打算从源代码编译 Bro/Zeek，请在运行安装程序时提供`**--disable-bro**`标志

**与丽塔一起导入和分析数据**

安装 RITA、设置配置文件的`**InternalSubnets**`部分并收集一些 Bro/Zeek 日志后，您就可以开始搜索了。

过滤和白名单在导入时进行。这些可选设置可以在配置文件中的`**InternalSubnets**`旁边找到。

丽塔将处理纯文本和 gzip 压缩格式的兄弟/Zeek TSV 日志。注意，如果你使用安全洋葱或 Bro 的 JSON 日志输出，你需要切换回传统的 TSV 输出。

*   **选项 1** :创建一次性数据集
    *   `**rita import path/to/your/bro_logs dataset_name**`从目录中的 Bro/Zeek 日志集合创建数据集
    *   直接位于所提供目录中的每个日志文件都将以给定的名称导入到数据集中
    *   如果您将更多数据导入同一个数据集，RITA 会自动将其转换为滚动数据集。
*   **选项 2** :创建滚动数据集
    *   滚动数据集允许您逐步分析一段时间内的日志数据。
    *   您可以像这样调用 Rita:`**rita import --rolling /path/to/your/bro_logs**`并随着新日志的生成(例如每小时一次)重复进行这个调用
    *   RITA 将数据以“块”的形式循环进出滚动数据库。您可以将每个块视为一个小时，默认情况下是数据集中的 24 个块。这提供了始终拥有最近 24 小时可用数据的能力。但是块是通用的，足以适应非默认的 Bro 日志配置或数据保留时间。

**滚动数据集**

有关滚动数据集的最简单使用情形，请参见上一节。本节涵盖了您可以定制的各种选项和更复杂的用例。

每个滚动数据集在转出数据之前都有一个可以容纳的区块总数。例如，如果数据集当前包含 24 个数据块，并被设置为最多容纳 24 个数据块，则下一个要导入的数据块将在引入新数据之前自动删除第一个数据块。

这将导致数据库仍然包含 24 个块。如果每个区块包含一小时的数据，那么您的数据集将包含 24 小时的数据。当创建滚动数据库时，您可以使用`**--numchunks**`手动指定块的数量，但是如果省略这个，RITA 将使用配置文件中的`**Rolling: DefaultChunks**`值。

同样，当导入一个新的块时，您可以用`**--chunk**`指定您希望在数据集中替换的块号。如果你不做这个，RITA 会自动为你增加数据块。

区块必须是 0(包括 0)到区块总数(不包括 0)。这必须介于 0(含)和区块总数(不含)之间。如果您尝试使用大于或等于块总数的块号，将会出现错误。

您让 RITA 导入的所有文件和文件夹都将导入到一个块中。这可能是 1 小时、2 小时、10 小时、24 小时或更长时间。RITA 不关心每个块中有多少数据，所以尽管每个块表示相同的时间量是正常的，但是每个块可以有不同的日志小时数。

这意味着您可以定期运行 RITA，而不用担心系统是否会离线一会儿或者数据是否会延迟。你得到的数据可能会比你预期的多一点或少一点，但是久而久之和新的数据被添加进去后，它会慢慢地自我修正。

**示例:**如果您想要一个包含一周数据的数据集，您可以每天运行一次下面的 rita 命令。

**rita 导入-滚动-numchunks 7/opt/bro/logs/当前周-数据集**

这将把一天的数据导入到每个块中，这样你将总共得到一周的数据。在前 7 天导入后，数据集将轮换出旧数据，以保留最近 7 天的数据。

注意，在本例中，您必须确保新的日志被添加到了`**/opt/bro/logs/current**`中。

**示例:**如果您想要一个包含 48 小时数据的数据集，您可以每小时运行以下 rita 命令。

**rita 导入–滚动–numchunks 48/opt/bro/logs/当前 48 小时-数据集**

**与丽塔一起检查数据**

*   使用 **show-X** 命令
    *   `**show-databases**`:打印当前存储的数据集
    *   `**show-beacons**`:显示 C2 软件标志的打印主机
    *   `**show-bl-hostnames**`:打印接收连接的黑名单主机名
    *   `**show-bl-source-ips**`:打印发起连接的黑名单 IP
    *   `**show-bl-dest-ips**`:打印接收连接的黑名单 IP
    *   `**show-exploded-dns**`:打印 dns 分析。暴露隐蔽的 dns 通道
    *   `**show-long-connections**`:打印长连接及相关信息
    *   `**show-strobes**`:打印出现频率过高的连接
    *   `**show-useragents**`:打印用户代理信息
*   默认情况下，RITA 以 CSV 格式显示数据
    *   `**-H**`以人类可读的格式显示数据
    *   通过`less -S`传输人类可读的结果可以防止自动换行
        *   例:`**rita show-beacons dataset_name -H | less -S**`
*   用`**html-report**`创建一个 html 报告

[Download](https://github.com/activecm/rita)