# Neurax:一个构建自蔓延二进制文件的框架

> 原文：<https://kalilinuxtutorials.com/neurax/>

[![Neurax : A Framework For Constructing Self-Spreading Binaries](img/dc821ad12a0d908c8fb5025bc8de8bba.png "Neurax : A Framework For Constructing Self-Spreading Binaries")](https://1.bp.blogspot.com/-jS21YOOroro/YMoTMMtli3I/AAAAAAAAJhc/ayV6wlKLx3g-Pufdt62QcMAldp6cPbiLwCLcBGAsYHQ/s728/neurax%2B%25281%2529.png)

Neurax 是一个帮助创建自传播软件的框架。

**要求**

`**go get -u github.com/redcode-labs/Coldfire**`

`**go get -u github.com/yelinaung/go-haikunator**`

**2.0 版新增**

*   新单词表变体+国家通用密码
*   临时被动扫描
*   `**.FastScan**`使主动扫描更快的选项
*   单词表是严格在内存中创建的
*   `**NeuraxScan()**`接受回调函数而不是通道作为参数。
*   `**NeuraxScan()**`无限循环扫描，可以设置整个子网/目标池的每次扫描间隔
*   对非 IP 格式的目标进行反向 DNS 查找
*   从 ARP 缓存中提取候选目标
*   可能只扫描选定的目标列表+优先特定目标(如默认网关)
*   使用被动网络扫描时，可以指定接口和超时。
*   改进的 command stager(可以选择使用提升的权限/多次执行)
*   选项名称的少量更改
*   `**NeuraxConfig.**`变成了`**N.**`(因为打字更短)
*   随机内存分配+二进制迁移的函数
*   连锁多个 stagers 的可能性(例如 **`wget`** + **`curl`** )
*   创建的单词表的数量和复杂性可以很容易地调整(选项有 **`.WordlistExpand` )**
*   可以设置创建的二进制文件的生存时间

**用途**

借助 Neurax，Golang 二进制文件可以在本地网络上传播，而无需使用任何外部服务器。

多样化的配置选项和命令阶段允许在各种无线环境中快速传播。

**示例代码**

**包主
导入。" github . com/red code-labs/Neurax "
func main(){
//指定要使用的服务端口和 Stager
N . Port = 5555
N . Stager = " wget "
//启动一个在后台公开当前二进制文件的服务器
go Neurax server()
//将当前二进制文件复制到所有逻辑驱动器
Neurax disks()
//创建一个应该在目标机器上启动的命令 Stager
//它将下载你可以使用 SSH bruteforce，一些 rce 或者任何你想要的东西；> */
}**

**配置条目列表**

| 名字 | 描述 | 缺省值 |
| --- | --- | --- |
| 名词（noun 的缩写）老练的人 | 要使用的命令登台程序的名称 | `**random, platform-compatible**` |
| 名词（noun 的缩写）StagerSudo | 如果为真，则使用提升的权限执行 Linux cmd 登台程序 | `**false**` |
| n .学员度量 | 重新执行命令 stager 的次数 | `**0**` |
| 名词（noun 的缩写）港口 | 服务端口 | `**6741**` |
| 名词（noun 的缩写）平台 | 目标平台 | `**detected automatically**` |
| 名词（noun 的缩写）小路 | 主机上保存二进制文件的路径 | `**random**` |
| 名词（noun 的缩写）文件名 | 下载的二进制文件应该使用并保存的名称 | `**random**` |
| 名词（noun 的缩写）Base64 | 用 base64 编码传输的二进制文件 | `**false**` |
| N.通信端口 | 二进制文件用来相互通信的端口 | `**7777**` |
| 名词（noun 的缩写）CommProto | 节点间的通信协议 | `**"udp"**` |
| 名词（noun 的缩写）反向拉伸器 | 包含 **`"<host>:<port>"`** 的远程反向外壳处理程序 | `**not specified**` |
| 名词（noun 的缩写）反转正片 | 用于反向连接的协议 | `**"udp"**` |
| 名词（noun 的缩写）ScanRequiredPort | NeuraxScan()仅在打开特定端口时将主机视为活动主机 | `**none**` |
| 名词（noun 的缩写）被动扫描 | NeuraxScan()使用被动 ARP 流量监控来检测主机 | `**false**` |
| 名词（noun 的缩写）ScanPassiveTimeout | NeuraxScan()监视 ARP 层的秒数 | `**50 seconds**` |
| N.扫描被动分析 | 被动扫描时使用的界面 | `**default**` |
| N.ScanActiveTimeout | NeuraxScan()将该值设置为每个线程中被扫描端口的超时值 | `**2 seconds**` |
| n .扫描被动 | NeuraxScan()捕获所有找到的设备上的数据包 | `**false**` |
| 名词（noun 的缩写）ScanPassiveNoArp | 被动扫描没有设置严格的 ARP 捕获过滤器 | `**false**` |
| 名词（noun 的缩写）扫描优先 | 包含要首先扫描的 IP 地址的片 | `**[]string{}**` |
| N.ScanFirstOnly(仅扫描) | NeuraxScan()仅扫描在`**.ScanFirst**`内指定的主机 | `**false**` |
| 名词（noun 的缩写）ScanArpCache | NeuraxScan()首先扫描在本地 ARP 缓存中找到的主机。仅适用于主动扫描 | `**false**` |
| 名词（noun 的缩写）ScanCidr | NeuraxScan()扫描这个 CIDR | `**local IP + "\24"**` |
| 名词（noun 的缩写）扫描线程 | 用于 NeuraxScan 的线程数() | `**10**` |
| 名词（noun 的缩写）扫描范围 | NeuraxScan()扫描目标主机的所有端口，以确定它是否处于活动状态 | `**from 19 to 300**` |
| 名词（noun 的缩写）扫描间隔 | 再次扫描整个子网之前的休眠时间间隔 | `**"2m"**` |
| 名词（noun 的缩写）ScanHostInterval | 在主动模式下扫描下一台主机之前的睡眠时间间隔 | `**"none"**` |
| 名词（noun 的缩写）ScanGatewayFirst | 使用主动扫描时，网关是扫描的第一台主机 | `**false**` |
| 名词（noun 的缩写）冗长的 | 如果为 true，所有错误消息都将打印到 STDOUT | `**false**` |
| 名词（noun 的缩写）去除 | 当出现任何错误时，二进制文件会从主机中删除自己 | `**false**` |
| 名词（noun 的缩写）PreventReexec | 如果为真，则当任何命令与之前已经接收到的命令相匹配时，不会执行该命令 | `**true**` |
| 名词（noun 的缩写）ExfilAddr | 当`**'v'**`前同步码存在时，命令输出发送到的地址。 | `**none**` |
| n . word list | NeuraxWordlist()对输入单词执行非标准转换 | **假** |
| N.WordlistCommon | 将 20 个最常用的密码添加到单词列表中 | `**false**` |
| N.WordlistCommonNum | 要使用的常用密码的数量 | `**all**` |
| N.WordlistCommonCountries | map[string]int，包含要使用的国家代码和密码数 | **map[string]int** |
| n . word 列表指针 | 指定 **`.WordlistExpand`** 时使用的赋值器 | `**{"single_upper", "cyryllic", "encapsule"}**` |
| 名词（noun 的缩写）WordlistPermuteNum | 由 NeuraxWordlistPermute()生成的置换的最大长度 | `**2**` |
| 名词（noun 的缩写）WordlistPermuteSeparator | 用于排列的分隔符 | `**"-"**` |
| 名词（noun 的缩写）单词列表无序播放 | 在返回之前打乱生成的单词表 | `**false**` |
| N.阿罗纳姆 | 此项定义了`**NeuraxAlloc()**`分配随机存储器的次数 | `**5**` |
| 名词（noun 的缩写）黑名单 | 包含从任何类型的扫描中排除的 IP 地址的切片 | `**[]string{}**` |
| 名词（noun 的缩写）快速 HTTP | IsHostInfected()中的 HTTP 请求是使用 fasthttp 库执行的 | `**false**` |
| 名词（noun 的缩写）调试 | 启用调试消息 | `**false**` |

**寻找新的目标**

功能`**NeuraxScan(func(string))**`能够检测本地网络上的活动主机。它唯一的参数是一个回调函数，在后台为每个活动的主机调用。当主机至少有 1 个开放端口、未被感染+满足 **`N.`** 中指定的条件时，该主机被视为活动主机

`**NeuraxScan()**`作为无限循环运行——它扫描由 **`.Cidr`** 配置条目指定的整个子网，当每台主机都被扫描时，函数会在 **`.ScanInterval`中给定的时间间隔内休眠。**

**磁盘感染**

Neurax 二进制文件不必使用无线方式复制自身。函数`**NeuraxDisks()**`将当前二进制文件(在非可疑名称下)复制到找到的所有逻辑驱动器。复制的二进制文件不会被执行，而只是驻留在它的目的地等待运行。 **`NeuraxDisks()`** 如果无法获得磁盘列表或无法复制到任何目标，则返回`**error**`。

另一个功能，`**NeuraxZIP(num_files int) err**`允许创建一个随机命名的。包含当前二进制文件的 zip 存档。它保存在当前目录中，包含多达`**num_files**`个随机文件。

**`NeuraxZIPSelf()`** 简单地压缩当前的二进制文件，创建一个同名的归档文件。

**同步命令执行**

函数`**NeuraxOpenComm()**`(作为 goroutine 启动)允许二进制接收和执行命令。它使用 **`.CommProto`中定义的协议监听`.CommPort`中指定的端口号。**字段`**.CommProto**`可以设置为`**"tcp"**`或`**"udp"**`。发送到用于通信的端口的命令以盲方式执行，它们的输出不会保存在任何地方。

可以在命令字符串之前添加可选的前导码。

格式:`**:<preamble_letters> <command>**`

带有前导的示例命令可能如下所示:`**:ar echo "pwned"**`

可以在前导码中指定以下字符:

*   `**a**`–接收到的命令被转发到每个被感染的节点，但首先接收到该命令的节点不会执行该命令
*   `**x**`–即使指定了`**a**`，也会执行收到的命令
*   **`r`**–收到命令后，二进制程序会从受感染的主机中移除自身并退出执行
*   `**k**`–向其他节点发送命令时保持前导码
*   `**s**`–在执行命令之前，休眠 1 到 5 秒之间的随机秒数
*   `**q**`–执行命令后，机器重启
*   `**o**`–命令被发送到单个随机节点。 **`a`** 必须指定
*   `**v**`–被执行命令的输出被发送到`**.ExfilAddr**`下指定的地址
*   **`m`**–防止命令重新执行的机制仅对该特定命令无效
*   `**l**`–命令在无限循环中执行
*   `**e**`–仅当节点具有提升的权限时，才执行命令
*   `**p**`–命令持续有效，并在每次启动时执行
*   `**d**`–执行命令的输出被打印到标准输出，用于调试目的
*   `**f**`–命令执行后发射叉弹
*   **`!`**–如果命令执行出错且指定了`**a**`，则该命令不会被转发

默认情况下，不带任何前导码发送的原始命令由该命令所针对的单个节点执行。

还需要注意的是，当 **`k`** 不存在于前导码中时，在第一个节点接收到前导码后，该前导码会立即从命令中移除。

**示例 1–前导没有被转发到其他节点:**

**(1)【TCP _ client】":ar whoami "-->[infected host 1]
(2)[infected host 1]" whoami "-->[infected hostn]
[infected host 1]在命令发送到(2)
中所有受感染的节点后删除自己，因为“r”在前导中指定。没有指定“x”，所以“whoami”没有被[InfectedHost1]** 执行

**示例 2–转发前导码**

**(1)【TCP _ client】":akxr whoami "-->[infected host 1]
(2)【infected host 1】":akxr whoami "-->【infected hostn】
(n)【infected hostn】":axkr whoami "-->…………………
………………………………->…………………
[infected hostn]两者都执行命令并试图**

**反向连接**

可以用`**NeuraxReverse()**`建立一个交互式的反壳。它将以`**"<host>:<port>"**`的形式从 **`.ReverseListener`** 中指定的主机名接收命令。使用的协议在`**.ReverseProto**`下定义。如果`**NeuraxOpenComm()**`在调用该功能前启动，每个命令将如上一节所述。否则，命令将在本地执行。

**注意:**该函数也应作为 goroutine 运行，以防止接收使用的无限循环造成阻塞。

**清理**

每当一个节点接收到`**"purge"**`命令时，它就向所有其他节点重新发送该命令，从主机中移除自己并退出。这种行为也可以在源代码的某个地方使用 **`NeuraxPurge()`** 开始执行。

**单词表创建**

如果你选择的传播媒介是基于某种暴力，最好准备一个合适的词汇表。在客户端将单词存储在文本文件中并不是很有效，所以你可以使用 **`NeuraxWordlist(...words) []string`改变一个基本的单词列表。**要排列一组给定的单词，使用`**NeuraxWordlistPermute(..words) []string**`。

**设置生存时间**

如果你想让你的二进制文件在给定时间后自动删除，在你的代码开始处使用 **`NeuraxSetTTL()`** 。这个函数应该作为一个 goroutine 启动。例如:

`**go NeuraxSetTTL("2m")**`

从初始执行 2 分钟后将使二进制运行 **`NeuraxPurgeSelf()`** 。

**同时使用多个载物台**

如果您想要链接给定平台的所有可用登台程序，请将`**.Stager**`设置为 **`"chain"`。**

**移动丢弃的二进制文件**

如果需要在初始执行后复制二进制，使用 **`NeuraxMigrate(path string)`** 。它将复制`**path**`下的二进制文件，删除当前的二进制文件并执行新迁移的二进制文件。

[**Download**](https://github.com/redcode-labs/Neurax#finding-new-targets)