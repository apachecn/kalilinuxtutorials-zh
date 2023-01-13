# NFStream:一个灵活的网络数据分析框架

> 原文：<https://kalilinuxtutorials.com/nfstream/>

[![NFStream : A Flexible Network Data Analysis Framework](img/4066b66efb4d34af7f4dada74af5fc77.png "NFStream : A Flexible Network Data Analysis Framework")](https://1.bp.blogspot.com/--PfpKvLltCs/Xjxz-X9m9DI/AAAAAAAAEwE/dRdBpYjIK-wYgpg4vBWsaYd4MTDMidFRACLcBGAsYHQ/s1600/nfstream%25281%2529.png)

**NFStream** 是一个 Python 包，它提供了快速、灵活、富于表现力的数据结构，旨在使处理**在线**或**离线**网络数据变得既简单又直观。

它旨在成为用 Python 进行实际的、**真实世界**网络数据分析的基础高级构建块。此外，它还有一个更广泛的目标，即成为研究人员的通用网络数据处理框架**，提供跨实验的数据再现性。**

 ****主要特点**

*   **性能:** **nfstream** 设计速度快(支持 pypy3 时快 10 倍)，占用 CPU 和内存少。
*   **第七层可见性:** **nfstream** 深度包检测引擎基于 [**nDPI**](https://github.com/ntop/nDPI) 。它允许 nfstream 执行 [**可靠的**](http://people.ac.upc.edu/pbarlet/papers/ground-truth.pam2014.pdf) 加密应用识别和元数据提取(例如 TLS、QUIC、TOR、HTTP、SSH、DNS)。
*   **灵活性:**添加一个 2 行的流特征作为 [**NFPlugin**](https://nfstream.readthedocs.io/en/latest/plugins.html) 。
*   **面向机器学习:**将你训练好的模型添加为 [**NFPlugin**](https://nfstream.readthedocs.io/en/latest/plugins.html) 。

**怎么用？**

*   处理一个大的 pcap 文件，只是想把它聚合成网络流？ **nfstream** 用几行代码让这条路变得更容易:

从 nfstream 导入 nf streamer
my _ awesome _ streamer = nf streamer(source = " Facebook . pcap ")#或网络接口(source = " eth 0 ")
for flow in my _ awesome _ streamer:
print(flow)#打印它，附加到 pandas Dataframe 或你想要的任何东西:)！

NFEntry(
id=0，
first_seen=1472393122365，
last_seen=1472393123665，
version=4，
src_port=52066，
dst_port=443，
protocol=6，
vlan_id=0，
src_ip='192.168.43.18 ''脸书'，
category _ name = ' social network '，
client_info='facebook.com '，
server _ info = ' * . Facebook . com '，
j3a _ client = ' bfcc 1a 3891601 EDB 4 f 137 ab 7 ab 25 b 840 '，
j3a _ server = ' 2 D1 EB 5817 ECE 335 c 24904 f 516 ad5 da 12 '
)

*   从 pcap 到熊猫 DataFrame？

导入熊猫为 PD
streamer_awesome = nf streamer(source = ' devil . pcap ')
data =[]
为 streamer _ awesome 中的 flow:
data . append(flow . to _ named tuple())
my _ df = PD。data frame(data = data)
my _ df . head(5)#享受！

*   没有找到具体的流量特征？用几行代码向 **nfstream** 添加插件:

从 nfstream 导入 nf plugin

class my _ awesome _ plugin(nf plugin):
def on _ update(self，obs，entry):
if OBS . length>= 666:
entry . my _ awesome _ plugin+= 1

streamer _ awesome = nf streamer(source = ' devil . pcap '，plugins =[my _ awesome _ plugin()])
for flow in streamer _ awesome:
print(flow . my _ awesome _ plugin)#查看您动态创建的

**也可阅读-[Blinder:一个 Python 库，用于自动化基于时间的盲目 SQL 注入](https://kalilinuxtutorials.com/blinder/)**

**先决条件**

**apt-get 安装 libpcap-dev**

**安装**

**使用画中画**

最新发布版本的二进制安装程序可用:

pip3 安装 nfstream

**从源代码构建**

如果您想在本地机器上构建 **nfstream** :

**git 克隆 https://github . com/aouinized/nfstream . git
nfstream CD
python 3 setup . py install**

[**Download**](https://github.com/aouinizied/nfstream)**