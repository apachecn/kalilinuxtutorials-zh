# ChopChop : ChopChop 是一个 CLI，帮助开发人员扫描端点并识别敏感服务/文件/文件夹的公开

> 原文：<https://kalilinuxtutorials.com/chopchop/>

[![](img/f4f34d2ec0e33f81e70095d307297e9e.png)](https://blogger.googleusercontent.com/img/a/AVvXsEh50DCgqK0naaCW18H5az73kVwOCFvZZLxuOTc7MRtIn_FezMS5tQh1HDKbepw_0nqFTXjl0W2nL9kcK5dx0aRZbHdGoxiA4wQPe53rw23ngiyZGpuJ4qwkb5hg6lDkJkpHccN8rDf-Bfh_AMA6Bcdhlp7V0ZWdVwyFGs2fIvabqHymGwFYL1HJ11zX=s469)

ChopChop 是一个命令行工具，用于对 web 应用程序进行动态安全测试，最初由米其林证书编写。

它的目标是扫描几个端点，并通过 webroot 识别服务/文件/文件夹的公开。检查/签名在一个配置文件中声明(默认:`**chopchop.yml**`)，完全可配置，尤其是由开发人员。

**大楼**

我们试图让构建过程变得轻松，希望它能像以下这样简单:

**$ go mod 下载
$ go 构建。**

文件夹中应该有一个结果`**gochopchop**`二进制文件。

**使用档案号** r

感谢 Github 容器注册表，我们能够为您提供一些新构建的 Docker 图像！

**码头运行 ghcr . io/Michelin/gochop 扫描 https://** foobar.com -v 调试

但是如果您愿意，您也可以在本地构建它，见下文:

**本地建造**

docker build -t gochopc hop。

**用途**

我们一直在努力让`**goChopChop**`变得尽可能简单。使用该实用程序扫描主机非常简单:

**$ ./gochopchop scan https://foobar.co** m

**使用 Docker**

**坞站运行 gochop 扫描 https://foobar.com**

**自定义配置文件**

**坞站运行-v ./:/app 斩波扫描-c/app/斩波. yml h** ttps://foobar.com

**下一步是什么**

Golang 的重写发生在几个月前，但仍有许多工作要做。以下是我们计划集成的一些功能:[x]线程化以获得更好的性能[x]指定并发线程数量的能力[x]颜色和更好的格式化[x]过滤检查/签名以搜索[x]模拟和单元测试的能力[x] Github CI 等等！

**测试**

为了快速地端到端测试 chopchop，我们在`**tests/server.go**`中提供了一个 web 服务器。要尝试一下，请运行`**go run** **tests/server.go**`，然后用下面的命令`**./gochopchop scan http://localhost:8000 --verbosity Debug**`运行 chopchop。ChopChop 应该打印“未发现漏洞”。

您也可以使用`**go test -v ./...**`启动单元测试。这些测试集成在 github CI 工作流中。

**可用旗帜**

您可以找到可用于`scan`命令的可用标志:

| 旗 | 满旗 | 描述 |
| --- | --- | --- |
| `**-h**` | `**--help**` | 帮助向导 |
| `**-v**` | `**--verbosity**` | 日志记录的详细级别 |
| `**-c**` | `**--signature**` | 自定义签名文件的路径 |
| `**-k**` | `**--insecure**` | 禁用 SSL 验证 |
| `**-u**` | `**--url-file**` | 包含要测试的 URL 的指定文件的路径 |
| `**-b**` | `-**-max-severity**` | 如果严重性超过或等于指定标志，则阻止 CI 管道 |
| `**-e**` | `**--export**` | 输出的导出类型(csv 和/或 json) |
|  | `**--export-filename**` | 指定导出文件的文件名 |
| `**-t**` | `**--timeout**` | HTTP 请求超时 |
|  | `**--severity-filter**` | 按严重性过滤插件 |
|  | `**--plugin-filter**` | 按插件名称过滤插件 |
|  | `**--threads**` | 并发线程数 |

**高级用法**

以下是您可能感兴趣的高级用法列表。注意:可以使用类似`>`的用于后处理的重定向器。

*   扫描和禁用 SSL 验证的能力

**$。/gochopchop 扫描 https://foobar.com-不安全**

能够使用自定义配置文件(包括自定义插件)进行扫描

**$。/gochopchop 扫描 https://foobar.com–不安全–签名 test_config.yml**

能够列出所有插件或按严重性:`**plugins**`或`**plugins --severity High**`

**$。/gochopchop 插件–严重性高**

能够为 4 个工作线程指定并发线程的数量:`**--threads 4**`

**$。/gochopchop 插件–线程** s 4

根据严重级别(等于或超过指定的严重级别)阻止 CI 管道的能力:`**--max-severity Medium**`

**$。/gochopchop 扫描 https://foobar.com-最高-中等严重程度**

能够指定要检查的特定签名

**。/gochopchop 扫描 https://foobar.com–超时 1–详细度–导出=csv，JSON–导出-文件名 boo–插件-过滤器=Git，Zimbra，Jenkins**

能够列出所有插件

**$。/gochopchop 插件**

列出高严重性插件

**$。/gochopchop 插件–严重性高**

设置位于文件中的列表或 URL

**$。/gochopchop scan–URL-file URL _ file . txt**

以 CSV 和 JSON 格式导出 GoChopChop 结果

**$。/gochopchop 扫描 https://foobar.com–export = CSV，JSON–export-filename 结果**

**创建新支票**

开一张新支票很简单:

**端点:"/。git/config"
检查:
名称:Git exposed
匹配:
【分支】
补救:不部署。生产服务器上的 git 文件夹
描述:验证可以从站点
访问 GIT 存储库严重性:“Hig** h”

端点(例如`**/.git/config**`)被映射到多个检查，这避免了发送 X 个检查的 X 个请求。可以通过一个 HTTP 请求进行多次检查。每张支票都需要这些字段:

| 属性 | 类型 | 描述 | 可选？ | 例子 |
| --- | --- | --- | --- | --- |
| 名字 | 线 | 支票的名称 | 不 | Git 暴露 |
| 描述 | 线 | 支票的简短描述 | 不 | 确保。无法从 webroot 访问 git 存储库 |
| 补救 | 线 | 针对此特定“问题”提供补救措施 | 不 | 不要部署。生产服务器上的 git 文件夹 |
| 严重 | 枚举(“高”、“中”、“低”、“信息”) | 如果批评在你的环境中引发，请对其进行评级 | 不 | 高的 |
| 状态代码 | 整数 | 应该返回的 HTTP 状态代码 | 是 | Two hundred |
| 头球 | 字符串列表 | HTTP 响应中应该包含的标头列表 | 是 | 不适用的 |
| 无标题 | 字符串列表 | HTTP 响应中不应出现的标头列表 | 是 | 不适用的 |
| 比赛 | 字符串列表 | 列出 HTTP 响应中应该包含的字符串 | 是 | "[分支机构] |
| 不匹配 | 字符串列表 | 列出不应出现在 HTTP 响应中的字符串 | 是 | 不适用的 |
| 查询字符串 | 获取必须传递给端点的参数 | 线 | 是 | `**query_string: "id=FOO-chopchoptest"**` |

**外部库**

| 库名 | 环 | 许可证 |
| --- | --- | --- |
| 毒蛇 | https://github.com/spf13/viper | 带许可证 |
| 去-漂亮 | https://github.com/jedib0t/go-pretty | 带许可证 |
| 眼镜蛇 | https://github.com/spf13/cobra | Apache 许可证 2.0 |
| strfmt | https://github.com/go-openapi/strfmt | Apache 许可证 2.0 |
| Go-homedir | https://github.com/mitchellh/go-homedir | 带许可证 |
| pkg 错误 | https://github.com/pkg/errors | BSD 2(简化许可证) |
| Go-runewidth | https://github.com/mattn/go-runewidth | 带许可证 |

更多信息请参考`**third-party.txt**`文件。

[**Download**](https://github.com/michelin/ChopChop)