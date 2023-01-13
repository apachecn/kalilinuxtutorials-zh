# Scallion:基于 GPU 的洋葱哈希生成器

> 原文：<https://kalilinuxtutorials.com/scallion/>

[![Scallion : GPU-Based Onion Hash Generator](img/13eef82c8d4376784260d147ae3116c5.png "Scallion : GPU-Based Onion Hash Generator")](https://1.bp.blogspot.com/-XgLL3mTIDoU/Xii1jC-KBZI/AAAAAAAAEhs/XVSPCkdc7RYoOD7e0xuSIamftMg8jATGACLcBGAsYHQ/s1600/Tor.png)

葱油让你创造虚荣 GPG 键和。使用 OpenCL 的洋葱地址(针对 [Tor 的](https://www.torproject.org/) [隐藏服务](https://www.torproject.org/docs/hidden-services))。它运行在 Mono(在 Arch Linux 上测试)和。NET 3.5+(在 Windows 7 和 Server 2008 上测试)。

它目前处于测试阶段，正在积极开发中。尽管如此，我们认为它已经可以使用了。预期的改进主要是在性能、用户界面和易于安装方面，而不是用于生成密钥的整体算法。

**常见问题解答**

以下是一些常见问题及其答案:

1.  为什么要生成 GPG 键？Scallion 用于在信任网的强集中查找每个 32 位密钥 id 的冲突，证明 32 位密钥 id 是多么不安全。在 DEFCON ( [视频](https://www.youtube.com/watch?v=Ow-YcP_KsIw))上有/有[个演讲，更多信息可以在 https://evil32.com/](https://www.defcon.org/html/defcon-22/dc-22-speakers.html#Klafter)[的](https://evil32.com/)上找到。
2.  什么是有效字符？Tor。洋葱地址使用 [Base32](http://www.ietf.org/rfc/rfc4648.txt) ，由所有字母和数字 2 到 7 组成。它们不区分大小写。GPG 指纹使用[十六进制](http://en.wikipedia.org/wiki/Hexadecimal)，由数字 0-9 和字母 A-F 组成
3.  你能使用比特币专用集成电路(如 KnC 的墨西哥胡椒)来加速这个过程吗？遗憾的是，没有。虽然 Scallion 使用的过程在概念上是相似的(增加一个 nonce 并检查哈希)，但细节是不同的(比特币的 SHA-1 vs 双 SHA-256)。此外，比特币专用集成电路之所以速度如此之快，是因为它们是为比特币挖矿应用量身定制的。例如，这是 CoinCraft A-1 公司的[数据表](https://bitmine.ch/wp-content/uploads/2013/11/CoinCraft-A1.pdf)，这是一款从未问世的 ASIC，但可能代表了一般的方法。微控制器以比特币块的最后 128 位、之前位的哈希中间状态、目标难度和最大随机数的形式发送工作。ASIC 选择插入随机数的位置，并选择哪些块符合散列。Scallion 必须在不同的位置插入 nonce，它检查模式匹配，而不仅仅是“低于 XXXX”。
4.  如何使用多种设备？运行多个 Scallion 实例。😄青葱搜索是概率性的，所以你不会用第二个设备重复工作。真正的多设备支持不会太难，但也不会增加太多。我已经在 [tmux](http://tmux.sourceforge.net/) 或 [screen](https://www.gnu.org/software/screen/) 中运行了几个青葱实例，并取得了巨大的成功。当发现一个模式时，您只需要手动中止所有的作业(或者编写一个 shell 脚本来监视输出文件，并在看到结果时杀死所有的作业)。

**也读作-[lol BITS:C #反向 Shell 使用 BITS 作为通信协议](https://kalilinuxtutorials.com/lolbits-reverse-shell-using-bits-communication-protocol/)**

**依赖关系**

*   安装和配置 OpenCL 和相关驱动程序。请参考您的发行版文档。
*   OpenSSL。对于 Windows，包括了预构建的 x86 DLLs
*   仅在 windows 上， [VC++可再发行版 2008](https://www.microsoft.com/en-us/download/details.aspx?id=5582)

**构建 Linux**

先决条件

*   为您的 linux 发行版获取最新的 mono:[http://www.mono-project.com/download/](http://www.mono-project.com/download/)
*   安装常用依赖项:`**sudo apt-get update sudo apt-get install libssl-dev mono-devel**`
*   AMD/开源版本`**sudo apt-get install ocl-icd-opencl-dev**`
*   Nvidia 打造 **`sudo apt-get install nvidia-opencl-dev nvidia-opencl-icd`**
*   最后 **`msbuild scallion.sln`**

**Docker Linux(仅限 NVIDIA GPU)**

*   拥有 nvidia-docker 容器运行时
*   构建容器:`**docker build -t scallion -f Dockerfile.nvidia .**`
*   运行:`**docker run --runtime=nvidia -ti --rm scallion -l**` [预期输出截图](https://user-images.githubusercontent.com/9354925/53215957-37ed6100-3653-11e9-97d0-97a6c06eabe4.png)

**构建窗口**

*   在 VS Express for Desktop 2012 中打开“scallion.sln”
*   构建解决方案时，我在调试模式下做了所有的事情。

**多模式哈希**

Scallion 支持通过原始的正则表达式语法找到多个模式中的一个或多个。仅字符类(例如`**[abcd]**`)都支持。`.`字符代表任何字符。洋葱地址总是 16 个字符长，GPG 指纹总是 40 个字符。你可以在比赛的末尾加上`$`来找到一个后缀(例如。`**DEAD$**`)。最后，管道语法(例如`**pattern1|pattern2**`)可以用来寻找多个图案。搜索多字节模式(在合理范围内)不会导致速度明显下降。许多正则表达式会在 GPU 上产生一个单一的模式，并且不会导致速度降低。

一些使用案例及示例:

*   生成一个前缀，后跟一个数字以提高可读性: `**mono scallion.exe prefix[234567]**`
*   一次搜索几个模式(n.b. -c 导致葱白即使一次命中也继续生成)**`mono scallion.exe -c prefix scallion hashes mono scallion.exe -c "prefix|scallion|hashes"`**
*   搜索后缀“bad beef”**`mono scallion.exe .........badbeef mono scallion.exe --gpg badbeef$ # Generate GPG key`**
*   复杂的自我解释示例: `**mono scallion.exe "suffixa$|suffixb$|prefixa|prefixb|a.suffix$|a.test.$"**`

它是如何工作的？

在高层次上，青葱的工作原理如下:

*   在 CPU 上使用 OpenSSL 生成 RSA 密钥
*   将密钥发送到 GPU
*   增加密钥的公共指数
*   散列密钥
*   如果散列密钥不是部分冲突，请转到步骤 3
*   如果密钥没有通过 PKCS #1 v2.1 推荐的健全性检查(在 CPU 上检查)，请转到步骤 3
*   部分碰撞的全新钥匙！

基本算法如上所述。速度/性能是 GPU 和 CPU 上大规模并行化的结果。

**速度/性能**

重要的是要认识到葱白执行的是概率搜索。实际时间可能与预测时间相差很大

最初的 RSA 密钥生成是由 CPU 完成的。ivybridge i7 使用单核每秒可以生成 51 个密钥。每个密钥可以提供 1 千兆哈希值的指数来挖掘，一个像样的 CPU 可以跟上几个 GPU，因为它目前正在实施。

SHA1 哈希是在 GPU 上完成的。我们测试过的几款 GPU 的哈希表如下(按制造商分组，按功耗排序):

| 国家政治保卫局。参见 OGPU | 速度 |
| --- | --- |
| Intel i7-2620M | 9.9 兆赫兹/秒 |
| Intel i5-5200U | 118 英里/秒 |
| NVIDIA GT 520 系列 | 38.7 毫瓦/秒 |
| NVIDIA Quadro K2000M | 90 毫瓦/秒 |
| NVIDIA GTS 250 | 128 英里/秒 |
| NVIDIA GTS 450 | 144 毫瓦/秒 |
| 英伟达 GTX 670 | 480 英里/秒 |
| 英伟达 GTX 970 | 2350 毫瓦/秒 |
| 英伟达 GTX 980 | 3260 英里/秒 |
| 英伟达 GTX 1050 (M) | 1400 毫瓦/秒 |
| 英伟达 GTX 1070 | 4140 毫瓦/秒 |
| 英伟达 GTX 1070 TI | 5100 毫瓦/秒 |
| 英伟达 GTX 泰坦 X | 4412 兆赫兹/秒 |
| 英伟达 GTX 1080 | 5760 英里/秒 |
| 英伟达特斯拉 V100 | 11646 英里/秒 |
| AMD A8-7600 辅助动力装置 | 120 毫瓦/秒 |
| AMD Radeon HD5770 | 520 英里/秒 |
| AMD Radeon HD6850 | 600 毫瓦/秒 |
| AMD 镭龙 RX 460 | 840 英里/秒 |
| AMD 镭龙 RX 470 | 957 英里/秒 |
| AMD 镭龙 R9 380X | 2058 英里/秒 |
| AMD FirePro W9100 | 2566 兆赫兹/秒 |
| AMD 镭龙 RX 480 | 2700 毫瓦/秒 |
| AMD 镭龙 RX 580 | 3180 英里/秒 |
| AMD 镭龙 R9 纳米 | 3325 英里/秒 |
| AMD 织女星前沿版 | 7119 英里/秒 |

MH/s =每秒百万散列

值得注意的是，英特尔已经为其处理器发布了 OpenCL 驱动程序，在 CPU 上可以发现短暂的冲突。

要计算给定部分碰撞所需的秒数(平均)，请使用以下公式:

| 类型 | 预计时间 |
| --- | --- |
| GPG 密钥 | 2^(4*length-1) /哈希 speed |
| 。洋葱地址 | 2^(5*length-1) /哈希 speed |

例如，在我的 nVidia Quadro K2000M 上，我看到大约 90 MH/s。以这样的速度，我可以生成一个 8 字符。洋葱前缀约在 1h 41m，**，`2^(5*8-1)/90 million = 101 minutes`。**

**工作组规模**

Scallion 将默认使用您的设备报告的首选工作组大小。这是一个合理的默认值，但是尝试工作组可能会提高性能。

**安全**

葱白生成的密钥和小葱生成的密钥很像。它们具有异常大的公共指数，但是它们通过 openssl 的 RSA_check_key 函数通过了 PKCS #1 v2.1 推荐的全套健全性检查。Scallion 支持多种 RSA 密钥大小，针对 1024b、2048b 和 4096b 优化了内核。其他密钥大小可能有效，但尚未经过测试。

[**Download**](https://github.com/lachesis/scallion)