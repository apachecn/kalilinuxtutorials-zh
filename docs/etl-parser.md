# Etl-Parser:纯 Python 中的事件跟踪日志文件解析器

> 原文：<https://kalilinuxtutorials.com/etl-parser/>

[![](img/51ea0d9c500d3cd4bb08cc4ea4744a61.png)](https://blogger.googleusercontent.com/img/a/AVvXsEiF4SWDmlGlVWIQkjYia5uSLvrQsjUJxRsLiVsRbQUuNt8RbSknKGnFuPHRrodERPlzCisY9O72VZpexkqLeHqrh836oYcmqKaAiNPSVTuayxAj3ln_RgKAEB8dIrI2_EwIzaBuDWt4vn8VexdDEK7DgQ_YtMXTE9cpkTltSBV-xotvogf_7l4jquMJ=s728)

**Etl-Parser** 是一个用于`**ETL**` Windows 日志文件的纯 Python 3 解析器库。`**ETL**`是 ETW 的默认格式，也是内核日志程序的默认格式。

没有系统依赖性，在 Windows 和 Linux 上都可以很好地工作。

由于这种格式没有记录，我们合并了 Geoff Chappe [l](https://www.geoffchappell.com/) 的博客信息和空客 CERT 团队进行的逆向工程活动。

什么是`**ETL**`,为什么工作起来很痛苦？把`ETL`看作一个容器，就像`AVI`是视频文件一样。阅读`ETL`就像在没有正确编解码器的情况下阅读`**AVI**`文件一样令人沮丧。

`**etl-parser**`试图通过包含以下众所周知的日志格式的解析器来解决这个问题:

*   ETW 清单基础提供程序
*   跟踪记录
*   内核日志的 MOF

**如何使用`etl-parser`？**

`**etl-parser**`提供两种脚本。第一个脚本`**etl2xm**l`将所有已知的 ETL 事件转换成 XML:

ETL 2 XML-I example . ETL-o example . XML

第二个脚本，`**etl2pcap**`将通过`**netsh**`创建的网络捕获转换为`p**cap**`文件格式:

**netsh start trace capture = yes
netsh stop trace
ETL 2pcap-I nettrace . ETL-o nettrace . pcap**

您也可以将`**etl-parser**`用作库:

**from ETL . ETL import IEtlFileObserver，build _ from _ stream
from ETL . system import SystemTraceRecord
from ETL . perf import perf info
from ETL . Event import Event
from ETL . Trace import Trace
from ETL . WinTrace import WinTrace
class etlfile logger(IEtlFileObserver):
def on _ system _ Trace(self，Event:SystemTraceRecord):
“Mof 内核消息，带有进程 Id 和线程 Id Event:Trace):
" " unknown " " "
def on _ Event _ record(self，Event:Event):
" " ETW 事件这是您要搜索的内容" " "
#选择与您的事件相对应的" parse_ "函数
message = Event . parse _ Trace logging()# Invoke Trace logging 解析器
message = Event . parse _ etw()# Invoke 基于清单的解析器
def on_win_trace(self，Event:win Trace):
" " unknown " " "
etw**

**安装**

`**etl-parser**`可从 pip 获得:

**pip 安装 etl 解析器**

或者，您可以使用`**setup.p**y`安装`**etl-parser**`:

**git 克隆 https://github.com/airbus-cert/etl-parser.git
CD ETL 解析器
pip install -e .**

**缺少一个解析器**？

如果您遇到解析错误，请在 Airbus CERT GitHub 存储库上打开一个问题。

**为什么是 ETL 解析器？**

日志格式有很好的文档记录，现在有很多可用的库和工具。对于`**ETL**`来说，这不是真的:在开发的时候，据我们所知没有重要的开源项目，并且`**ETL**`格式也没有很好的文档记录。

Windows 系统程序员大量使用 ETL 来记录有用的工件:

*   **T2`C:\Windows\System32\WDI\LogFiles\BootPerfDiagLogger.etl`**
*   **T2`C:\Windows\System32\WDI\LogFiles\ShutdownPerfDiagLogger.etl`**
*   **`NetTrace.etl`经`netsh`**
*   **T2`C:\Windows\System32\WDI\<GUID>\<GUID>\snapshot.etl`**
*   等等。

许多新的 API 如`**Tracelogging**`或`W**PP**`都是基于 ETW 的。这些 API 被微软 Windows 开发人员广泛使用。`**Tracelogging**`由 **`etl-parser`称呼，`WPP`** 将在以后的版本中称呼。

微软提供了很多创建 ETL 痕迹的消费者，比如**`xperf.exe``logman.exe``netsh.exe`**等。

我们认为这是 DFIR 分析师的金矿。