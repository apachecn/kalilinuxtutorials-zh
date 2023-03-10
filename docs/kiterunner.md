# Kiterunner:上下文内容发现工具

> 原文：<https://kalilinuxtutorials.com/kiterunner/>

[![Kiterunner : Contextual Content Discovery Tool](img/181a440424dc17f6ae481d9eb1fd0576.png "Kiterunner : Contextual Content Discovery Tool")](https://1.bp.blogspot.com/-wwXrhZ4-vOo/YKIPUlZPTQI/AAAAAAAAJHM/dwuPq0BV-dYejqoVjObmopnBTH0p07bDACLcBGAsYHQ/s1009/kiterunner%2B%25281%2529.png)

长期以来，内容发现一直专注于查找文件和文件夹。虽然这种方法对于托管静态文件或在部分路径上用 3xx 响应的遗留 web 服务器来说是有效的，但对于现代 web 应用程序，尤其是 API 来说不再有效。

随着时间的推移，我们已经看到投入了大量时间来使内容发现工具更快，以便可以使用更大的单词表，但是内容发现的艺术并没有得到创新。

Kiterunner 是一个工具，它不仅能够以闪电般的速度执行传统的内容发现，还能够在现代应用程序中强制路由/端点。

现代应用程序框架，如 Flask、Rails、Express、Django 和其他框架遵循显式定义路由的范例，这些路由需要特定的 HTTP 方法、头、参数和值。

当使用传统的内容发现工具时，这样的路线经常被错过并且不容易被发现。

通过整理 Swagger 规范的数据集并将其压缩到我们自己的模式中，Kiterunner 可以使用该数据集通过为它发送的每个请求发送正确的 HTTP 方法、头、路径、参数和值来强制 API 端点。

Swagger 文件是从许多数据源收集的，包括对 40 多条最常见的 swagger 路径的互联网广泛扫描。其他数据源包括通过 BigQuery 的 [GitHub 和](https://cloud.google.com/bigquery/public-data/github) [APIs.guru](https://apis.guru/) 。

**安装**

**下载一个版本**

你可以从 https://github.com/assetnote/kiterunner/releases 下载一个预建的拷贝。

**从源构建**

#编译二进制文件
make build
#symlink 你的二进制文件
ln-s $(pwd)/dist/kr/usr/local/bin/kr
#编译单词表
#kr kb 编译
kr kb 编译 routes . JSON routes . kite
# scan away
kr 扫描 hosts . txt-w routes . kite-x 20-j 100–ignore-length = 1053

JSON 数据集可以在下面找到:

*   [routes-large.json](https://wordlists-cdn.assetnote.io/rawdata/kiterunner/routes-large.json.tar.gz) (压缩 118MB，解压缩 2.6GB)
*   [routes-small.json](https://wordlists-cdn.assetnote.io/rawdata/kiterunner/routes-small.json.tar.gz) (压缩 14MB，解压缩 228MB)

或者，也可以从以下链接下载编译后的`.kite`文件:

*   [routes-large.kite](https://wordlists-cdn.assetnote.io/data/kiterunner/routes-large.kite.tar.gz) (压缩 40MB，解压缩 183M)
*   [路线-小风筝](https://wordlists-cdn.assetnote.io/data/kiterunner/routes-small.kite.tar.gz) (2MB 压缩，35MB 解压缩)

**AUR**

使用基于 Arch 的发行版的用户可以从 [AUR](https://aur.archlinux.org/packages/kiterunner-bin/) 下载预建的二进制文件。你可以使用像`yay`这样的“AUR 助手”来安装 kiterunner

**yay-S kiter runner-bin**

**用途**

**快速启动**

**kr【扫描|蛮】【旗帜】**

`**<input>**`可以是文件、域或 URI。我们会帮你解决的。更多细节见[输入/主机格式化](https://github.com/assetnote/kiterunner#inputhost-formatting)

# **只有主机列表而没有单词列表
kr scan hosts . txt-A = API routes-210328:20000-x 5-j 100–fail-status-codes 400，401，404，403，501，502，426，411
#你有自己的单词列表但你也想要 assetnote 单词列表
kr scan target.com-w routes . kite-A = API routes-211**

CLI 帮助

**用法:
风筝扫描【标志】
标志:
-A，–asset note-word list 字符串使用 wordlist.assetnote.io 中的单词列表，指定要使用的类型/名称，例如 apiroutes-210228。您可以指定一个额外的 maxlength，以便只使用单词列表中的前 N 个值，例如 API routes-210228；20000 将只使用单词列表
中的前 20000 行——黑名单——域名字符串被列入重定向黑名单的域名。我们不会跟踪到这些域的重定向
–延迟持续时间延迟放置对单个主机的请求
–禁用-预检查是否跳过主机发现
–失败-状态代码指出哪些状态代码被列入失败黑名单。如果设置了此选项，将覆盖成功-状态-代码
–过滤器-api 字符串仅扫描与此 ksuid
匹配的 API–强制-方法字符串是否忽略 ogl 文件中指定的方法并强制将此方法
-H，–头字符串头添加到请求中(默认为[x-forwarded-for:127 . 0 . 0 . 1])
-H，–扫描帮助帮助
–忽略长度字符串要忽略的内容长度字节范围。你可以有多个。例如 100-105 或 1234 或 123，34-53。这包括两端
–kite builder-full-scan 执行完全扫描，无需先执行相位扫描。
-w，–kite builder-list strings ogl wordlist 用于扫描
-x，–max-connection-per-host int 单个主机的最大连接数(默认为 3)
-j，–max-parallel-hosts int 一次扫描的最大并发主机数(默认为 50)
–max-redirects int 要跟踪的最大重定向数(默认为 3)
-d，–preflight-depth int 在执行预检检查时，我们尝试检查的目录深度。0 表示仅检查 docroot(默认为 1)
–配置文件输出文件的配置文件名称字符串名称
–扫描时显示进度条。默认情况下仅在 Stderr 上启用(默认为真)
–quarantine-threshold int 如果主机连续返回 N 次命中，我们将主机作为通配符隔离。设置为 0 以禁用(默认为 10)
–success-status-codes 指出哪些状态代码作为成功列入白名单。这是默认模式
-t，–用于所有请求的超时持续时间超时(默认 3s)
–用于请求的用户代理字符串用户代理(默认“Chrome。Mozilla/5.0(麦金塔；英特尔 Mac OS X 10 _ 15 _ 7)apple WebKit/537.36(KHTML，像 Gecko 一样)Chrome/88 . 0 . 4324 . 96 Safari/537.36”)
–通配符检测可以设置为 false 以禁用通配符重定向检测(默认为 true)
全局标志:
–配置字符串配置文件(默认为$HOME/.kiterunner.yaml)
-o，–输出字符串输出格式。可以是 json，text，pretty(默认“pretty”)
-q，–quiet 安静模式。将静音不必要的漂亮文本
-v，–日志详细程度的详细字符串级别。可以是错误、信息、调试、跟踪(默认“信息”)**

暴力标志(以上所有标志+)

这将用提供的扩展名替换%EXT%。向后兼容 dirsearch，因为 shubs 喜欢他一些 dirsearch
-e，–扩展字符串扫描时要追加的扩展
-w，–单词列表字符串用于扫描的普通单词列表

**输入/主机格式化**

当提供输入时，kiterunner 将尝试按以下顺序解析输入:

1.  是输入一个文件。如果是这样，将文件中的所有行作为单独的域读取
2.  输入被视为一个“域”

如果你提供了一个“域”，但是它是作为一个文件存在的，例如`google.com`但是`google.com`也是当前目录中的一个 txt 文件，我们将加载`google.com`这个文本文件，因为我们首先找到了它。

**域名解析**

你最好提供完整的 URI 作为输入，但是你可以提供不完整的 URIs，我们会试着猜你的意思。您可以提供的域列表示例如下:

**one.com
two.com:80
three.com:443
four.com:9447
https://five.com:9090
http://six.com:80/api**

上面的域列表将扩展到后续的目标列表中

**(为 one.com 创建了两个目标，因为没有指定端口和协议)
http://one.com(暗示端口 80)
https://one.com(暗示端口 443)
http://two.com(暗示端口 80)
https://three.com(暗示端口 443)
http://four.com:9447(非 tls 端口猜测)
https://five.com:9090
http://six.com/api(暗示端口 80；基础路径 API 追加)**

我们应用的规则是:

*   如果你提供一个方案，我们就用这个方案。
    *   我们只支持 http & https
    *   如果你不提供一个方案，我们将根据端口进行猜测
*   如果您提供一个端口，我们将使用该端口
    *   如果您的端口是 443 或 8443，我们将假定它是 tls
    *   如果您不提供端口，我们将猜测端口 80、443
*   如果您提供一个路径，我们会将该路径添加到针对该主机的所有请求中

**API 扫描**

当你只有一个目标时

**#单一目标
kr 扫描 https://target.com:8443/-w 航线. kite-A = API routes-210228:20000-X10–ignore-length = 34
#单一目标，但你想尝试 http 和 https
kr 扫描 target.com-w 航线. kite-A = API routes-210228:20000-X10–ignore-length = 34
#目标列表
kr 扫描目标. txt -w 航线**

**香草冰淇淋**

kr brute https://target.com-A = raft-large-words-A = API routes-210228:20000-x 10-d = 0–ignore-length = 34-ejson，txt

**直接搜索暴力事件**

因为当你有一个老式的单词表，并且在单词表中还有%EXT%时，你可以使用`-D`。这将仅替换路径中存在%EXT%的扩展名

**kr brute https://target.com-w dirsearch . txt-x 10-D = 0–ignore-length = 34-ejson，txt -D**

**技术特征**

**深度扫描**

kiterunner 的一个关键特性是基于深度的扫描。这试图处理给定的基于虚拟应用路径的路由检测通配符。深度定义执行基线检查的目录深度，例如

**~/kiter runner $ cat word list . txt
/API/v1/user/create
/API/v1/user/delete
/API/v2/user/
/API/v2/admin/
/secrets/v1/
/secrets/v2/**

*   深度为 0 时，只有 **`/`** 会执行通配符检测的基线检查
*   在深度 1， **`/api`** 和`**/secrets**`将执行基线检查；并且这些支票将相应地用于对抗`**/api**`和`**/secrets**`
*   在深度 2 处，**`/api/v1``/api/v2``/secrets/v1`**和 **`/secrets/v2`** 都将执行基线检查。

默认情况下，`kr scan`的深度为 1，因为从内部使用来看，我们经常看到这是虚拟路由最常见的深度。`kr brute`的默认深度为 0，因为您通常不希望使用静态单词列表来执行该检查。

自然地，增加深度会增加扫描的准确性，但是这也会增加对目标的请求数量。(`# of baseline checks * # of depth baseline directories`)。因此，我们建议不要超过 1，在极少数情况下，不要超过深度 2。

**使用资产注释单词表**

我们提供了从 assetnote.io 下载和缓存单词列表的内置功能。您可以将这些功能与接收逗号分隔的别名或全名列表的`**-A**`标志一起使用。

你可以用`**kr wordlist list**`得到所有 Assetnote 单词表的完整列表。

使用时的单词表缓存在 **`~/.cache/kiterunner/wordlists`中。**用的时候，这些都是从 **`.txt` - > `.kite`** 编译过来的

+—————————————————————————————————
|别名|文件名|源文件|计数|文件大小|缓存|
+————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————— 9996122 | 139.0 MB | false |
| cfm | cfm . txt | manual . JSON | 12100 | 260.3 kb | true |
| do | do . txt | manual . JSON | 173152 | 4.8 MB | false |
| dot _ filenames | dot _ filenames . txt | manual . JSON | 3191712 | 71.3 MB | false |
| html | html httpar chive _ API routes _ 2021 _ 01 _ 28 . txt | automated . JSON | 225456 | 6.6 MB | false |
| API routes-210228 | httpar chive _ API routes _ 2021 _ 02 _ 28 . txt | automated . JSON | 223544 | 6.5 MB | true |
| API routes-210328 | httpar chive _ API routes _ 2021 _ 03 _ 28
| aspx-210328 | httpar chive _ aspx _ ASP _ cfm _ SVC _ ashx _ asmx _ 2021 _ 03 _ 28 . txt | automated . JSON | 45928 | 926.8 kb | false |
| CGI-2011 18 | httpar chive _ CGI _ pl _ 2020 _ 11 _ 18 . txt | automated . JSON | 2637 | 44.0 kb | false |

**用途**

**kr scan targets . txt-A = API routes-210228-x 10–ignore-length = 34
kr brute targets . txt-A = aspx-210228-x 10–ignore-length = 34-easp，aspx**

**头部语法**

当使用 assetnote 提供的单词表时，您可能不想使用整个单词表，所以您可以使用`**head syntax**`选择使用给定单词表中的前 N 行。指定词表时格式为 **`<wordlist_name>:<N lines>`** 。

**用途**

# **这将使用 api routes 单词列表中的前 20000 行
kr scan targets . txt-A = API routes-210228:20000-x 10–ignore-length = 34
#这将使用 aspx 单词列表中的前 10 行
kr brute targets . txt-A = aspx-210228:10-x 10–ignore-length = 34-easp，aspx**

**并发设置/快速进行**

Kiterunner 在许多主机上运行速度很快。但是，仅仅因为你可以在 20000 goroutines 运行 kiterunner，并不意味着这是一个好主意。由于在调度等待网络 IO 和内核上下文切换的 goroutines 时花费了更多的时间，所以在高线程数时会出现瓶颈和性能下降。

kiterunner 有两个主要的并发设置:

*   `**-x, --max-connection-per-host**`–我们在一台主机上可以打开的最大连接数。由 1 个 goroutine 管理。为了避免拒绝主机，我们建议将其保持在 5-10 的低级别。根据到目标的延迟，到主机的每个连接平均每秒会产生 1-5 个请求(200 毫秒–1000 毫秒/请求)。
*   `**-j, --max-parallel-hosts**`–在任何给定时间扫描的最大主机数量。各由一名 goroutine 主管管理

根据您正在扫描的硬件，您可以优化运行的 goroutines 的“最大”数量会有所不同。在 AWS t3.medium 上，我们看到性能下降超过 2500 次。也就是说，500 台主机 x 每台主机 5 个连接器(2500)将产生最高性能。

我们建议**不要从你的 **macbook** 上运行【kiterunner。由于 macOS 上针对高 IO 计数和 Epoll 系统调用的内核优化较差，我们注意到，与在类似配置的 linux 实例上运行 kiterunner 相比，性能明显较差(0.3-0.5 倍)。**

为了最大限度地提高扫描单个目标或大型攻击面的性能，我们推荐以下技巧:

*   在与您扫描的目标相似的地理区域/数据中心启动 EC2 实例
*   使用不同的`**-x**`和 **`-j`** 选项，针对您设定的目标执行一些初始基准。我们建议以大约`**-x 5 -j 100**`为典型起点，并在 CPU 使用率/网络性能允许的情况下向上移动`**-j**`

**在文件格式之间转换**

Kiterunner 还可以让你在 JSON 模式、kite 文件和标准 txt 单词表之间进行转换。

**用途**

格式由`**<input>**`和`**<output>**`字段提供的文件类型扩展名决定。我们支持`**txt**`、`**json**`和`**kite**`

**kr kb convert word list . txt word list . kite
kr kb convert word list . kite word list . JSON
kr kb convert word list . kite word list . txt**

❯快跑。/cmd/kiterunner kb convert -qh
将输入文件格式转换为指定的输出文件格式
这将根据输入和输出的扩展名确定转换
我们支持以下文件类型:txt，json， kite
您可以将以下任何内容转换为相应的类型
-d 调试模式将尝试转换带有错误处理的模式
-v=debug Debug verbosity 将打印出模式的错误
用法:
kite kb convert[Flags]
Flags:
-d，–Debug Debug 解析
-h，–help 帮助转换
全局标志:
–配置字符串配置文件(默认为＄HOME/. kite runner . YAML)【T11 可以是 json，text，pretty(默认“pretty”)
-q，–quiet 安静模式。将屏蔽不必要的漂亮文本
-v，–日志详细程度的详细字符串级别。可以是 error、info、debug、trace(默认为“info”)“big query

**重放请求**

当您从 kiterunner 收到一堆输出时，可能很难立即理解为什么一个请求会导致特定的响应代码/长度。Kiterunner 提供了一种从使用的单词列表中重建请求的方法，包括所有的头和主体参数。

*   您可以通过将完整的响应输出复制粘贴到`**kb replay**`命令中来重放请求。
*   您可以指定一个`**--proxy**`来转发您的请求，因此如果您愿意，您可以使用第三方工具来修改/重复/拦截请求
*   golang net/http 客户端将对您的请求执行一些额外的更改，因为默认的 golang 规范实现方式(不幸的是)。

❯快跑。/cmd/kite runner kb replay-q–proxy = http://localhost:8080-w routes . kite " POST 403[287，10，1]https://target . com/de dalo/lib/de dalo/publication/server _ API/v1/JSON/thesaurus _ parents 0 cc 39 f 76702 ea 287 EC 3 e 93 f 4 b 4710 db 9 c 8 a 86251 "
11:25AM INF 原始重建请求 ar _ fields = 48637466&code = 66132381&db _ name = 08791392&lang = LG-eng&recursive = false&term _ id = 72336471 HTTP/1.1
Content-Type:any
11:25AM INF 出站请求
POST/dedalo/lib/dedalo/publication/server _ API/v1/JSONar _ fields = 48637466&code = 66132381&db _ name = 08791392&lang = LG-eng&recursive = false&term _ id = 72336471 HTTP/1.1
主机:target.com
用户代理:Go-HTTP-client/1.1
Content-Length:0
Content-Type:any
接受

**技术实现**

**中间数据类型(PRoutes)**

我们在 kiterunner 中使用单词列表和 kitebuilder json 模式的中间表示。这允许我们动态地生成单词列表中的字段，并根据给定的规范重建请求体/头和查询参数。

PRoute 类型由编码在`**pkg/proute.Crumb**`中的头、主体、查询和 Cookie 参数组成。Crumb 类型是在 UUIDs、Floats、int、Random Strings 等类型上实现的接口。

当执行 txt、json 和 kite 文件之间的转换时，所有的转换都首先转换到`**proute.API**`中间类型。然后写出相应的编码

**风筝文件格式**

我们使用一种超级秘密的 kite 文件格式来存储来自 kitebuilder 的 json 模式。这些只是 protobuf 编码的 **`pkg/proute.APIS`** 写到一个文件中。编译用于允许我们快速反序列化已经解析的单词列表。这种文件格式不稳定，只能使用 kiterunner 内置的转换工具进行交互。

当新版本的 kite 文件格式发布时，你可能需要重新编译你的 kite 文件

[**Download**](https://github.com/assetnote/kiterunner)