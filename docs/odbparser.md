# ODBParser : OSINT 工具，只搜索、解析和转储开放的 Elasticsearch 和 MongoDB 目录，这些目录包含您想要公开的数据

> 原文：<https://kalilinuxtutorials.com/odbparser/>

[![](img/723e6f7c0bcdd8183093c5688e1086a5.png)](https://1.bp.blogspot.com/-8i14nJL_QKM/YT7GdEiJbJI/AAAAAAAAK0A/E4mYvV5MBhAmLXbiZOFllLKLyO8eSqjOACLcBGAsYHQ/s728/glassdb%2B%25281%2529.png)

**ODBParser** 是一个在开放数据库中搜索 PII 被曝光的工具。

**仅用于识别暴露的 PII，警告服务器所有者不负责任的数据库维护
或查询您有权访问的数据库！**

**请负责任地使用**

**这是什么？**

我写这篇文章是想创建一个一站式的搜索、解析和分析开放数据库的工具，以识别第三方服务器上 PII 的泄漏。其他工具似乎要么只搜索开放的数据库，要么一旦你识别出它们就将它们转储，然后不加选择地获取数据。从一两个函数变成了这个回购协议中的东西，所以代码并不像它应该的那样干净漂亮。

**特色**

要识别打开的数据库，您可以:

*   使用所有可能的参数查询 **Shodan** 和 **BinaryEdge** (按国家、端口号等过滤)
*   指定单个 IP 地址
*   加载包含 IP 地址列表的文件
*   从剪贴板粘贴 IP 地址列表

转储选项:

*   解析所有数据库/集合以识别您指定的数据
*   获取服务器上托管的所有内容
*   仅获取一个索引/集合
*   使用 ctrl+c 跳过转储某些索引

后处理:

*   将 JSON 转储转换为 CSV
*   从 CSV 中删除无用的列

其他功能:

*   跟踪您查询的所有 IP 地址和数据库，以及每台服务器的相关信息。
*   维护统计文件，包含您查询的 IP 数量、您解析的数据库数量和您转储的记录数量
*   将您已经拥有的 JSON 转储转换为 CSV
*   对于每个记录总数超过限制的数据库，脚本将在一个特殊的文件中创建一个条目以及 5 个样本记录，以便您可以检查并决定该数据库是否值得抓取
*   默认输出是行分隔的 JSON 文件，每行有一个 JSON 对象。通过使用“proper JSON”标志，您可以选择让它输出一个“正确的 JSON”文件
*   您可以动态地将文件转换为 CSV 格式，也可以在运行完成后只转换某些文件(我推荐后者)。转换后的 JSON 文件将被移动到同一目录下名为“JSON backups”的文件夹中。**注意:**当转换为 CSV 时，脚本会删除完全重复的行，并删除所有值都为 NaN 的列和行，因为这是我想要做的。如果你想得到 JSON 文件的精确副本，请随意编辑函数。
*   **Windows ONLY** 如果脚本撤回大量包含您关心的字段的索引，脚本将列出数据库的名称，暂停并给你十秒钟时间来决定是否要继续并从每个索引中提取所有数据，因为我发现如果即使在您指定了您想要的字段后，返回了太多的数据库，很有可能数据是假的或无用的日志，并且您通常可以从名称中判断是否是这种情况。如果你不在 10 秒内采取行动，脚本将继续转储每个索引。
*   正如您可能已经注意到的，许多人一直在扫描 MongoDB 数据库并将它们作为人质，经常将名称更改为类似“TO _ RESTORE _ EMAIL _ xxxrestore . com”的内容。MongoDb scraper 将通过对照指示 pwnage 的字符串列表来检查 DB/collection 的名称，从而忽略所有已经被 pwned 的数据库和集合
*   脚本相当冗长(可能太冗长了)，但我喜欢看到发生了什么。如果你愿意，可以不发表书面声明。

**定制**

查看 odbconfig.py 文件来指定您的参数，因为游戏的真正名称是暴露您感兴趣的数据。我在配置文件中提供了一些例子。和他们一起玩！

您可以:

*   通过在配置文件中指定子字符串来指定要收集的索引或集合名称。例如，如果有术语“客户端”，脚本将拉索引称为“客户端”或“客户端数据”我建议您将这些列表留空，因为您永远不知道您关心的数据库将被调用，而是指定您关心的字段。
*   指定您关心的字段:如果您只想获取字段名称中包含“email”的 ES 索引，例如“user_emails”，您可以这样做。如果您想确保索引中至少有 2 个您关心的字段，您也可以这样做。或者，如果您只想获取所有内容，而不管其中有什么字段，您也可以这样做。
*   指定不需要的索引，例如系统索引名称和其他通常用于基本日志记录的索引。配置文件中提供了示例。
*   覆盖配置并获取服务器上的所有内容
*   指定输出(默认为 JSON，可以选择 CSV)
*   设置默认情况下数据库脚本将转储的最小和最大大小，您可以设置标记以根据具体情况覆盖最大文档数。

**安装及要求**

*   克隆或下载到机器
*   获取 Shodan 和/或 BinaryEdge 的 API 密钥
*   在 ODBconfig.py 文件中配置参数
*   从文件安装要求

我建议为 ODBParser 创建虚拟环境，这样就不会出现模块版本不正确的问题。**注:**仅在 Python 3.7.3 和 Windows 10 上测试。

**请负责任地使用**

**下一步措施和已知问题**

*   多清理一点代码
*   多线程各种进程。
*   扩展到其他数据库类型
*   添加其他开放目录搜索引擎(Zoomeye 等。)
*   由于 ES <2.0 works. Appreciate any help! **方式，无法滚动某些 ES 实例的第一页，很确定已修复此问题。如果出现 scrollid 错误，则打开问题**

**用途**

**示例:python odb parser . py-cn US-p 8080-t users–elastic–shod an–CSV–limit 100
python odb parser . py-IP 192 . 168 . 2:8080–mongo–ignorelogs–nosizelimits
迄今为止的损坏:解析了 0 个服务器|转储了 0 个数据库|拉出了 0 条记录
可选参数:
-h，–帮助显示此帮助消息并退出
查询选项:
–shod 指定 ES 或 MDB w/
标志。
–binary，-如果使用 BinaryEdge，则添加此标志。指定 ES 或 MDB
带标志。
–IP，-ip 查询一台服务器。添加类似 so '192.165.2.1:8080'
的端口，或者将为每种数据库类型使用默认端口。添加 ES 或
MDB 标志来指定解析器。
–file，-f 从文件中加载行分隔的 IPs。添加端口或者
将为每种数据库类型采用默认端口。添加 ES 或 MDB
标志来指定解析器。
–从剪贴板粘贴-v 查询分隔线 IP。添加端口或
将假定每个数据库类型的默认端口，例如 ES 的 9200
。添加 ES 或 MDB 标志以指定解析器。
Shodan/BinaryEdge 选项:
–limit，-l 每次查询的最大结果数。默认是
500。
–端口，-p 按端口过滤。
–国家，按国家过滤(两个字母的国家代码)。
–terms，-t 在此输入您想要的任何附加查询术语，例如
‘users’
Dump 选项:
–mongo，-mdb 用于 IP、Shodan、BinaryEdge &将方法粘贴到
指定的解析器。
–elastic，-es 用于将 IP、Shodan、BinaryEdge &粘贴方法到
指定的解析器。
–property JSON，-pj 如果想要输出正确的 JSON
文件，添加此标志。默认值是每行一个 JSON 字符串对象。
–数据库，-db 指定要抓取的数据库。For MDB 必须采用
格式格式‘db:collection’。与 IP arg & 'es'
或' mdb '标志
–Get all、-g 一起使用获取所有索引，而不管字段和
集合/索引名称(覆盖配置
文件中的选择)。
–ignore logs 连接到您已经签出的服务器。
–nosizelimits，-n 转储指数无论多大。默认最大单据
数量为 800，000。
–csv 将 JSON 转储文件动态转换为 CSV 格式。(将
JSON 文件放在备份文件夹中，以防
有转换问题)
CSV/后处理选项:
–convertToCSV，-c 事后将 JSON 文件或 JSON 转储的文件夹转换为 CSV
。在
当前工作目录
中输入完整路径或文件夹名称–如果在后处理过程中将 JSON 文件转换为
CSV 时遇到内存问题，则不使用。
–如果您的 JSON 转储文件
不是真正的 JSON 文件，而是从其他来源获得的行分隔的 JSON
对象，则使用–convertToCSV 标志。
–don tclean，-dc 选择当转换为
CSV 时是否要保留无用数据。有关更多信息，请参见文档。**

[Download](https://github.com/citcheese/ODBParser)