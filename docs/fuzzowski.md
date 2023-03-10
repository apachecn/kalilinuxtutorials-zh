# Fuzzowski:网络协议 Fuzzer

> 原文：<https://kalilinuxtutorials.com/fuzzowski/>

[![Fuzzowski : The Network Protocol Fuzzer](img/4ad1daf8aa8a08da39f5eb6f6d6cef64.png "Fuzzowski : The Network Protocol Fuzzer")](https://asciinema.org/a/0RMDMrJWiFo4RoRwAjx61BXDY)

我们的想法是成为我们希望**使用的网络协议模糊器。**

 **该工具的目的是在模糊网络协议的整个过程中提供帮助，允许定义通信，帮助识别服务崩溃的“嫌疑人”，等等

**最后变更**
【2019 年 16 月 12 日】

*   **数据生成模块**完全重新编码(原语、块、请求)
    *   改进的字符串模糊库，允许自定义列表，文件和回调命令
    *   **变量**数据类型，它接受一个由会话、用户或响应设置的变量
*   **会话**完全重新编码。现在它基于**测试用例** s，其中包含了执行请求、检查响应、存储数据(如收到的错误等)所需的所有信息。
*   添加了**个响应**。现在，您可以用 s_response()定义响应，这允许检查来自服务器的响应，设置变量，甚至对响应执行额外的测试，以检查是否有问题
*   如果测试失败，监视器现在会自动将测试用例标记为可疑
*   增加了 **IPP(互联网打印协议)**模糊器，我们在我们的打印机研究项目([https://www.youtube.com/watch?v=3X-ZnlyGuWc&t = 7s](https://www.youtube.com/watch?v=3X-ZnlyGuWc&t=7s))中曾经发现不同打印机品牌的几个漏洞

**也可阅读-[CTF Tool:交互式 CTF 探索工具](https://kalilinuxtutorials.com/ctftool/)**

**特色**

*   基于 Sulley Fuzzer 进行数据生成[[https://github.com/OpenRCE/sulley](https://github.com/OpenRCE/sulley)
*   实际上，分叉的布弗兹(这是苏利的一个分支)[[https://github.com/jtpereyda/boofuzz](https://github.com/jtpereyda/boofuzz)
*   Python3
*   非随机(有限数量的可能性)
*   要求“创建包”的类型(穗 fuzzer 风格)
*   也允许从参数创建“原始”包，带有注入点(对于模糊简单的协议非常有用)
*   有一个很好的控制台暂停，审查和重新测试任何可疑的(提示工具包 ftw)
*   允许自动或通过控制台跳过导致错误的参数
*   可疑数据包的良好打印格式(以准确了解被模糊的内容)
*   当您将测试用例标记为崩溃时，它会将 POC 保存为 python 脚本
*   监控模块收集目标的信息，检测奇怪的行为和标记嫌疑人
*   重新启动模块，如果连接丢失，将重新启动目标(例如，关闭电源，然后打开智能插头)

**协议实施**

*   **LPD(行式打印守护程序)**:完全实现
*   **IPP(互联网打印协议)**:部分实施
*   **BACnet(楼宇自动化和控制网络协议)**:部分实施
*   **Modbus (ICS 通信协议)**:部分实现

**安装**

**virtualenv venv-p python 3
source venv/bin/activate
pip install-r requirements . txt**

**帮助**

用法:python -m fuzzowski [-h] [-p {tcp，udp，SSL }][-b BIND][-ST SEND _ TIME out]
[-rt RECV _ TIME out][–SLEEP-TIME SLEEP _ TIME][-NC][-TN][-NR][-NRF][-Cr]
[–THRESHOLD-REQUEST CRASH _ THRESHOLD _ REQUEST]
[–THRESHOLD-ELEMENT CRASH _ THRESHOLD _ ELEMENT]
[–ignore-aborted][–ignore-reset][–ignore]
主机端口
位置参数:
主机目的地主机
端口目的地端口
可选参数:
-h，–help 显示此帮助消息并退出
连接选项:
-p {tcp，udp，ssl}，–Protocol { TCP，udp，ssl}
Protocol(默认 tcp)
-b BIND，–BIND 绑定到端口
-st SEND_TIMEOUT，–SEND _ time out SEND _ time out –RECV _ TIME out RECV _ TIME out
设置 recv() timeout(默认 5s)
–SLEEP-TIME SLEEP _ TIME
每次测试之间的睡眠时间(默认 0)
-nc，–new-conns 在同一个测试的每个包之后打开一个新的连接
-tn，–Transmit-next-node
发送 fuzzed 节点图中的下一个节点
RECV()选项:
-nr，–no-RECV 不接收() –Check-recv 检查 recv()
崩溃选项中是否已接收到数据:
–THRESHOLD-REQUEST CRASH _ THRESHOLD _ REQUEST
在跳过请求之前设置请求中允许的崩溃次数(默认为 9999)
–THRESHOLD-ELEMENT CRASH _ THRESHOLD _ ELEMENT
在跳过请求之前设置原语中允许的崩溃次数(默认为 3)
–Ignore-aborted 忽略经济错误
–Ignore-reset 忽略经济重置错误
–错误 –回调回调
使用回调生成器将回调地址设置为 fuzz，而不是普通突变
–文件文件名使用文件内容进行模糊突变
模糊器:
-f {cops，dhcp，ipp，lpd，netconf，teltp，raw}，–FUZZ { cops，dhcp，ipp，lpd，netconf，telnet_cli，tftp，raw}
可用协议
-r FUZZ _ REQUESTS[FUZZ _ REQUESTS…]，–请求模糊 remove _ job]
telnet _ CLI:[commands]
TFTP:[read]
raw:[' \ x01 string \ n ' ' \ x02 request 2 \ x00 '…]
重新启动选项:
–Restart module _ name[args…]
重新启动模块:
run: ' [ …]'(将命令和参数用引号括起来，作为唯一的一个参数传递)
smartplug:它将关闭和打开 Smart Plug【T62 -m {IPPMon} [{IPPMon} …]
监视器模块:
IPPMon:向目标发送 get-attributes IPP 消息
其他选项:
–PATH PATH 模糊基于 HTTP 的协议时设置路径(默认/)
–DOCUMENT _ url DOCUMENT _ URL
设置 print_uri 的文档 URL

**例题**

使用默认选项模糊 get_printer_attribs IPP 操作:

**python-m fuzzowski printer 1 631-f IPP-r get _ printer _ attribs–重启 smartplug**

[![](img/d77bec6a4812b482630e66aa4b63ab39.png)](https://asciinema.org/a/0RMDMrJWiFo4RoRwAjx61BXDY)

使用 IPP 的原始功能来模糊手指协议:

**python-m fuzzowski printer 79-f raw-r ' { { root } } \ n '**

[![](img/61e72c4410507a3d133e2d78572e5660.png)](https://asciinema.org/a/Pch0JbkNK97dgrCUMK8iIfJv5)

使用 IPP 的原始特性来模糊手指协议，但是不使用预定义的变化，而是使用一个文件:

**python-m fuzzowski printer 79-f raw-r ' { { root } } \ n '–file ' path/to/my/fuzzlist '**

[**Download**](https://github.com/nccgroup/fuzzowski)**