# LiveTargetsFinder:生成用于定位的实时主机和 URL 的列表，自动使用 MassDNS

> 原文：<https://kalilinuxtutorials.com/livetargetsfinder/>

[![](img/0274ff94989ec832d4badd779a114d0a.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiZrkEN8ImDoLTmaLKam6QHEgvMqwfUBgCKvstdUUBNRN2mzEnPg7Rqfm5sWMhSnf2r-9sZ4_vs0FkX74n5zuoEYjmEDK4iov7aLS0XgdRC1a0Rnm_tFhqsC5Z0UrAONg7cQ84bLhhmqamLFd_p6uDy7dPF6Ovq_jiieAPAFTU6wex3fcXHSVe1KVcD/s728/download%20(2).png)

**LiveTargetsFinder** ，生成实时主机和 URL 的列表用于定位，自动使用 Massdns、Masscan 和 nmap 过滤掉无法访问的主机

给定一个域名输入文件，该脚本将自动使用 MassDNS 过滤掉无法解析的主机，然后将结果传递给 Masscan，以确认主机是否可达以及在哪个端口上。然后，该脚本将生成一个完整的 URL 列表，用于进一步定位(传递到 gobuster 或 dirsearch 之类的工具中，或者发出 HTTP 请求)、一个可到达的域名列表和一个可到达的 IP 地址列表。作为可选的最后一步，您可以在这个缩减的主机列表上运行 nmap 版本扫描，验证早期可访问的主机是否已启动，并从它们的开放端口收集服务信息。

## 概述

该脚本对于大型域集特别有用，例如从具有数千个子域的 apex 域收集的子域枚举。对于这些大型列表，nmap 扫描会花费很长时间。这里的目标是首先使用精度较低但速度更快的 MassDNS，通过移除无法解析的域来快速减小输入列表的大小。然后，Masscan 将能够从 MassDNS 获取输出，并进一步确认主机是否可达以及在哪些端口上。然后，脚本将解析这些结果，并生成发现的活动主机列表。

现在，主机列表应该减少到足以适合进一步扫描/测试。如果您想更进一步，您可以告诉脚本在可访问主机列表上运行 nmap 扫描，对于较短的主机列表，这应该会花费更多的时间。运行 nmap 后，Masscan 给出的任何假阳性都将被过滤掉。原始 nmap 输出将以常规 nmap XML 格式存储，来自版本检测的附加信息将被添加到 SQLite 数据库中。

## 装置

**如果使用 nmap 扫描选项，该工具假定您已经安装了 nmap**

*注意*:仅当您尚未安装 MassDNS 和 Masscan，或者您希望在此 repo 中重新安装它们时，才需要运行安装脚本。如果不运行该脚本，可以提供相应可执行文件的路径作为参数。该脚本还期望 MassDNS 中包含的解析器列表位于 **`{massDNS_directory}/lists/resolvers.txt`。**

**git 克隆 https://github.com/allyomalley/LiveTargetsFinder.git
CD LiveTargetsFinder
sudo pip 3 install-r requirements . txt**

*(OPTIONAL)*

**chmod +x install_deps.sh
。/install_deps.sh**

如果您尚未安装 MassDNS 和 Masscan，并且希望自己安装它们，请参阅说明文件:

## 使用

python 3 livetargetsfinder . py[domain list][选项]

| 旗 | 描述 | 默认 | 需要 |
| --- | --- | --- | --- |
| `**--target-**`**`list`** | 包含域列表的输入文件，例如 google.com |  | 是 |
| `**--massdns-path**` | 非默认情况下，MassDNS 可执行文件的路径 | *。/massdns/bin/massdns* | 不 |
| `**--masscan-path**` | 非默认情况下，Masscan 可执行文件的路径 | *。/masscan/bin/masscan* | 不 |
| `**--nmap**` | 在收集的实时主机上运行 nmap 版本检测扫描 | *禁用* | 不 |
| `**--db-path**` | 如果使用–nmap 选项，请提供要附加到的数据库的路径(如果不存在，将创建该路径) | *output/livetargetsfinder . sqlite3* | 不 |

*   请注意，Masscan 和 MassDNS 设置是硬编码在 liveTargetsFinder.py 中的，您可以随意编辑它们(第 87 + 97 行)。
*   由于这个工具是为非常大的列表而设计的，我调整了许多设置，试图平衡速度、准确性和网络限制——这些都可以调整，以适应您的需求和带宽。
*   Masscan **的默认设置仅扫描端口 80 和 443** 。
    *   **`-s`，(`--hashmap-size`** )是出于性能原因而特别选择的——您可能能够增加这个值。
    *   完整的 MassDNS 参数:
        *   `**-c 25 -o J -r ./massdns/lists/resolvers.txt -s 100 -w massdnsOutput -t A targetHosts**`
        *   证明文件
*   另一个值得注意的设置是 Masscan 的`**--max-rate**`参数——您可能希望对此进行调整。
    *   完整质量扫描参数:
        *   `**-iL ipFile -oD masscanOutput --open-only --max-rate 5000 -p80,443 --max-retries 10**`
        *   证明文件
*   默认 nmap 设置**仅扫描端口 80 和 443** ，使用定时 T4 和一些 NSE 脚本。
    *   完整的 nmap 参数:
        *   `**--script http-server-header.nse,http-devframework.nse,http-headers -sV -T4 -p80,443 -oX {output.xml}**`

## 举例

已运行安装脚本:

**python 3 livetargets finder . py–target-list victim _ domains . txt**

未运行安装脚本:

**python 3 livetargetsfinder . py–target-list victim _ domains . txt–mass DNS-path../mass DNS/bin/mass DNS–mass can-path../masscan/bin/masscan**

## 输出

输入:victimDomains.txt

| 文件 | 描述 | 例子 |
| --- | --- | --- |
| output/victim domains _ target URLs . txt | 可访问的实时 URL 列表 | http://github.com https://github.com |
| output/victimDomains _ domains _ alive . txt | 实时域名列表 | google.com github.com |
| output/victimDomains _ IPS _ alive . txt | 实时 IP 地址列表 | 10.1.0.200, 52.3.1.166 |
| *提供的或默认的数据库路径* | SQLite 数据库存储实时主机及其服务运行信息 |  |
| output/victimDomains _ mass DNS . txt | 来自 MassDNS 的原始输出，采用 ndjson 格式 |  |
| output/victimDomains _ mass can . txt | Masscan 的原始输出，采用 ndjson 格式 |  |
| output/victimDomains_nmap.txt | nmap 的原始输出，XML 格式 |

[Download](https://github.com/allyomalley/LiveTargetsFinder)