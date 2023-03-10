# Sx:快速，现代，易于使用的网络扫描仪

> 原文：<https://kalilinuxtutorials.com/sx/>

[![https://1.bp.blogspot.com/-J7baMYPigdE/YO67yc2iEFI/AAAAAAAAKB4/eCH6PvKjYGM7lq9yI6QpBhzp9HlU7o68ACLcBGAsYHQ/s728/logo-svg.png](img/be36a1948fbb54de163f1c51f1d16267.png "https://1.bp.blogspot.com/-J7baMYPigdE/YO67yc2iEFI/AAAAAAAAKB4/eCH6PvKjYGM7lq9yI6QpBhzp9HlU7o68ACLcBGAsYHQ/s728/logo-svg.png")](https://1.bp.blogspot.com/-J7baMYPigdE/YO67yc2iEFI/AAAAAAAAKB4/eCH6PvKjYGM7lq9yI6QpBhzp9HlU7o68ACLcBGAsYHQ/s728/logo-svg.png)

sx 是遵循 UNIX 理念设计的命令行网络扫描器。

这个项目的目标是用干净简单的代码创建最快的网络扫描器。

**特性**

*   **⚡比 nmap 快 30 倍**
*   **ARP 扫描**:扫描您的本地网络以检测活动设备
*   **ICMP 扫描**:使用高级 ICMP 扫描技术检测实时主机和防火墙规则
*   **TCP SYN 扫描**:传统的半开扫描，查找开放的 TCP 端口
*   **TCP FIN / NULL / Xmas 扫描**:绕过某些防火墙规则的扫描技术
*   **使用任何 TCP 标志的自定义 TCP 扫描**:发送您想要的任何外来数据包，并获得在回复数据包中设置了所有 TCP 标志的结果
*   **UDP 扫描**:扫描 UDP 端口并获取完整的 ICMP 回复，以检测开放端口或防火墙规则
*   **应用程序扫描**:
    *   **SOCKS5 扫描**:通过扫描文件中的 ip 范围或 IP/端口对列表来检测实时 SOCKS5 代理
    *   **Docker 扫描**:检测监听 TCP 端口的开放 Docker 守护进程，并获取关于 Docker 节点的信息
    *   **Elasticsearch 扫描**:检测打开的 Elasticsearch 节点，并提取所有索引名称的集群信息
*   **使用有限循环乘法群在 IP 地址上随机迭代**
*   **JSON 输出支持** : sx 是专门为方便自动处理结果而设计的

**安装**

最简单的方法是从 GitHub 版本下载，并将可执行文件放在您的路径中。

**从源代码构建**

要求:

*   升级到 1.15 或更高版本
*   libpcap(如果您使用 **wireshark** ，则已经安装)

从源代码树的根目录运行:

**去建造**

**快速启动**

这里有一个简单的例子，展示了如何用 **`sx`扫描网络。**

**ARP 扫描**

扫描您的本地网络并显示连接设备的 IP 地址、MAC 地址和相关硬件供应商:

**sx arp 192.168.0.1/24**

样本输出:

**192 . 168 . 0 . 1 B0:be:76:40:05:8d TP-LINK 技术有限公司
192 . 168 . 0 . 111 80:C5:F2:0b:02:E3 azure wave 技术有限公司
192 . 168 . 0 . 171 88:53:95:2d:3c:af 苹果公司**

使用 JSON 输出:

**sx ARP–JSON 192 . 168 . 0 . 1/24**

样本输出:

**{"ip":"192.168.0.1 "、" mac":"b0:be:76:40:05:8d "、"供应商":" TP-LINK TECHNOLOGIES CO .，LTD."}
{"ip":"192.168.0.111 "、" mac":"80:c5:f2:0b:02:e3 "、"供应商":" azure wave Technology Inc . " }
{ " IP ":" 192.192**

在退出之前等待 5 秒钟以接收延迟的应答包，默认情况下`**sx**`等待 300 毫秒:

**sx ARP–退出延迟 5s 192.168.0.1/24**

每 10 秒重新扫描网络的实时扫描模式:

**sx ARP 192 . 168 . 0 . 1/24–直播 10 秒**

**TCP 扫描**

与 nmap 和其他扫描器在实际扫描之前隐式执行 ARP 请求以将 IP 地址解析为 MAC 地址不同，`**sx**`显式使用 **ARP 缓存**概念。ARP 缓存文件是一个简单的文本文件，每行包含一个 JSON 字符串( [JSONL](https://jsonlines.org/) 文件)，它具有与上面描述的 ARP 扫描 JSON 输出相同的 JSON 字段。TCP 和 UDP 等更高级协议的扫描从 stdin 读取 ARP 缓存文件，然后开始实际扫描。

这不仅简化了程序的设计，而且加快了扫描过程，因为不必每次都执行 ARP 扫描。

让我们假设实际的 ARP 缓存在`**arp.cache**`文件中。我们可以手动创建它或使用 ARP 扫描，如下所示:

**sx ARP 192 . 168 . 0 . 1/24–JSON | tee ARP . cache**

一旦我们有了 ARP 缓存文件，我们就可以运行更高级别的协议扫描，如 TCP SYN 扫描:

**cat ARP . cache | sx TCP-p 1-65535 192 . 168 . 0 . 171**

样本输出:

192 . 168 . 0 . 171 192 . 168 . 0 . 171 443

在这种情况下，我们发现端口 22 和 443 是打开的。

使用 JSON 输出进行扫描:

**cat ARP . cache | sx TCP–JSON-p 1-65535 192 . 168 . 0 . 171**

样本输出:

**{ " scan ":" tcpsyn " IP ":" 192 . 168 . 0 . 171 " port ":22 }
{ " scan ":" tcpsyn "，" IP ":" 192 . 168 . 0 . 171 " port ":443 }**

扫描多个端口范围:

**cat arp.cache | sx tcp -p 1-23，25-443 192.168.0.171**

或单个端口:

**cat ARP . cache | sx TCP-p 22443 192 . 168 . 0 . 171**

用 JSON 输出扫描文件中的 IP/端口对:

**cat ARP . cache | sx TCP–JSON-f IP _ ports _ file . jsonl**

输入文件的每一行都是一个 json 字符串，它必须包含 **ip** 和**端口**字段。

样本输入文件:

**{ " IP ":" 10 . 0 . 1 . 1 "," port ":1080 }
{ " IP ":" 10 . 0 . 2 . 2 "," port ":1081 }**

可以使用`**-a**`或`**--arp-cache**`选项指定 ARP 缓存文件:

**sx TCP-a ARP . cache-p 22443 192 . 168 . 0 . 171**

或标准输入重定向:

**sx TCP-p 22443192 . 168 . 0 . 171<ARP . cache**

您也可以使用`**tcp syn**`子命令来代替`**tcp**`:

**cat ARP . cache | sx TCP syn-p 22 192 . 168 . 0 . 171**

`**tcp**`子命令只是`**tcp syn**`子命令的简写，除非`**--flags**`选项被通过，见下文。

**VPN 接口**

`**sx**`支持虚拟网络接口扫描(wireguard、openvpn 等。)在这种情况下，**没有必要使用 arp 缓存，因为这些接口需要原始 IP 数据包而不是以太网帧作为输入。例如，扫描 vpn 网络上的 IP 地址:**

**sx TCP 10 . 1 . 27 . 1-p80–JSON**

**TCP FIN 扫描**

大多数网络扫描器试图解释扫描的结果。例如，他们说“此端口已关闭”，而不是“我收到一个 RST”。有时候他们是对的。有时候不会。这对初学者来说更容易，但当你知道自己在做什么时，你会继续试图从程序的解释中推断出到底发生了什么，尤其是对于更高级的扫描技术。

试图克服那些问题。它返回有关 TCP FIN、NULL、Xmas 和自定义 TCP 扫描的所有回复数据包的信息。该信息包含 IP 地址、TCP 端口和回复数据包中设置的所有 TCP 标志。

TCP FIN 扫描及其其他变体(NULL 和 Xmas)利用 RFC793 第 3.9 节:

航段到达

如果状态为关闭(即 TCB 不存在),则

传入数据段中的所有数据都将被丢弃。包含 RST 的输入
段被丢弃。不包含 RST 的传入数据段
导致发送一个 RST 作为响应。选择
确认和序列字段值，以使发送违规
段的 TCP 可以接受
复位序列。

因此关闭的端口应该返回带有 RST 标志的数据包。

如果状态是监听，则

任何其他控制或文本承载段(不包含 SYN)必须有 ACK，因此将被 ACK 处理丢弃。传入的 RST 数据段可能是无效的，因为它不可能是为了响应此连接实例发送的任何内容而发送的。所以你不太可能到达这里，但是如果你到达了，放下这个部分，然后返回

这里的主短语:**掉段**，返回。因此，大多数操作系统上的开放端口会丢弃包含除 SYN、ACK 和 RST 之外的任何标志的 TCP 数据包。

让我们用 TCP FIN 扫描来扫描一些关闭端口:

**cat ARP . cache | sx TCP fin–JSON-p 23 192 . 168 . 0 . 171**

样本输出:

**{"scan":"tcpfin "，" IP ":" 192 . 168 . 0 . 171 "" port ":23，" flags":"ar"}**

`**flags**`字段包含回复数据包中的所有 TCP 标志，其中每个字母代表一个 TCP 标志:

*   **`s`**-旗帜之子
*   `**a**`-【ack flag】。
*   **`f`**–鳍旗
*   `**r**`-rst 标志
*   `**p**`-psh 标志
*   `**u**`–URG 旗帜
*   `**e**`-欧洲经委会标志
*   `**c**`–CWR 标志
*   **`n`**–NS 旗

在这种情况下，我们发现端口 23 发送了设置了 ACK 和 RST 标志回复数据包(根据 rfc793，这是关闭端口的典型响应)。

如果我们扫描一个开放的端口，我们得不到响应(除非防火墙欺骗响应)。

其他类型的 TCP 扫描可以通过类推来进行。

TCP 空扫描:

**cat ARP . cache | sx TCP null–JSON-p 23 192 . 168 . 0 . 171**

TCP 圣诞节扫描:

**cat ARP . cache | sx TCP xmas–JSON-p 23 192 . 168 . 0 . 171**

**自定义 TCP 扫描**

可以使用`**--flags**`选项发送带有自定义 TCP 标志的 TCP 数据包。

让我们向指纹远程操作系统发送带有 SYN、FIN 和 ACK 标志 TCP 数据包:

**cat ARP . cache | sx TCP–flags syn，fin，ack–JSON-p 23 192 . 168 . 0 . 171**

Windows 和 MacOS 不会响应此数据包，但 Linux 会发送带有 RST 标志的回复数据包。

`**--flags**`选项的可能参数:

*   `**syn**`旗帜之子
*   `**ack**`-【ack flag】。
*   `**fin**`–鳍旗
*   `**rst**`-rst 标志
*   `**psh**`-psh 标志
*   `**urg**`–URG 旗帜
*   `**ece**`-欧洲经委会标志
*   `**cwr**`–CWR 标志
*   `**ns**`-ns 标志

**UDP 扫描**

`**sx**`可以帮助调查开放的 UDP 端口。UDP 扫描利用 RFC1122 第 4.1.3.1 节:

> 如果数据报到达的目的地是 UDP 端口，而该端口没有挂起的监听调用，则 UDP 应该发送 ICMP 端口不可达消息。

与 TCP 扫描类似，`**sx**`返回有关 UDP 扫描的所有回复 ICMP 数据包的信息。该信息包含 IP 地址、ICMP 数据包类型和回复数据包中设置的代码。

例如，要检测主机上的 DNS 服务器，请运行:

**cat ARP . cache | sx UDP–JSON-p53 192 . 168 . 0 . 171**

样本输出:

**{"scan":"udp "，" IP ":" 192 . 168 . 0 . 171 ", " icmp ":{ " type ":3，" code":3}}**

在这种情况下，我们发现主机发送了带有**目的地不可达**类型和**端口不可达**代码的 ICMP 回复数据包(根据 rfc1122，这是关闭端口的典型响应)。

防火墙通常设置不同于**端口的 ICMP 代码，因此很容易被检测到。**

**速率限制**

有时，您需要限制生成的数据包的发送速度。这可以通过`--rate`选项来完成。

例如，要将速度限制为每 5 秒 1 个数据包:

**cat ARP . cache | sx TCP–速率 1/5s–JSON-p 22，80，443 192.168.0.171**

**排除子网**

有时您需要从扫描中排除一些 ip 地址和子网。这可以通过`**--exclude**`选项来完成。它指定要排除的带有 CIDR 表示法中的 IP 或子网的文件，每行一个。

例如，要排除 RFC 1918 地址，创建一个包含以下内容的文件`**ips.txt**`:

10 . 0 . 0 . 0/8
172 . 16 . 0 . 0/16
192 . 168 . 0 . 0/16

您也可以插入注释和空行:

# **排除 RFC 1918 地址
10.0.0.0/8 #注释 1
172.16.0.0/12 #注释 2
192.168.0.0/16 #注释 3
初始化过程中使用的 0.0.0.0/8 #地址(RFC 6890)
#排除 RFC 5735 地址
127.0.0.0/8 #环回地址
1998**

并使用`**--exclude ips.txt**`选项运行扫描。

**实时局域网 TCP SYN 扫描器**

作为扫描组合的一个例子，您可以结合 ARP 和 TCP SYN 扫描来创建定期扫描整个局域网的实时 TCP 端口扫描程序。

启动实时 ARP 扫描并将结果保存到`**arp.cache**`文件:

**sx ARP 192 . 168 . 0 . 1/24–live 10s–JSON | tee ARP . cache**

在另一个终端启动 TCP SYN 扫描:

**虽然真实；do sx TCP-P1-65535-a ARP . cache-f ARP . cache；睡眠 30；完成**

**SOCKS5 扫描**

`**sx**`可以检测 live SOCKS5 代理。要进行扫描，您必须指定一个 IP 范围或带有 IP/端口对的 JSONL 文件。

例如，IP 范围扫描:

**sx socks -p 1080 10.0.0.1/16**

用 JSON 输出扫描文件中的 IP/端口对:

**sx socks–JSON-f IP _ ports _ file . jsonl**

输入文件的每一行都是一个 json 字符串，它必须包含 **ip** 和**端口**字段。

样本输入文件:

**{ " IP ":" 10 . 0 . 1 . 1 "," port ":1080 }
{ " IP ":" 10 . 0 . 2 . 2 "," port ":1081 }**

您还可以指定要扫描的端口范围:

**sx socks-p 1080-4567-f IPS _ file . jsonl**

在这种情况下，将只从文件中提取 ip 地址，不再需要**端口**字段。

**弹性搜索扫描**

Elasticsearch scan 检索集群信息和所有索引以及别名的列表。

例如，IP 范围扫描:

**sx elastic-p 9200 10 . 0 . 0 . 1/16**

默认情况下，扫描使用 http 协议，要使用 https 协议，请指定`**--proto**`选项:

**sx elastic–proto https-p 9200 10 . 0 . 0 . 1/16**

用 JSON 输出扫描文件中的 IP/端口对:

**sx elastic–JSON-f IP _ ports _ file . jsonl**

输入文件的每一行都是一个 json 字符串，它必须包含 **ip** 和**端口**字段。

样本输入文件:

**{ " IP ":" 10 . 0 . 1 . 1 "," port ":9200 }
{ " IP ":" 10 . 0 . 2 . 2 "," port ":9201 }**

您还可以指定要扫描的端口范围:

**sx elastic-p 9200-9267-f IPS _ file . jsonl**

在这种情况下，将只从文件中提取 ip 地址，不再需要**端口**字段。

[**Download**](https://github.com/v-byte-cpu/sx)