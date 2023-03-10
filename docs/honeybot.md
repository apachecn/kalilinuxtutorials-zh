# HoneyBot:捕获、上传和分析网络流量

> 原文：<https://kalilinuxtutorials.com/honeybot/>

[![HoneyBot : Capture, Upload & Analyze Network Traffic](img/41824b6b0834dd91ca561c5c8e0453fc.png "HoneyBot : Capture, Upload & Analyze Network Traffic")](https://1.bp.blogspot.com/-T6frwIg-eBA/XmaWEHT-rUI/AAAAAAAAFWk/_ECyemtGK2kYCB7X7uZswNuBzleS4psRgCLcBGAsYHQ/s1600/HoneyBot%25281%2529.png)

HoneyBot 是一组脚本和库，用于通过 PacketTotal.com 捕获和分析数据包。目前，该库提供了三种脚本:

*   `**capture-and-analyze.py**`——在一个界面上捕获一段时间，并上传捕获进行分析。
*   `**upload-and-analyze.py**`–向 PacketTotal.com 上传并分析多个数据包捕获。
*   `**trigger-and-analyze.py**`–监听未知连接，并在建立连接时开始捕获。捕获会自动上传和分析。

**警告:**任何上传到的数据包捕获在完成分析后将公开。

**限制**

*   只有。pcap 和。支持 pcapng 文件。
*   最大 6 MB 分析。

**用例**

*   设置您的蜜罐，将网络流量直接传输到 PacketTotal.com 进行分析。
*   分析恶意 PCAPs 的个人存储库。
*   确定数百个数据包捕获的良性。
*   自动分析(和共享)蜜罐数据包捕获。
*   自动化初步恶意软件分析/分类。

**又念——[推特网:监控推特流 2020](https://kalilinuxtutorials.com/twitwork/)**

**先决条件**

*   必须安装 WireShark 。
    *   如果你使用的是基于 linux 的操作系统，你可以安装 t-shark
        *   **T2`apt-get install tshark`**
*   [需要 Python 3.5](https://www.python.org/downloads/) 或更高版本。
*   在利用这些脚本之前，您必须[请求一个 api 密钥](https://packettotal.com/api.html)。

**安装**

**pip install-r requirements . txt
python setup . py 安装**

**用途**

**capture-and-analyze.py**

**用法:**Capture-and-analyze . py[-h][–SECONDS SECONDS][–INTERFACE INTERFACE]
[–analyze][–list-interfaces][–list-pcaps]
[–export-pcaps]

**捕获、上传并分析网络流量；由 PacketTotal.com 提供动力。**

**可选参数:**
-h，–help 显示此帮助消息并退出
–SECONDS 秒捕获流量的秒数。
–接口 INTERFACE
接口的名称(–list-interfaces 以显示
可用)
–analyze 如果包含，捕获将被上传到
PacketTotal.com 进行分析。
–list-interfaces 列出可用的接口。
–list-pcap 列出提交给 PacketTotal.com 进行分析的 pcap。
–export-pcaps 将提交给 PacketTotal.com 进行分析的 pcaps 写入 csv 文件。

**上传并分析. py**

用法:Upload-and-analyze . py[-h][–PATH PATH[PATH…]][–analyze]
[–list-pcaps][–export-pcaps]

上传分析。pcap/。批量 pcapng 文件；由 PacketTotal.com 提供动力。

可选参数:
-h，–help 显示此帮助信息并退出
–PATH PATH[PATH…]
指向 pcap 或 pcap 目录的一个或多个路径。
–分析如果包含，捕获的图像将上传至
PacketTotal.com 进行分析。
–list-pcap 列出提交给 PacketTotal.com 进行分析的 pcap。
–导出-pcaps 将提交给 PacketTotal.com 进行分析的 pcaps 写入 csv 文件。

**trigger-and-analyze.py**

**用法:**trigger-and-analyze . py[-h][–INTERFACE INTERFACE][–LEARN LEARN]
[–Listen][–CAPTURE-SECONDS CAPTURE _ SECONDS]
[–list-interfaces][–list-pcaps]
[–export-pcaps]

**监听未知连接，一旦有连接，就开始捕获。捕获会自动上传并进行分析；由 PacketTotal.com 提供**

**可选参数:**
-h，–help 显示此帮助消息并退出
–INTERFACE INTERFACE
接口的名称(–list-interfaces to show
available)
–LEARN 建立已知
连接白名单的秒数。白名单
中的连接将被忽略。
–监听如果包含，我们将开始监听未知的
连接，并立即开始数据包捕获
并上传到 PacketTotal.com 进行分析。
–CAPTURE-SECONDS CAPTURE _ SECONDS
触发触发器后需要
捕获和分析的网络流量的秒数。
–list-interfaces 列出可用的接口。
–list-pcap 列出提交给 PacketTotal.com 进行分析的 pcap。
–导出-pcaps 将提交给 PacketTotal.com 进行分析的 pcaps 写入 csv 文件。

[**Download**](https://github.com/PacketTotal/HoneyBot)