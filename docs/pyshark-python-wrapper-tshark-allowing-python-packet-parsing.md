# pyshark:t shark 的 Python 包装器，允许使用 Wireshark 解析器解析 Python 包

> 原文：<https://kalilinuxtutorials.com/pyshark-python-wrapper-tshark-allowing-python-packet-parsing/>

[![Pyshark : Python Wrapper For TShark, Allowing Python Packet Parsing Using Wireshark Dissectors](img/0aa94099fa8521e6a194fce53978d26f.png "Pyshark : Python Wrapper For TShark, Allowing Python Packet Parsing Using Wireshark Dissectors")](https://1.bp.blogspot.com/-hy1YnCW1xWw/XV6Vx-Yg3nI/AAAAAAAACHM/vdjTkqu0ICIOjaisP2P2cFnrxMFkh1UfQCLcBGAs/s1600/wireshark.png)

tshark 的 Python 包装器，允许使用 wireshark 解析器解析 python 包。 **Python2 弃用**–这个包不再支持 Python2。如果您希望在 Python2 中仍然使用它，您可以:

*   使用版本 0.3.8
*   通过 pypi 安装 pyshark-legacy
*   克隆 pyshark-legacy[repo([https://github.com/KimiNewt/pyshark-legacy](https://github.com/KimiNewt/pyshark-legacy))]，在那里将应用错误修复。

**寻找贡献者**–由于各种原因，我现在很难找到时间来维护和增强这个包。任何拉动请求将被审查，如果任何一个人感兴趣，是合适的，我很乐意将他们纳入该项目。请随时给我发邮件，邮箱:dorgreen1。

有相当多的 python 包解析模块，这一个是不同的，因为它实际上不解析任何包，它只是使用 t shark(wireshark 命令行实用程序)的能力来导出 XML 以使用它的解析。

该软件包允许使用您安装的所有 wireshark 解析器解析捕获文件或实时捕获。在 windows/linux 上测试。

**也可阅读-[GoDoH:一个 DNS-Over-HTTPS C2](https://kalilinuxtutorials.com/godoh-dns-over-https/)**

**安装**

**所有平台**

只需运行以下命令来安装 pypi 的最新版本

**pip 安装 pyshark**

或者从 git 存储库安装:

git 克隆 https://github . com/kiminewt/pyshark . git
pyshark/src
python setup . py install CD

麦克·OS X

您可能必须安装 libxml，这可能是意外的。如果收到 clang 的错误或关于 libxml 的错误消息，请运行以下命令:

```
xcode-select --install
pip install libxml
```

您可能需要接受 XCode 的 EULA，所以请准备好点击 GUI 中的“接受”对话框。

**用途**

**从捕获文件中读取:**

导入 pyshark
cap = pyshark。file capture('/tmp/my capture . cap ')
cap

print cap[0]
包(长度:698)
层 ETH:
目的地:消隐
源:消隐
类型:IP (0x0800)
层 IP:
版本:4
头长度:20 字节
区分服务字段:0x00 (DSCP 0x00:默认；ECN: 0x00: Not-ECT(不支持 ECN 的传输))
总长度:684
标识:0x254f (9551)
标志:0x00
片段偏移量:0
生存时间:1
协议:UDP (17)
报头校验和:0xe148【正确】
来源:空白
目的地:空白
…

**其他选项**

*   **param keep_packets** :通过 next()读取数据包后是否保留。用于在阅读大写字母时节省内存。
*   **param input_file** :包含数据包捕获文件(PCAP PCAP)的路径或类似文件的对象..)或 TShark xml。
*   **param display_filter** :一个显示(wireshark)过滤器，在读取之前应用于 cap。
*   **param only_summaries** :仅生成数据包摘要，速度快得多，但包含的信息很少
*   **param disable_protocol** :禁用协议检测(tshark >版本 2)
*   **param decryption_key** :用于加密和解密捕获流量的密钥。
*   **param encryption_type** :捕获流量中使用的加密标准(必须是“WEP”、“WPA-PWD”或“WPA-PWK”)。默认为 WPA-PWK。
*   **param t shark _ Path**:t shark 二进制文件的路径

**从实时界面读取:**

捕获= pyshark。live capture(interface = ' eth 0 ')
capture . sniff(time out = 50)
capture

capture[3]

对于 capture . sniff _ continuously(packet _ count = 5)中的数据包:
打印'刚到:'，数据包

**其他选项**

*   **param interface** :要监听的接口的名称。如果未给定，则采用第一个可用的。
*   **param bpf_filter** :要在数据包上使用的 bpf 过滤器。
*   **param display_filter** :要使用的 Display (wireshark)过滤器。
*   **param only_summaries** :仅生成数据包摘要，速度快得多，但包含的信息很少
*   **param disable_protocol** :禁用协议检测(tshark >版本 2)
*   **param decryption_key** :用于加密和解密捕获流量的密钥。
*   **param encryption_type** :捕获流量中使用的加密标准(必须是“WEP”、“WPA-PWD”或“WPA-PWK”)。默认为 WPA-PWK)。
*   **param t shark _ Path**:t shark 二进制文件的路径
*   **param output_file** :另外将捕获的数据包保存到这个文件中。

**使用环形缓冲区从实时接口读取数据**

捕获= pyshark。livering capture(interface = ' eth 0 ')
capture . sniff(time out = 50)
capture

capture[3]

对于 capture . sniff _ continuously(packet _ count = 5)中的数据包:
打印'刚到:'，数据包

**其他选项**

*   **param ring_file_size** :环文件的大小，单位为 kB，默认为 1024
*   **param num_ring_files** :要保留的环文件数，默认为 1
*   **param ring_file_name** :环文件的名称，默认为/tmp/pyshark.pcap
*   **param interface** :要监听的接口的名称。如果未给定，则采用第一个可用的。
*   **param bpf_filter** :要在数据包上使用的 bpf 过滤器。
*   **param display_filter** :要使用的 Display (wireshark)过滤器。
*   **param only_summaries** :仅生成数据包摘要，速度快得多，但包含的信息很少
*   **param disable_protocol** :禁用协议检测(tshark >版本 2)
*   **param decryption_key** :用于加密和解密捕获流量的密钥。
*   **param encryption_type** :捕获流量中使用的加密标准(必须是“WEP”、“WPA-PWD”或“WPA-PWK”)。默认为 WPA-PWK)。
*   **param t shark _ Path**:t shark 二进制文件的路径
*   **param output_file** :另外将捕获的数据包保存到这个文件中。

**从实时远程界面读取:**

捕获= pyshark。RemoteCapture('192.168.1.101 '，' eth0')
capture.sniff(超时=50)
capture

**其他选项**

*   **param remote_host** :要捕获的远程主机(IP 或主机名)。应该在运行 rpcapd。
*   **param remote_interface** :远程机器上要捕获的远程接口。请注意，在 windows 上，它不是设备显示名称，而是真正的接口名称(即\设备\NPF_..).
*   **param remote _ port**:rpcapd 服务正在监听的远程端口
*   **param bpf_filter** :读取前应用于 cap 的 BPF (tcpdump)过滤器。
*   **param only_summaries** :仅生成数据包摘要，速度快得多，但包含的信息很少
*   **param disable_protocol** :禁用协议检测(tshark >版本 2)
*   **param decryption_key** :用于加密和解密捕获流量的密钥。
*   **param encryption_type** :捕获流量中使用的加密标准(必须是“WEP”、“WPA-PWD”或“WPA-PWK”)。默认为 WPA-PWK)。
*   **param t shark _ Path**:t shark 二进制文件的路径

**访问分组数据:**

可以通过多种方式访问数据。数据包被分成不同的层，首先你必须到达相应的层，然后你可以选择你的字段。

以下所有工作:

数据包['ip']。dst
192 . 168 . 0 . 1
packet . IP . src
192 . 168 . 0 . 100
packet[2]。src

要测试某个层是否在数据包中，您可以使用其名称:

数据包
中的“IP”为真

要查看所有可能的字段名，使用`packet.layer.field_names`属性(即`packet.ip.field_names`)或解释器上的自动完成功能。

你也可以得到一个字段的原始二进制数据，或者它的一个漂亮的描述:

p.ip.addr.showname
源或目的地址:10 . 0 . 0 . 10(10 . 0 . 0 . 10)
#以及一些新属性:
p . IP . addr . int _ value
167772170
p . IP . addr . binary _ value
' \ n \ x00 \ x00 \ n '

**解密数据包捕获**

Pyshark 支持使用 WEP、WPA-PWD 和 WPA-PSK 标准(WPA-PWD 是默认标准)自动解密踪迹。

cap1 = pyshark。FileCapture('/tmp/capture1.cap '，decryption _ key = ' password ')
cap 2 = pyshark。LiveCapture(interface='wi0 '，decryption_key='password '，encryption_type='wpa-psk ')

每个捕获类中都有一组受支持的加密标准，SUPPORTED_ENCRYPTION_STANDARDS。

pyshark。file capture . SUPPORTED _ ENCRYPTION _ STANDARDS
(' WEP '，' wpa-pwd '，' wpa-psk')
pyshark。live capture . SUPPORTED _ ENCRYPTION _ STANDARDS
(' WEP '，' wpa-pwd '，' wpa-psk ')

[**Download**](https://github.com/KimiNewt/pyshark)