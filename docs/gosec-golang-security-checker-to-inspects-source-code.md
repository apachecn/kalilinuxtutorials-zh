# Gosec : Golang 安全检查器检查源代码

> 原文：<https://kalilinuxtutorials.com/gosec-golang-security-checker-to-inspects-source-code/>

[![Gosec : Golang Security Checker To Inspects Source Code](img/eed613d935ed18236e9573ab54f5ea56.png "Gosec : Golang Security Checker To Inspects Source Code")](https://1.bp.blogspot.com/-ZZPJMrMzHfw/Xb7sGIrjFDI/AAAAAAAADO8/Y5j4LIaL9I8es7IZP7tgZfI18gdsfILNQCLcBGAsYHQ/s1600/Gosec%2B%25281%2529.png)

Gosec 是一个通过扫描 Go AST 来检查源代码安全问题的工具。根据 Apache 许可证 2.0 版许可(“许可证”)。除非符合许可证的规定，否则您不得使用本文件。你可以在这里获得[执照的副本。](http://www.apache.org/licenses/LICENSE-2.0)

**安装**

**CI 安装**

**# binary 将$ GOPATH/bin/gosec**
curl-sfL https://raw . githubusercontent . com/securego/gosec/master/install . sh | sh-s—-b $ GOPATH/bin vX。Y.Z

**#或者安装成。/bin/**curl-sfL https://raw . githubusercontent . com/securego/gosec/master/install . sh | sh-s vX。Y.Z

**#在 alpine linux 中(因为默认没有附带 curl)**
wget-O –- q https://raw . githubusercontent . com/securego/gosec/master/install . sh | sh-s vX。Y.Z

**#如果你想使用“发布”页面提供的校验和
#那么你必须为你的操作系统下载一个 tar.gz 文件**而不是二进制文件
wget https://github.com/securego/gosec/releases/download/vX.Y.Z/gosec_vX。y . Z _ OS . tar . gz

**#该文件将位于您运行命令
#的当前文件夹中，您可以像这样检查校验和**
echo " gosec_vX。y . Z _ OS . tar . gz " | sha 256 sum-c–
gosec–帮助

**本地安装**

去找 github.com/securego/gosec/cmd/gosec

**用途**

Gosec 可以配置为只运行规则的子集，排除某些文件路径，并生成不同格式的报告。默认情况下，所有规则都将针对提供的输入文件运行。要从当前目录递归扫描，你可以提供`**./...**`作为输入参数。

**可用规则**

*   G101:查找硬编码的凭据
*   G102:绑定到所有接口
*   G103:审核不安全块的使用
*   G104:未检查审计错误
*   G106:审核 ssh 的使用。InsecureIgnoreHostKey
*   G107:作为污点输入提供给 HTTP 请求的 Url
*   G108:在/debug/pprof 上自动公开的分析端点
*   G201:使用格式字符串的 SQL 查询构造
*   G202:使用字符串连接的 SQL 查询构造
*   G203:在 HTML 模板中使用非转义数据
*   G204:审核命令执行的使用
*   G301:创建目录时使用了较差的文件权限
*   g302:chmod 使用的文件权限差
*   G303:使用可预测的路径创建临时文件
*   G304:作为污点输入提供的文件路径
*   G305:解压缩 zip 存档文件时的文件遍历
*   G401:检测 DES、RC4、MD5 或 SHA1 的使用情况
*   G402:查找错误的 TLS 连接设置
*   G403:确保最小 RSA 密钥长度为 2048 位
*   G404:不安全的随机数源(rand)
*   G501:导入黑名单:crypto/md5
*   G502:导入黑名单:加密/解密
*   G503:导入黑名单:crypto/rc4
*   G504:导入黑名单:net/http/cgi
*   G505:导入黑名单:crypto/sha1

**退役规则**

*   G105:审核 math/big 的使用。CVE 是固定的

**选择规则**

默认情况下，gosec 将根据提供的文件路径运行所有规则。然而，可以通过`**-include=**`标志选择要运行的规则子集，或者使用`**-exclude=**`标志指定一组要明确排除的规则。

**#运行一组特定的规则
$ gosec -include=G101，G203，G401。/…

#运行除规则 G303
$ gosec -exclude=G303 之外的所有内容。/…**

**CWE 制图**

由`gosec`检测到的每个问题都被映射到一个 [CWE(通用弱点枚举)](http://cwe.mitre.org/data/index.html)，后者以更通用的术语描述了该弱点。确切的映射可以在这里找到[。](https://github.com/securego/gosec/blob/53be8dd8644ee48802114178cff6eb7e29757414/issue.go#L49)

**配置**

配置文件中可以提供许多全局设置，如下所示:

**{
“全局”:{
“nosec”:“已启用”，
“审计”:“已启用”
}
}**

*   `**nosec**`:该设置将覆盖整个代码库中定义的所有`**#nosec**`指令
*   `audit`:在审计模式下运行，这种模式支持额外的检查，对于正常的代码分析来说，这可能太多管闲事了

**#使用全局配置文件
$ gosec -conf config.json 运行。**

还有一些规则接受配置。例如，在规则`G104`上，可以定义包以及在审计未检查错误时将被跳过的功能列表:

 **【g104】:
【io/ioutil】:【write file】
}
}**

**依赖关系**

当 go 模块打开时，gosec 将自动获取正在分析的代码的相关性(例如`** GO111MODULE=on**`)。如果不是这种情况，则需要在扫描之前通过运行`**go get -d**`命令显式下载依赖项。

**排除测试文件&文件夹**

gosec 将忽略所有软件包中的测试文件以及您的供应商目录中的任何依赖项。

可以使用以下标志启用测试文件的扫描:

gosec 测试。/…

此外，还可以排除其他文件夹，如下所示:

**gosec-exclude-dir = rules-exclude-dir = cmd。/…**

### 注释代码

与所有自动检测工具一样，也会有误报的情况。如果 gosec 报告了一个已经被手动验证为安全的故障，可以用`#nosec`注释对代码进行注释。

注释导致 gosec 停止处理 AST 中的任何其他节点，因此可以应用于整个块，或者更细粒度地应用于单个表达式。

**导入" MD5 "//# nosec

func main(){
/* # nosec */
if x>y {
h:= MD5。New() //这个也会被忽略
}
}**

当某个特定的误报被识别并确认为安全时，您可能希望在一段代码中仅隐藏该单个规则(或一组特定的规则)，同时继续扫描其他问题。为此，您可以在`**#nosec**`注释中列出要隐藏的规则，例如:`**/* #nosec G401 */**` **或** `**// #nosec G201 G202 G203**`

在某些情况下，您可能还想重访使用过`#nosec`注释的地方。要运行扫描仪并忽略任何`#nosec`注释，您可以执行以下操作:

gosec -nosec=true。/…

**建立标签**

gosec 能够将您的 [Go build 标签](https://golang.org/pkg/go/build/)传递给分析器。它们可以以逗号分隔的列表形式提供，如下所示:

gosec-标记调试，忽略。/…

**输出格式**

gosec 目前支持 text、json、yaml、csv、sonarqube 和 JUnit XML 输出格式。默认情况下，结果将报告给 stdout，但也可以写入输出文件。输出格式由'-fmt '标志控制，输出文件由'-out '标志控制，如下所示:

**#将 json 格式的输出写入 results . JSON
$ gosec-fmt = JSON-out = results . JSON *。去**

**发展**

**打造**

**制作**

**测试**

**进行测试**

**发布构建**

确保您已经安装了 [goreleaser](https://github.com/goreleaser/goreleaser) 工具，然后您可以按如下方式发布 gosec:

**git tag v 1 . 0 . 0
export GITHUB _ TOKEN =<YOUR GITHUB TOKEN>
make release**

该工具的发布版本可在`dist`文件夹中获得。构建信息应该显示在用法文本中。

**。/dist/Darwin _ amd64/gosec-h
gosec–Golang 安全检查器

gosec 分析 Go 源代码寻找常见编程错误

版本:1.0.0
GIT 标签:v1.0.0
构建日期:2018-04-27T12:41:38Z**

请注意，所有已发布的档案也会上传到 GitHub。

**码头工人图像**

您可以按如下方式构建 docker 映像:

**制作图像**

您可以在本地 Go 项目的容器中运行`gosec`工具。您只需将项目装入卷中，如下所示:

**docker run -it -v <你的项目路径> / <项目> :/ <项目> securego/gosec / <项目> /…**

**生成 TLS 规则**

TLS 规则的配置可以从 [Mozilla 的 TLS ciphers 推荐](https://statics.tls.security.mozilla.org/server-side-tls-conf.json)中生成。

首先，您需要安装生成器工具:

去找 github.com/securego/gosec/cmd/tlsconfig/…

您现在可以调用项目根中的`go generate`:

**去生成。/…**

这将生成`**rules/tls_config.go**`文件，其中包含 Mozilla 推荐的当前密码。

[**Download**](https://github.com/securego/gosec)