# IOCExtract:高级危害指示器(IOC)提取器

> 原文：<https://kalilinuxtutorials.com/iocextract/>

[![IOCExtract : Advanced Indicator Of Compromise (IOC) Extractor](img/325d3f1bdc934f652650ab941831f15e.png "IOCExtract : Advanced Indicator Of Compromise (IOC) Extractor")](https://1.bp.blogspot.com/-bzm1TCH_HBc/XPiIxozJqKI/AAAAAAAAAqk/H9GEOtZ7W5syEAH1Sg2tnm_2fUINx0fDACLcBGAs/s1600/Indicator%2BOf%2BCompromise%25281%2529.png)

IOCExtract 是一个高级的危害指示器(IOC)提取器。这个库从文本语料库中提取 URL、IP 地址、MD5/SHA 散列、电子邮件地址和 YARA 规则。它在输出中包含一些编码的和“缺省的”IOC，并可选地解码/重构它们。

**问题**

恶意软件分析师或终端软件通常会“方得”URL 和 IP 地址等 IOC，以防止意外接触实时恶意内容。能够提取和汇总这些 IOC 对于分析师来说通常是有价值的。不幸的是，现有的“IOC 提取”工具经常绕过它们，因为它们没有被标准正则表达式捕获。

例如，用括号将句点括起来的简单去边框技术:

**127。]0[.]0[.]1**

使用简单 IP 地址正则表达式的现有工具将完全忽略这个 IOC。

**也可阅读-[phones Piot:使用开放的 ADB 端口，我们可以利用 Android 设备](https://kalilinuxtutorials.com/phonesploit-adb-ports-exploit-andriod/)**

**解决方案**

通过将特制的正则表达式与一些定制的后处理相结合，我们能够检测并去除“去除毛刺”的 IOC。这为分析人员节省了时间和精力，否则他们可能不得不手动查找 IOC 并将其转换成机器可读的格式。

**一个简单的用例**

许多推特用户发布 C2s 或其他有价值的国际奥委会信息，并附上被篡改的网址。比如，[这条来自@研讯](https://twitter.com/InQuest/status/969469856931287041)的推文:

*   推荐阅读及佳作来自@ unit 42 _ Intel:https://research center . Palo alto networks . com/2018/02/unit 42-sofa cy-attacks-multiple-government-entities/…
*   调查客户已检测到来自 hotfixmsupload 的威胁。]com
*   自 2017 年 3 月 6 日和 cdnverify[。]网自 2018 年 2 月 1 日。

如果我们通过提取器运行它，我们可以很容易地提取出 URL:

*   https://researchcenter.paloaltonetworks.com/2018/02/unit42-sofacy-attacks-multiple-government-entities/
*   hotfixmsupload[。]com
*   cdnverify[。]net

在提取时传入`refang=True`会消除混淆，但是因为这些是真实的 IOC，所以让我们在文档中保留它们的默认值。🙂

**安装**

为了安装`regex`依赖项，您可能需要安装 Python 开发头文件。在基于 Ubuntu/Debian 的系统上，尝试:

**sudo apt-get 安装 python-dev**

然后从 pip 安装`iocextract`:

**pip 安装 iocextract**

如果您在 Windows 上安装有问题，尝试通过从 PyPI 下载[合适的轮子并运行例如:](https://pypi.org/project/regex/#files)

**pip 安装 regex-2018 . 06 . 21-cp27-none-win _ amd64 . whl**

**用途**

尝试提取一些默认的 URL:

**content = " " " "
…我真的很爱榜样。]com！
…这些天所有的机器人都在 hxxp://example.com/bad/url 上。C2: tcp://example。]com:8989/bad
… """
为 IOC extract . extract _ urls(content)中的 URL 导入 IOC extract
:
…打印 URL
…
hxxp://example . com/bad/URL
TCP://example[。]com:8989/bad
示例[。]com
tcp://example[。]com:8989/bad**

请注意，如果被多个正则表达式捕获，一些 URL 可能会出现两次。

如果您愿意，还可以“refang ”,或者从 IOC 中删除常见的混淆方法:

**对于 iocextract.extract_urls 中的 URL(content，refang=True):
…打印 URL
…
http://example.com/bad/url
http://example.com:8989/bad
http://example.com
http://example.com:8989/bad**

您甚至可以提取和解码十六进制编码和 base64 编码的 URL:

**>>>content = ' 612062756 e 6368206 f 6620776 f 72647320687474703 a2 F2 f 6578616d 706 c 652 e 636 f 6 D2 f 70617468206 d6f 726520776 f 726473 '
为 iocextract.extract_urls 中的 URL(content**

这个库中的所有函数都返回迭代器，而不是列表。这种行为的好处是`iocextract`可以用非常低的开销处理非常大的输入。但是，如果出于某种原因，您需要多次迭代 IOC，那么您必须将结果保存为一个列表:

**> > >列表(IOC extract . extract _ URLs(content))[' hxxp://example . com/bad/URL '，' tcp://example[。]com:8989/bad '，'例[。]com '，' tcp://example[。]com:8989/bad']**

还包括一个命令行工具:

**$ iocextract -h
用法:IOC extract[-h][–INPUT INPUT][–OUTPUT OUTPUT][–extract-emails]
[–extract-IPS][–extract-ipv6s]
[–extract-URLs][–extract-yara-rules][–extract-hashes]
[–custom-REGEX REGEX _ FILE][–refang][–strip-URLs]
[–wide]

如果没有指定参数
，默认行为是提取所有的 IOC。

可选参数:
-h，–帮助显示此帮助消息并退出
–输入输入默认值:stdin
–输出输出默认值:stdout
–extract-emails
–extract-IPS
–extract-ipv4s
–extract-ipv6s
–extract-URLs
–extract-yara-rules
–extract-hashes
–custom-REGEX _ FILE 默认:
否
–宽预处理输入，允许宽编码字符**
**匹配。默认:否**

只有 URL、电子邮件和 IPv4 地址可以被“重新分配”。

**更多详情**

该库目前支持下列 IOC:

*   IP 地址
    *   完全支持 IPv4
    *   部分支持 IPv6
*   资源定位符
    *   使用协议说明符:http、https、tcp、udp、ftp、sftp、ftps
    *   使用`[.]`锚，即使没有协议说明符
    *   支持 IPv4 和 IPv6(RFC 2732)URL
    *   带有协议说明符的十六进制编码的 URL:http、https、ftp
    *   使用协议说明符的 URL 编码的 URL:http、https、ftp、ftps、sftp
    *   使用协议说明符的 Base64 编码的 URL:http、https、ftp
*   电子邮件
    *   部分支撑，固定在`@`或`at`上
*   YARA 规则
    *   包含导入、包含和注释
*   混杂
    *   讯息摘要 5
    *   SHA1
    *   SHA256
    *   SHA512
*   自定义正则表达式
    *   只有一个捕获组

对于 IPv4 地址，支持以下方得技术:

| 技术 | 被剥夺的 | 重新调整 |
| --- | --- | --- |
| `. -> [.]` | 1[.]1[.]1[.]1 | 1.1.1.1 |
| `. -> (.)` | 1(.)1(.)1(.)1 | 1.1.1.1 |
| `. -> \.` | `1\.1\.1\.1` | 1.1.1.1 |
| 部分的 | 1[.1[.1.]1 | 1.1.1.1 |
| 任何组合 | 1.)1[.1.)1 | 1.1.1.1 |

对于电子邮件地址，支持以下方得技术:

| 技术 | 被剥夺的 | 重新调整 |
| --- | --- | --- |
| `. -> [.]` | me@example[。]com | [me@example.com](mailto:me@example.com) |
| `. -> (.)` | me @例(。)com | [me@example.com](mailto:me@example.com) |
| `. -> {.}` | [me@example。}com](mailto:me@example{.}com) | [me@example.com](mailto:me@example.com) |
| `. -> _dot_` | [me@example](mailto:me@example) 点 com | [me@example.com](mailto:me@example.com) |
| `@ -> [@]` | me[@]example.com | [me@example.com](mailto:me@example.com) |
| `@ -> (@)` | me(@)example.com | [me@example.com](mailto:me@example.com) |
| `@ -> {@}` | [me{@}example.com](mailto:me{@}example.com) | [me@example.com](mailto:me@example.com) |
| `@ -> _at_` | 我在 example.com | [me@example.com](mailto:me@example.com) |
| 部分的 | me@}示例[。com | [me@example.com](mailto:me@example.com) |
| 添加的空格 | [me @例](mailto:me@example)【例。] com | [me@example.com](mailto:me@example.com) |
| 任何组合 | me @example [。)com | [me@example.com](mailto:me@example.com) |

对于 URL，支持以下方得技术:

| 技术 | 被剥夺的 | 重新调整 |
| --- | --- | --- |
| `. -> [.]` | `example[.]com/path` | `http://example.com/path` |
| `. -> (.)` | `example(.)com/path` | `http://example.com/path` |
| `. -> \.` | `example\.com/path` | `http://example.com/path` |
| 部分的 | `http://example[.com/path` | `http://example.com/path` |
| `/ -> [/]` | `http://example.com[/]path` | `http://example.com/path` |
| [思科 ESA](https://www.cisco.com/c/en/us/support/docs/security/email-security-appliance/118775-technote-esa-00.html) | `http:// example .com /path` | `http://example.com/path` |
| `:// -> __` | `http__example.com/path` | `http://example.com/path` |
| `:// -> :\\` | `http:\\example.com/path` | `http://example.com/path` |
| `hxxp` | `hxxp://example.com/path` | `http://example.com/path` |
| 任何组合 | `hxxp__ example( .com[/]path` | `http://example.com/path` |
| 十六进制编码 | `687474703a2f2f6578616d706c652e636f6d2f70617468` | `http://example.com/path` |
| urlencode | `http%3A%2F%2fexample%2Ecom%2Fpath` | `http://example.com/path` |
| Base64 编码 | `aHR0cDovL2V4YW1wbGUuY29tL3BhdGgK` | `http://example.com/path` |

请注意，上面的表格并不详尽，也可以正确提取其他 URL/方得模式。如果您注意到某些东西丢失或不能正常工作，请随时通过 GitHub [问题](https://github.com/inquest/python-iocextract/issues)让我们知道。

base64 正则表达式是用 [@deadpixi](https://github.com/deadpixi) 的 [base64 正则表达式工具](http://www.erlang-factory.com/upload/presentations/225/ErlangFactorySFBay2010-RobKing.pdf)生成的。

**自定义正则表达式**

如果您想使用 CLI 提取 IOC，使用您自己的自定义正则表达式，创建一个每行有一个正则表达式字符串的纯文本文件，并使用`--custom-regex`标志传递它。确保每个正则表达式字符串恰好包含一个[捕获组](https://www.regular-expressions.info/brackets.html)。例如:

**http://(例\。com)/
(？:https|ftp)://(示例\。com)/**

这个自定义正则表达式文件将从匹配的 URL 中提取域`example.com`。`(?: )`非捕获组将不包括在比赛中。

如果您想提取整个匹配，只需将整个正则表达式字符串括起来，如下所示:

**(https？://.*?。com)**

如果您的正则表达式无效，您将看到如下错误消息:

**自定义正则表达式错误:位置 5** 处缺失)

如果您的正则表达式不包含捕获组，您将看到如下错误消息:

**自定义正则表达式错误:没有这样的组**

[**Download**](https://github.com/inquest/python-iocextract)