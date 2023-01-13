# Fennec:用于*Nix 系统的工件收集工具

> 原文：<https://kalilinuxtutorials.com/fennec-artifact-collection-tool-for-nix-systems/>

[![](img/db2616bb2f1a491f02a2e6870cfd105d.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjub1y5LqZMGWxm4r8KtCLfscaBWupnpfWp6Z1364kdFLoS2KkxvjrbZHKFs7Yw3DHO3GjgjOxvYv8oKoAy1nCSSwZIf0tuokXPoeMoR288QsGVWwUFBv6ctVPz1DfO96KbEIWkS_UbDTwN43NfilEcOdNCOs6NGeLlKdo_E2r0lZeAe6DS-KaQ-BnN/s728/fennec_logo%20(1).png)

**Fennec** 是一个用 Rust 编写的工件收集工具，在基于*nix 的系统上进行事件响应时使用。fennec 允许您编写一个包含如何收集工件的配置文件。

## 特性

*   单个静态编译的二进制文件
*   执行任何 osquery SQL 查询
*   执行系统命令
*   使用正则表达式解析任何文本文件
*   收集系统日志和文件的能力
*   以结构化方式返回数据
*   支持多种输出格式(JSONL，CSV 和 KJSON)
*   灵活的配置文件
*   直接写入 ZIP 文件以节省空间
*   非常快！

## 测试

| 操作系统详细信息 | 体系结构 | 成功？ | 细节 |
| --- | --- | --- | --- |
| ubuntu 20 . 04 . 3 lts | x86_64 | 981 号房 |  |
| Ubuntu 19.04 | x86_64 | 981 号房 |  |
| ubuntu 18 . 04 . 6 lts | x86_64 | 981 号房 |  |
| Ubuntu 17.04 | x86_64 | 981 号房 |  |
| ubuntu 16 . 04 . 7 lts | x86_64 | 981 号房 |  |
| Ubuntu 15.10 | x86_64 | 981 号房 |  |
| ubuntu 14 . 04 . 6 lts | x86_64 | 981 号房 |  |
| Ubuntu 13.04 | x86_64 | 981 号房 |  |
| ubuntu 12 . 04 . 5 lts | x86_64 | 981 号房 |  |
| 2105 年 4 月 8 日 | x86_64 | 981 号房 |  |
| 2009 年 9 月 7 日 | x86_64 | 981 号房 |  |
| 厘斯 6.10 | x86_64 | 981 号房 |  |
| CentOS 5.11 | x86_64 | -好的 | osquery 要求 libc >= 2.12 |
| Ubuntu 20.04 | aarh64 足球俱乐部 | 981 号房 |  |
| 马科斯蒙特雷 v12.0.1 | x86_64 | 981 号房 |  |

## 用法

**fennec 0.1.0
阿卜杜勒拉赫曼阿尔法伊菲 aalfaifi@u0041.co
适用于*nix 系统的 Aritfact 收集工具
用法:
Fennec _ x86 _ 64-unknown-Linux-GNU【选项】
选项:
-c，–config 设置自定义配置文件
-f，–log-file 设置日志文件名【默认:Fennec . log】
-h，–help 打印帮助信息
-l，–日志级/osqueryd]
–output-format 设置输出格式[默认值:jsonl][可能值:jsonl，
csv，kjson]
-q，–quiet 不将日志打印到 stdout
–Show-config 显示嵌入式配置文件
-V，–version 打印版本信息**

*   **`-c`、`--config`** :使用指定的配置文件，不使用嵌入式配置
*   **`-f`、`--log-file`** :更改日志文件的默认名称(默认:`**fennec.log**`)
*   **`-h`、`--help`** :打印帮助信息
*   **`-l`、`--log-level`** :更改默认日志级别(默认:`**info**`)
*   **`-o`，`--output`** :更改 zip 文件的默认输出文件名(默认: **`{HOSTNAME}.zip`** ，其中主机名是运行时评估的机器主机名)
*   `**--osquery-path**`:osquery 可执行文件的路径，将根据以下条件使用该值:
    *   如果 osquery 二进制嵌入到`**fennec**`中，那么提取它并转储到`**--osquery-path**`
    *   如果 osquery 没有嵌入到`**fennec**`中，那么使用路径`**--osquery-path**`中的 osquery 二进制文件
*   `**--output-format**`:选择输出格式，支持的格式:
    *   jsonl:一个新的行分隔 JSON 对象(默认)
    *   csv:逗号分隔值
    *   kjson:如果您想将结果文件上传到 Kuiper 分析平台，请使用这种格式。
*   **`-q`、`--quiet`** :不打印日志到`**stdout**`
*   `**--show-config**`:打印嵌入式配置，然后退出
*   **`-V`，`--version`** :打印`**fennec**`版本然后退出

## 使用依赖项编译

fennec 依赖于`**osquery**`来运行类型为`**query**`的工件。名为`**deps**`的目录包含将根据目标操作系统和架构嵌入到二进制文件中的文件，在编译之前请遵循以下步骤:

*   根据需要修改配置文件`**deps/<TARGET_OS>/config.yaml**`
*   使用以下命令之一构建二进制文件:
    *   动态链接:

**货物建造-发布**

静态链接(编译所有依赖项):

**rust flags = "-C target-feature =+CRT-static " cargo build–release–target x86 _ 64-unknown-Linux-GNU**

## 例子

### 默认配置

以下是在本报告中使用相同配置在`**Ubuntu 20**`上运行的示例:

### 将 Fennec 与 Kuiper 一起使用

要将数据输出到 Kuiper 支持的格式，请使用以下参数执行 Fennec:

**须藤。/Fennec–输出格式 kjson**

或者将以下内容添加到配置中的`**args**`部分:

**参数:
"–输出格式"
"kjson"**

重新编译然后执行:

**须藤。/fennec**

然后将生成的 zip 文件上传到 Kuiper，下面是一个例子:

## 配置

默认情况下，路径`**deps/config.yaml**`中的配置将在编译期间嵌入到可执行文件中。该配置采用 YAML 格式，包含两个部分:

### 参数

包含作为命令行参数传递给可执行文件的参数列表，下面是一个关于`**args**`部分的示例，它将输出格式设置为`**jsonl**`，并将日志文件名设置为`**fennec.log**`:

**参数:
"–输出格式"
" jsonl "
"–日志文件"
"fennec.log"**

命令行参数将按以下优先级使用:

*   传递给可执行文件的参数
*   配置文件中的参数
*   默认参数

### 神器

包含要收集的工件列表。每个工件包含以下字段:

*   名称:工件的名称，工件的结果将以这个名称写入文件
*   类型:工件的类型，支持的工件有:
    *   询问
    *   收藏品
    *   命令
    *   从语法上分析
*   描述(**可选**):包含工件的描述
*   查询**或**路径**或**命令:查询工件类型是否为**查询**并且是否包含 osquery SQL 查询列表。如果工件类型是 collection **或** parse，并且它包含一个路径列表。如果工件类型为**命令**并且包含命令列表，则命令。这些名称是为了可读性，您可以在任何工件类型中使用它们中的任何一个。
*   regex:该字段仅在使用工件类型 **parse** 时使用，该字段包含用于解析文本文件的 regex
*   maps ( **可选的**):包含一个映射器列表，用于修改键名称和格式值，查看 maps 部分了解更多细节

#### 神器类型:查询

执行 osquery SQL 查询。以下示例工件检索系统上的所有用户:

**神器:
名称:用户
类型:查询
描述:“列出所有本地用户”
查询:
' select * from groups join user _ groups using(GID)join users using(uid)'**

#### 工件类型:集合

这个工件类型收集在字段**路径**中指定的文件/文件夹。以下是这种收集系统日志的工件类型的示例:

**工件:
名称:日志
类型:收集
描述:“收集系统日志”
路径:
'/var/log/* */* '**

#### 工件类型:命令

使用 shell 命令解释器按以下优先级执行系统命令:

*   **$SHELL** 环境变量
*   **/bin/bash**
*   **/bin/sh**

这是检索错误登录这种工件类型的一个示例:

**神器:
名称:bad_logins
类型:命令
描述:“获取失败的登录(/var/log/btmp)”
命令:
' lastb–time-format = iso '**

#### 工件类型:解析

这种工件类型提供了使用 regex 解析文本文件并以结构化格式返回数据的能力。下面的示例解析 nginx 访问日志，并以结构化格式返回结果:

**artifcats:
名称:nginx_access
类型:parse
描述:“nginx 访问日志”
路径:
–/var/log/Nginx/access。*
regex:'(？P[0-9]{1，3}。[0-9]{1,3}.[0-9]{1,3}.[0-9]{1,3}) – (?P[^ ]+) [(？p[0-9]{ 2 }/[a-zA-Z]{ 3 }/[0-9]{ 4 }:[0-9]{ 2 }:[0-9]{ 2 }:[0-9]{ 2 }+[0-9]{ 4 })]"(？P[A-Z]+)？[ ]?(?P. *？)[ ]?(HTTP/(？P[0-9。]+))?"(?P[0-9]{3})(？P[0-9]+)"(？P.* ？)" "(?P.*？)" '**

该配置将逐行读取路径`**/var/log/nginx/access.***`中的文件，并运行正则表达式来提取字段。这个工件还检查文件是否是用于压缩旧日志以节省空间的`**gzip**`格式，并对它们进行解压缩和解析。正则表达式应该是 rust 正则表达式库中记录的**命名的 captures** 格式。以下是解析前后的 nginx 访问记录示例:

*   原始记录
*   **192 . 168 . 133 . 70—[23/Jan/2022:19:14:37+0000]" GET/blog/HTTP/1.1 " 200 2497 " https://u 0041 . co/" " Mozilla/5.0(X11；Linux x86 _ 64rv:78.0)壁虎/20100101 火狐/78.0"**

已解析记录

**{
"c_ip": "192.168.133.70 "，
"remote_user": "-"，
" time ":" 23/Jan/2022:19:14:37+0000 "，
"method": "GET "，
"uri": "/blog/"，
"http_prot": "1.1 "，
" status _ code ":" 2000 "Linux x86 _ 64RV:78.0)Gecko/2010 01 01 Firefox/78.0 "，
" full _ path ":"/var/log/nginx/access . log . 9 . gz "
}**

### 地图

此可选字段可用于更改结果字段名称，并对字段值运行称为修饰符的后处理。下面的示例将显示不带映射的 nginx 访问记录的解析结果:

*   工件配置:

**artifcats:
名称:nginx_access
类型:parse
描述:“nginx 访问日志”
路径:
/var/log/nginx/access。*
regex:'(？P[0-9]{1，3}。[0-9]{1,3}.[0-9]{1,3}.[0-9]{1,3}) – (?P[^ ]+) [(？p[0-9]{ 2 }/[a-zA-Z]{ 3 }/[0-9]{ 4 }:[0-9]{ 2 }:[0-9]{ 2 }:[0-9]{ 2 }+[0-9]{ 4 })]"(？P[A-Z]+)？[ ]?(?P. *？)[ ]?(HTTP/(？P[0-9。]+))?"(?P[0-9]{3})(？P[0-9]+)"(？P.* ？)" "(?P.*？)" '**

#### 修饰语

modifiers 提供对工件结果的字段值的后处理。例如重新格式化日期和时间。继续上面的例子，我们可以将字段`**@timestamp**`中的日期和时间格式更改为格式`**%Y**-**%m-%d %H:%M:%S**`。我们可以向工件配置中添加以下内容来实现这一点:

**工件:
名称:nginx_access
类型:解析
描述:“nginx 访问日志”
路径:
/var/log/nginx/access。*
regex:'(？P[0-9]{1，3}。[0-9]{1,3}.[0-9]{1,3}.[0-9]{1,3}) – (?P[^ ]+) [(？p[0-9]{ 2 }/[a-zA-Z]{ 3 }/[0-9]{ 4 }:[0-9]{ 2 }:[0-9]{ 2 }:[0-9]{ 2 }+[0-9]{ 4 })]"(？P[A-Z]+)？[ ]?(?P. *？)[ ]?(HTTP/(？P[0-9。]+))?"(?P[0-9]{3})(？P[0-9]+)"(？P.* ？)" "(?P.*？)" '
映射:
从:时间
到:" @timestamp"
修饰符:
名称:datetime_to_iso
参数:
input _ time _ format:' % d/% b/% Y:% H:% M:% S % z '
output _ time _ format:' % Y-% M-% d % H:% M:% S '**

可用的修改器有:

| 名字 | 细节 | 输入时间格式 | 输出时间格式 |
| --- | --- | --- | --- |
| 历元至 iso | 将纪元时间戳转换为自定义日期和时间格式 | 不适用的 | 指定输出日期和时间格式，默认为`**%Y-%m-%d %H:%M:%S**` |
| 日期时间到 iso | 将日期和时间从格式`**input_time_format**`重新格式化为格式`**output_time_format**` | 指定输入日期和时间格式 | 指定输出日期和时间格式，默认为`**%Y-%m-%d %H:%M:%S**` |
| 无年至 iso 的时间 | 将没有年份数据的日期和时间从格式`**input_time_format**`格式化为格式`**output_time_format**` | 指定输入日期和时间格式 | 指定输出日期和时间格式，默认为`**%Y-%m-%d %H:%M:%S**` |

`**time_without_year_to_iso**`修改器的工作方式如下:

*   添加当前年份，然后检查解析器时间是否
*   否则就是前一年

此修饰符假设日志仅针对**一年**，请谨慎使用此修饰符

[**Download**](https://github.com/AbdulRhmanAlfaifi/Fennec)