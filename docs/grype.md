# Grype:一个针对容器映像和文件系统的漏洞扫描器

> 原文：<https://kalilinuxtutorials.com/grype/>

[![Grype : A Vulnerability Scanner For Container Images And Filesystems](img/c4af71b1ffce777aa85fd886a0865165.png "Grype : A Vulnerability Scanner For Container Images And Filesystems")](https://1.bp.blogspot.com/-odsnuQ5BQZA/X5q6cnRaphI/AAAAAAAAH5g/hFVU7rcq-ggnVavEN22xqyP3afeDJjBCwCLcBGAsYHQ/s1281/grype.gif)

Grype 是一个针对容器映像和文件系统的漏洞扫描器。[轻松安装二进制](https://github.com/anchore/grype#installation)试试看。

![Grype : A Vulnerability Scanner For Container Images And Filesystems](img/c4af71b1ffce777aa85fd886a0865165.png "Grype : A Vulnerability Scanner For Container Images And Filesystems")

**特性**

*   扫描容器映像或文件系统的内容，查找已知的漏洞。
*   查找主要操作系统包的漏洞
    *   阿尔卑斯山的
    *   巴布克斯
    *   CentOS /红帽
    *   一种自由操作系统
    *   人的本质
*   查找特定语言包的漏洞
    *   鲁比(邦德勒)
    *   Java(罐子等)
    *   JavaScript(NPM/纱线)
    *   Python(鸡蛋/轮子)
    *   python pip/requirements . txt/setup . py 清单
*   支持 Docker 和 OCI 图像格式

如果您遇到问题，请使用问题跟踪器让我们知道[。](https://github.com/anchore/grype/issues)

**入门**

[安装二进制文件](https://github.com/anchore/grype#installation)，并确保`grype`在您的路径中可用。要扫描图像中的漏洞:

**grype <图像>**

上述命令扫描容器中可见的漏洞(即图像的压扁表示)。要将所有图像层的软件包括在漏洞扫描中，无论其是否出现在最终图像中，请提供`--scope all-layers`:

**grype <图像>–范围所有层**

Grype 可以扫描 Docker 以外的各种资源。

#扫描容器映像档案(来自` docker image save …`、` podman save …`或` skopeo copy `命令的结果)grype path/to/image . tar

#扫描目录 grype dir:path/to/dir

Grype 的输出格式也是可配置的:

**grype <图像> -o <格式>**

可用的`format`有:

*   **`json` :** 用这个从 Grype 那里获取尽可能多的信息！
*   **`cyclonedx` :** 符合 [CycloneDX 1.2](https://cyclonedx.org/) 规范的 XML 报表。
*   **`table` :** 一栏式汇总(默认)。

Grype 从公开发布的 [Anchore Feed 服务](https://ancho.re/v1/service/feeds)中提取了一个漏洞数据库。该数据库在每次扫描开始时更新，但也可以手动触发更新。

**grype 数据库更新**

**安装**

*   **推荐**

**#将最新版本安装到/usr/local/BIN curl-sSfL https://raw . githubusercontent . com/anchore/grype/main/install . sh | sh-s—-b/usr/local/BIN

#将特定版本安装到特定目录 curl-sSfL https://raw . githubusercontent . com/anchore/grype/main/install . sh | sh-s—-b<SOME _ BIN _ PATH><RELEASE _ VERSION>**

*   **苹果电脑**

brew tap anchore/grype
brew install grype

运行 Grype 时，您可能会遇到“macOS 无法验证应用程序没有恶意软件”的错误，因为它尚未签名和公证。您可以使用`xattr`来覆盖它。

**xattr-rd com . apple . quarantine grype**

**外壳完成**

Grype 通过其 CLI 实现( [cobra](https://github.com/spf13/cobra/blob/master/shell_completions.md) )提供 shell 完成。通过运行以下命令之一，为您的 shell 生成完成代码:

*   **T2`grype completion <bash|fish>`**
*   **T2`go run main.go completion <bash|fish>`**

这将向 STDOUT 输出一个 shell 脚本，然后可以用作 Grype 的完成脚本。运行带有`-h`或`--help`标志的上述命令之一，将为您选择的 shell 提供如何执行该操作的说明。

注意: [Cobra 还没有发布完全的 ZSH 支持](https://github.com/spf13/cobra/issues/1226)，但是一旦发布，我们会在这里添加它！

**配置**

配置搜索路径:

*   **T2`.grype.yaml`**
*   **T2`.grype/config.yaml`**
*   **T2`~/.grype.yaml`**
*   **T2`<XDG_CONFIG_HOME>/grype/config.yaml`**

配置选项(示例值为默认值):

**#启用/禁用启动时检查应用程序更新**
检查应用程序更新:true

**#与-fail-on 相同；扫描时，如果发现严重性等于或高于#给定的严重性，则返回代码将为 1**
默认值为未设置，将跳过此验证(选项:可忽略、低、中、高、严重)
失败-严重:“

**”#与-o 相同；漏洞报告的输出格式(选项:table、json、cyclonedx)**
输出:“table”

**【同-s；寻找包的搜索空间(选项:所有层，压扁)**
范围:“压扁”

**#同-q；抑制所有输出(漏洞列表除外)**
quiet:false

**db:
#执行时检查数据库更新**
auto-update:true

**#位置写入漏洞数据库缓存**
CACHE-dir:" $ XDG _ CACHE _ HOME/grype/db "

**#漏洞数据库的 URL**
update-URL:" https:/"注意:详细日志记录抑制 ETUI
级别:“错误”
**#使用结构化日志记录**
结构化:false，

**未来计划**

目前正在调查以下潜在发展领域:

*   支持允许列表、包映射
*   建立稳定的交换格式 w/Syft
*   接受 SBOM (CycloneDX，Syft)作为输入，而不是图像/目录

[**Download**](https://github.com/anchore/grype)