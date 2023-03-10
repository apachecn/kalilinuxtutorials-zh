# 数据包嗅探器:一个纯 Python 的网络数据包嗅探工具

> 原文：<https://kalilinuxtutorials.com/packet-sniffer/>

[![](img/0468eec473831609ea2174df775f215e.png)](https://blogger.googleusercontent.com/img/a/AVvXsEjDToItCzX7v1glRvanas8aDq4D_Pxh7Yu6M5eTdS3ZT3HPDeM85oSzjFwzBfq6Nz5dqpk_i-W6vgqgBM9DLJ2snaVNQ3hQ5W7UK8jUzEM6MDvUTnj0eyypHbVei9KHs9UkqTISy3we0-vpOgCdjt0MN0Ibmx0cR828-3mz7KZc3xZM1FXjyrBWo_DX=s728)

包嗅探器是一个简单的纯 Python 网络包嗅探器。数据包到达给定的网络接口控制器时被分解，其信息显示在屏幕上。

这个应用程序不依赖于第三方模块，可以由任何 Python 3.x 解释器运行。

**安装**

**GNU / Linux**

简单地用`**git clone**`克隆这个存储库，并执行`**packet_sniffer.py**`文件，如下面的用法部分所述。

**用户@主机:~/DIR$ git 克隆 https://github.com/EONRaider/Packet-Sniffer.git**

**其他系统**

这个项目依赖于`**PF_PACKET**`——一个在 Windows 或 Mac OS X 上找不到的状态包过滤器。出于演示的目的，您可以在 Docker 容器中试用这个包。尽管它不能完全访问您机器上的本地主机，但您仍然可以嗅探 Docker 子网，至少可以让模块运行。

使用此命令从项目目录构建并运行:

docker build -t sniff。&docker 运行–网络主机嗅探

注意，entry 命令只是简单的`**python packet_sniffer.py**`，所以可以通过覆盖默认命令来随意使用模块的全部功能。请记住，我们之前用名称“sniff”标记了容器，因此我们可以通过以下方式将命令行参数传递给嗅探器:

**docker run–网络主机 sniff【你的命令在这里】
echo“现在让我们打印帮助”
docker run–网络主机 sniff python packet _ sniffer . py–help**

OS X 或 Windows 不支持使用`**--network host**`,因此该容器不会完全发挥作用——但您会看到数据包在 docker 子网内传输。

**用途**

**packet_sniffer.py [-h] [-i 接口] [-d]
一个纯 Python 的网络包嗅探器。
可选参数:
-h，–help 显示此帮助信息并退出
-i 接口，–INTERFACE INTERFACE
将从中捕获数据包的接口(默认从所有可用接口捕获
)。
-d，–显示捕获过程中输出数据包数据。**

**运行应用程序**

| 目标 | 开始在所有可用接口上捕获数据包 |
| 执行 | **sudo python 3 packet _ sniffer . py** |
| 结果 | 请参考下面的输出示例 |

样本输出:

**[>]476 号包在 17:45:13:
[+]MAC……AE:45:39:30:8f:5a->DC:d9:AE:71:c8:B9
[+]IP v4…………192 . 168 . 1 . 65->140.82.113.3 | PROTO:TCP TTL:64
[+]TCP…………40820-【中..443->40820 | Flags:0x 010>ACK
[>]478 号包 17:45:18:
[+]MAC……DC:d9:AE:71:c8:B9->AE:45:39:30:8f:5a
[+]ARP 谁有 192.168.1.65？- >告诉 192 . 168 . 1 . 254
[>]479 号包 17:45:18:
[+]MAC……AE:45:39:30:8f:5a->DC:d9:AE:71:c8:B9
[+]ARP……..192.168.1.65 - >位于 AE:45 . 39 . 30 . 8f:5a**

[**Download**](https://github.com/EONRaider/Packet-Sniffer)