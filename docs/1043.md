# FFUF:用 Go 编写的快速 Web Fuzzer

> 原文：<https://kalilinuxtutorials.com/ffuf-fast-web-fuzzer-written-in-go/>

[![FFUF : Fast Web Fuzzer Written In Go](img/f024f45e88c3eb038b86bd1e77a4c4de.png "FFUF : Fast Web Fuzzer Written In Go")](https://1.bp.blogspot.com/-ay-eYmSpZEY/XfDxhv1AxcI/AAAAAAAAD6c/N2LgLXqj6Xov9OR0q5tyQQtwiteqMiKGACLcBGAsYHQ/s1600/Fast%2BWeb%2BFuzzer.png)

FFUF 是一个用 Go 编写的快速 web fuzzer。因此，让我们来看看这个工具的一些特性，这将使用户对它有更多的了解；

*   快！
*   允许模糊化 HTTP 头值、POST 数据和 URL 的不同部分，包括 GET 参数名和值
*   静默模式用于干净的输出，易于在其他进程的管道中使用。
*   模块化架构，允许通过合理的努力与现有工具链集成
*   易于添加的过滤器和匹配器(它们可以互操作)

**示例案例**

**典型目录发现**

[![](img/feee9e852cd0b911d2bd5ae7d5c44226.png)](https://asciinema.org/a/211360)

[![](img/064bbaaf99dd652fa7e04a27a63ff604.png)](https://asciinema.org/a/211350)

[![](img/feee9e852cd0b911d2bd5ae7d5c44226.png)](https://asciinema.org/a/211360)

[![](img/def3d801e6224411dff3ce873600a8a8.png)](https://asciinema.org/a/94462)

**也可阅读-[反垃圾邮件:检测一次性电子邮件地址](https://kalilinuxtutorials.com/antidisposmail-detecting-disposable-email-addresses/)**

通过在 URL 的末尾使用 FUZZ 关键字(`**-u**`):

**ffuf-w/path/to/word list-u https://target/FUZZ**

**虚拟主机发现(无 DNS 记录)**

[![](img/feee9e852cd0b911d2bd5ae7d5c44226.png)](https://asciinema.org/a/211360)

假设默认的 virtualhost 响应大小是 4242 字节，我们可以过滤掉所有具有该大小的响应(`-fs 4242`)，同时模糊化 Host-header:

**ffuf-w/path/to/vhost/word list-u https://target-H " Host:FUZZ "-fs 4242**

**获取参数模糊化**

GET 参数名称模糊化非常类似于目录发现，其工作原理是将`FUZZ`关键字定义为 URL 的一部分。这还假设无效 GET 参数名称的响应大小为 4242 字节。

**ffuf-w/path/to/param names . txt-u https://target/script . PHP？FUZZ=test_value -fs 4242**

如果参数名是已知的，可以用同样的方法对值进行模糊处理。此示例假设一个错误的参数值返回 HTTP 响应代码 401。

**ffuf-w/path/to/values . txt-u https://target/script . PHP？valid_name=FUZZ -fc 401**

**发布数据模糊化**

这是一个非常简单的操作，也是通过使用`FUZZ`关键字。这个例子只是模糊了 POST 请求的一部分。我们再次过滤掉了 401 条回复。

**ffuf-w/path/to/POST data . txt-X POST-d " username = admin \&password = FUZZ "-u https://target/log in . PHP-fc 401**

**使用外部变异器产生测试用例**

对于这个例子，我们将模糊通过 POST 发送的 JSON 数据。 [Radamsa](https://gitlab.com/akihe/radamsa) 用作变异算子。

当使用`**--input-cmd**`时，ffuf 将显示匹配的位置。这个相同的位置值将作为环境变量`**$FFUF_NUM**`提供给被调用者。我们将使用这个位置值作为 mutator 的种子。文件 example1.txt 和 example2.txt 包含有效的 JSON 有效负载。我们匹配所有的响应，但是过滤掉响应代码 **`400 - Bad request` :**

**FFUF–input-cmd ' Rada MSA–seed $ FFUF _ NUM example 1 . txt example 2 . txt '-H " Content-Type:application/JSON "-X POST-u https://ffuf.io.fi/-MC all-fc 400**

**用途**

要定义 ffuf 的测试用例，可以在 URL ( **`-u`** )、标题(`**-H**`)或 POST 数据(`**-d**`)的任何地方使用关键字`**FUZZ**`。

的用法。/ffuf:
-D DirSearch 样式单词表兼容模式。与-e 标志一起使用。用-e.
-H "Name: Value"
标题" Name: Value "提供的每个扩展名替换单词列表条目中的%EXT%,用冒号分隔。接受多个 H 标志。
-V 显示版本信息。
-X 字符串
要使用的 HTTP 方法(默认“GET”)
-AC
自动校准过滤选项
-acc 值
自定义自动校准字符串。可以多次使用。implies-AC
-b " name 1 = value 1；name 2 = value 2 "
Cookie data " name 1 = value 1；NAME2=VALUE2”，用于复制为卷曲功能。
与-H "Cookie: …"
-c 彩色化输出结合使用时，结果不可预测。
-复制为 curl 功能的压缩
虚拟标志(忽略)(默认为真)
-cookie 值
Cookie 数据(别名为-b)
-d 字符串
POST 数据
-数据字符串
POST 数据(别名为-d)
-数据-ascii 字符串
POST 数据(别名为-d)
-数据-二进制字符串
POST 数据(别名为-d)
-调试日志字符串【日志
-e 字符串
逗号分隔的要应用的扩展名列表。提供的每个扩展将扩展单词列表条目一次。
-fc 字符串
从响应中过滤 HTTP 状态代码。代码和范围的逗号分隔列表
-fl 字符串
根据响应的行数过滤。逗号分隔的行数和范围列表
-fr string
Filter regexp
-fs string
Filter HTTP 响应大小。逗号分隔的大小和范围列表
-fw 字符串
根据响应的字数进行过滤。字数和范围的逗号分隔列表
-i 复制为卷曲功能的虚拟标志(忽略)(默认为真)
-输入-cmd 值
产生输入的命令。–使用此输入法时需要输入数字。overrides-w .
-input-num int
要测试的输入数量。与–input-cmd 一起使用。(默认值为 100)
-k TLS 身份验证
-mc 字符串
匹配来自 respose 的 HTTP 状态代码，使用“all”匹配每个响应代码。(默认“200，204，301，302，307，401，403”)
-ml 字符串
匹配响应的行数
-mode 字符串
多词表操作模式。可用模式:clusterbomb、pitchfork(默认为“cluster bomb”)
-Mr string
Match regexp
-ms string
Match HTTP response size
-MW string
Match word amount of response
-o string
Write Output to file
-of string
输出文件格式。可用格式:json、ejson、html、md、csv、ecsv(默认“JSON”)
-p delay
请求之间的延迟秒，或者随机延迟的范围。例如“0.1”或“0.1-2.0”
-r 跟随重定向
-s 不打印附加信息(静默模式)
-sa
在所有错误情况下停止。隐含-sf 和-se
-se
在虚假错误上停止
-sf
在> 95%的响应返回 403 禁止
时停止-t int
并发线程数。(默认为 40)
-超时 int
HTTP 请求超时，以秒为单位。(默认 10)
-u string
目标 URL
-v 详细输出，打印完整的 URL 和重定向位置(如果有)以及结果。
-w 值
单词列表文件路径和(可选)自定义模糊关键字，使用冒号作为分隔符。使用文件路径“-”读取标准输入。可以多次提供。格式:'/path/to/word list:KEYWORD '
-x string
HTTP 代理 URL

**安装**

*   [从](https://github.com/ffuf/ffuf/releases/latest)[发布页面](https://github.com/ffuf/ffuf/releases/latest)下载一个预构建的二进制文件，解压并运行！或者
*   如果你安装了 go 编译器:`**go get github.com/ffuf/ffuf**`

ffuf 唯一的依赖就是 Go 1.11。不需要 Go 标准库之外的依赖。

**变更日志**

*   **主人**
    *   **新**
    *   **改变了**
        *   将`**-e**`(扩展)的使用限制在一个关键词:FUZZ
*   **v0.12**
    *   **新**
        *   增加了一个新的标志来选择多单词列表操作模式:`**--mode**`，可能的值:`**clusterbomb**`和`**pitchfork**`。
        *   添加了一个新的输出文件格式 eJSON，用于始终对输入数据进行 base64 编码。
        *   重定向位置总是显示在输出文件中(当使用`**-o**`时)
        *   完整的 URL 总是显示在输出文件中(当使用`**-o**`时)
        *   HTML 输出格式得到了数据表的支持，允许实时搜索，按列排序等。
        *   详细输出的新 CLI 标志`**-v**`。包括完整的 URL 和重定向位置。
        *   SIGTERM 监控，为了捕捉键盘中断，能够在退出前写`**-o**`文件。
    *   **改变了**
        *   修正了默认多单词列表模式下的一个错误
        *   修复了 JSON 输出回归，其中所有输入数据总是以 base64 编码
        *   `--debug-log`没有正确记录连接错误
        *   移除了`-l`标志，支持`-v`
        *   更多详细信息显示在启动的横幅。
*   **v0.11**
    *   **新**
        *   新 CLI 标志:-l，显示重定向响应的目标位置
        *   新 CLI flac: -acc，自定义自动校准字符串
        *   新 CLI 标志:-debug-log，将调试日志写入指定文件。
        *   新的 CLI 标志-ml 和-fl，过滤/匹配响应中的行数
        *   通过定义多个-w 命令行标志，能够使用多个单词列表/关键字。如果没有定义关键字，默认为 FUZZ 以保持向后兼容性。例子:`-w "wordlists/custom.txt:CUSTOM" -H "RandomHeader: CUSTOM"`。
    *   **改变了**
        *   新的 CLI 标志:-i，不执行任何操作的虚拟标志。为了与 curl 格式的副本兼容。
        *   新的 CLI 标志:-b/–cookie，cookie 数据与 copy as curl 兼容。
        *   新输出格式可用:HTML 和 Markdown 表。
        *   新 CLI 标志:-l，显示重定向响应的目标位置
        *   通过状态代码、响应大小或字数进行过滤和匹配现在允许使用除单个值之外的范围
        *   要丢弃的内部日志记录信息，可以用新的`-debug-log`标志写入文件。
*   **v0.10**
    *   **新**
        *   新的 CLI 标志:-ac 根据几个预设的 URL 自动校准响应大小和单词过滤器。
        *   新的 CLI 标志:-timeout 为所有 HTTP 请求指定自定义超时。
        *   新的 CLI 标志:–与浏览器的复制为卷曲功能兼容的数据。
        *   新 CLI 标志:–压缩的哑标志，不起任何作用。为了与 curl 格式的副本兼容。
        *   新的 CLI 标志:–input-cmd 和–input-num，用于使用外部命令处理输入生成。比如变异体。环境变量 FFUF_NUM 将在每次调用该命令时更新。
        *   当使用–input-cmd 时，在结果中显示位置而不是有效载荷。然而，除了位置之外,(所有格式的)输出文件将包括有效载荷。
    *   **改变了**
        *   单词表也可以从标准输入中读取
        *   定义-d 或 data 意味着 POST 方法，如果-X 没有将它设置为 GET 之外的其他值
*   **v0.9**
    *   **新**
        *   新的输出文件格式:CSV 和 eCSV (CSV 带有 base64 编码的输入字段，以避免 CSV 因有效负载包含逗号而中断)
        *   遵循重定向的新 CLI 标志
        *   错误连接将被停用一次
        *   状态栏中的错误计数器
        *   新的 CLI 标志:-se(出现虚假错误时停止)和-sa(出现所有错误时停止，意味着-se 和-sf)
        *   新的 CLI 标志:-e 提供添加到单词列表条目的扩展名列表，以及-D 提供 DirSearch 单词列表格式兼容性。
        *   响应状态代码匹配器的通配符选项。
*   **v0.8**
    *   **新**
        *   将输出以 JSON 格式写入文件的新 CLI 标志
        *   停止虚假 403 响应的新 CLI 标志
    *   **改变了**
        *   正则表达式匹配/过滤现在匹配响应正文旁边的标题

[**Download**](https://github.com/ffuf/ffuf)