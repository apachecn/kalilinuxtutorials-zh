# Heyserial:以编程方式为反序列化利用创建搜索规则

> 原文：<https://kalilinuxtutorials.com/heyserial/>

[![](img/68f049a18cd7db3dedb0b7ffe0f8a2d8.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjZ3YqTPuq67hgguRqC-iJSqjOQkO9h4kmnBpTsg89LA_5oAC_u_qUQ8UsnzrR1lv-hQr-5ufP68ZGA8M3Apmu2ON2qAE2oo-Ig4t0kvxAa3X9EXhkk4aQs2BwcJniSA1zhEOJnPMlJl7VkdawdjKD1uslEIb7gfz2NiSD8zfPxxeiNebuUSXUlIkth/s728/binance_10_trading_fee%20(1).png)

Heyserial 将以编程方式创建搜索规则，用于反序列化利用多个

*   关键词(如 cmd.exe)
*   小工具链(例如 CommonsCollection)
*   对象类型(例如，视图状态、Java、Python Pickle、PHP)
*   编码(例如 Base64、raw)
*   规则类型(例如 Snort、Yara)

### 使用

帮助:`**python3 heyserial.py -h**`

示例:

**python 3 hey serial . py-c ' example chain::condition 1+condition 2 '-t JavaObj
python 3 hey serial . py-k cmd.exe whoami '此文件不能在 DOS 模式下运行'
python3 heyserial.py -k 进程。start-t NETViewState-e base64 " base64+ut F16 le "**

# Utils

### utils/checkyoself.py

这是一个在各种样本文件上自动化批量测试 Snort 和 Yara 规则的工具。

用法:`**python3 checkyoself.py [-y rules.yara] [-s rules.snort] [-o file_output_prefix] [--matches] [--misses] -d malware.exe malware.pcap**`

例子:`**python3 checkyoself.py -y rules/javaobj -s rules/javaobj -d payloads/javaobj pcaps --misses -o java_misses**`

### utils/generate_payloads.ps1

YSoSerial.NET 1.34 版有效载荷生成。在 Windows 上从。/utils 目录。

*   资料来源:https://github.com/pwntester/ysoserial.net
*   许可证:ysoserial.net_LICENSE.txt

### utils/generate_payloads.sh

yso 串行有效负载生成。在 Linux 上从。/utils 目录。

*   资料来源:https://github.com/frohoff/ysoserial
*   许可证:ysoserial_LICENSE.txt

### utils/install_snort.sh

在基于 Debian 的系统上安装 Snort 对我来说有点麻烦，所以我在这里写了安装说明。

在您最近拍摄的虚拟机中使用，风险自负。

### utils/server.py

在 127.0.0.1:12345 上运行 HTTP 服务器并接受 POST 请求的简单 Python 脚本。

方便生成测试 PCAPs。

[**Download**](https://github.com/mandiant/heyserial)