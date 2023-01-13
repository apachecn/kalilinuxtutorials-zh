# Jfscan:基于 Masscan 和 NMap 的超快速可定制端口扫描仪

> 原文：<https://kalilinuxtutorials.com/jfscan/>

[![](img/c184b4561f08f4a616f34d5b6b942a67.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiPxuENji127ZeDlsCnFPK67JRJAGdhUa8a1pJ-dbx8-Qm7Q6o-Nmw_HrEbExdB5ySxJ9Eso7439ay2kDG9sVj1HEAk_yisrj0jgAED61iK9iAMWjW6-I0XtrnWbzTfMqw1fepCDBhAUvEZT1RMyTVUsc3oa9JKqMr3ucWigI2BxZQI12LA4THVrP_v/s728/logo%20(1).png)

JFScan 是一个超高速端口扫描仪 Masscan 的包装器。它旨在简化在各种格式的目标上扫描开放端口的工作。JFScan 接受以下形式的目标:URL、域或 IP(包括 CIDR)。您可以使用参数或使用 stdin 来指定带有目标的文件。

JFScan 还允许您只输出结果，并与其他工具(如 Nuclei)链接。如果您希望发现 web 应用程序中的漏洞，那么 JFScan 的 domain:port 输出是至关重要的，因为虚拟主机决定将提供哪些内容。

最后，它可以用 Nmap 扫描发现的端口。您还可以定义自定义选项，并使用 Nmap 惊人的脚本功能。

## 特征

*   使用 Nmap 执行大规模扫描！允许您使用 Masscan 扫描目标，并通过自定义设置在检测到的端口上执行 Nmap。类固醇上的 Nmap。*
*   扫描各种格式的目标，包括域名！
*   结果可以以域:端口格式生成。
*   它在 stdin/stdout 模式下工作，允许您向/从其他工具传输结果。
*   自动调整 masscan 的数据包速率，因此您不必这样做(通过–disable-auto-rate 禁用它)。
*   生成标准的 Nmap XML 报告。
*   完全支持 IPv6。
*   支持范围控制，仅扫描范围中定义的目标。

## 使用

**用法:JFScan[-h][–TARGETS TARGETS](-p PORTS |–TOP-PORTS TOP _ PORTS |–yummy-PORTS)[–RESOLVERS RESOLVERS][–enable-IPV6][–SCOPE SCOPE][–r MAX _ RATE][–WAIT][–disable-auto-RATE][–I INTERFACE][–SOURCE-IP SOURCE _ IP]
[–ROUTER-IP ROUTER _ IP][–ROUTER _ MAC][–ROUTER-MAC-MAC-IPV6 ROUTER _ MAC _ IPV6][-oi][-oi] 可以是一个范围或端口列表:0-65535 或 22，80，100-500，…
–TOP-PORTS TOP _ PORTS
仅扫描 N 个顶级端口，例如–TOP-PORTS 1000
–yummy-PORTS 仅扫描最美味的端口
-q，–quite output only results
-v，–verbose verbose output
–nmap 在发现的端口上运行 nmap
–nmap 默认 8
–NMAP-OUTPUT NMAP _ OUTPUT
以标准 XML 格式将结果从 nmap 输出到指定的文件(与 nmap 选项-oX 相同)
目标一个或多个目标，用逗号分隔，可接受的格式为:域名、IPv4、IPv6、URL
–目标带目标的文件，可接受的格式为:域名、IPv4、IPv6、URL
-oi，–only-IPS 仅输出 IP 地址，默认:所有资源
-od，–only-domains 仅输出域，默认 –OUTPUT OUTPUT
将 masscan 的结果输出到指定文件
–RESOLVERS RESOLVERS
用逗号分隔的自定义解析器，例如 8.8.8.8，1 . 1 . 1 . 1
–enable-ipv6 启用 IPv6 支持，否则在扫描过程中将忽略所有 IPv6 地址
–SCOPE 使用 IP 地址和 CIDR 控制作用域的作用域文件路径，预期格式:IPv6、IPv4、IPv6 CIDR、IPv4 CIDR
-r MAX_RATE， –MAX-RATE MAX _ RATE
masscan 的最大 kpps 速率
–等待等待数据包到达的秒数(扫描大型网络时)，masscan 的选项
–disable-auto-RATE 禁用 mass can 的速率调整机制(更多误报/漏报)
-i 接口， –接口接口
mass can 和 nmap 使用的接口
–SOURCE-ip SOURCE _ IP
mass can 接口的 IP 地址
–ROUTER-IP ROUTER _ IP
mass can 路由器的 IP 地址
–ROUTER-mac ROUTER _ MAC
mass can 路由器的 MAC 地址
–ROUTER-MAC-IPV6 ROUTER _ MAC _ IPV6
mass can IPV6 路由器的 MAC 地址
–版本显示程序的**

运行前，请遵循安装说明。不要在根目录下运行 JFScan，因为我们在 masscan 二进制文件上设置了特殊权限，所以不需要。

## 举例

仅扫描速率为 10 kpps 的端口 80 和 443 的目标:

`**$ jfscan -p 80,443 --targets targets.txt -r 10000**`

前 1000 个端口的扫描目标:

`**$ jfscan --top-ports 1000 1.1.1.1/24**`

您还可以在 stdin 上指定目标，并通过管道将其传送到 nuclei:

`**$ cat targets.txt | jfscan --top-ports 1000 -q | httpx -silent | nuclei**`

或者作为位置参数:

`**$ jfscan --top-ports 1000 1.1.1.1/24 -q | httpx -silent | nuclei**`

或者同时扫描所有内容，JFScan 并不关心，而是扫描所有指定的目标:

`**$ echo target1 | jfscan --top-ports 1000 target2 --targets targets.txt -q | httpx -silent | nuclei**`

利用 nmap 收集有关已发现服务的更多信息:

`**$ cat targets.txt | jfscan -p 0-65535 --nmap --nmap-options="-sV --scripts ssh-auth-methods"**`

targets.txt 可以包含以下形式的目标(类似于 IPv6):

**http://domain.com/
domain.com
1.2.3.4
1 . 2 . 3 . 0/24
1 . 1 . 1 . 1-1 . 1 . 1 . 30**

# 装置

*   安装前，确保安装了最新版本的 Masscan(测试版本为 1.3.2)。

首先，安装一个 libpcap-dev(基于 Debian 的发行版)或 libcap-devel(基于 Centos 的发行版):

**sudo 安装 libpcap-dev**

接下来，克隆官方存储库并安装:

**sudo apt-get–assume-yes 安装 git make gcc
git 克隆 https://github.com/robertdavidgraham/masscan
CD mass can
make
sudo make 安装**

Masscan 需要 root 权限才能运行。由于在 root 下运行二进制文件不是一个好主意，我们将为二进制文件设置一个 CAP_NET_RAW 功能:

**sudo setcap CAP _ NET _ RAW+EP/usr/bin/mass can**

安装 JFscan 需要 python3 和 pip3。

sudo 安装 python3 python3-pip

安装 JFScan:

**$ git 克隆 https://github.com/nullt3r/jfscan.git
$ CD jfscan
$ pip 3 安装。**

如果您不能从命令行直接运行 jfscan，那么您应该检查$HOME/是否正确。local/bin 位于您的路径中。

将下面一行添加到您的**或`~/.bashrc`中:**

**导出路径="$HOME/。local/bin:$PATH"**

[**Download**](https://github.com/nullt3r/jfscan)