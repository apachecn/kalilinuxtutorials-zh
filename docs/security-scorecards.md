# 安全记分卡:开放源代码的安全健康指标

> 原文：<https://kalilinuxtutorials.com/security-scorecards/>

[![Security Scorecards : Security Health Metrics For Open Source](img/bb702c7ee1ce9f1c9476cf3cac80b160.png "Security Scorecards : Security Health Metrics For Open Source")](https://1.bp.blogspot.com/-NOe9-YIehuk/YOp6-6s5iTI/AAAAAAAAJ9M/Ct-in2bnHqgZWbWz_sjn7HfcB7vH6o6tQCLcBGAsYHQ/s728/openssf_security%2B%25281%2529.png)

**安全记分卡**是一个开源的安全健康度量工具。

**动机**

一个简短的激励视频剪辑来激励我们:https://youtu.be/rDMMYT3vkTk“你通过了！全是 D…还有一个 A！”

**目标**

*   对开源项目的安全状况进行自动化分析和信任决策。
*   使用这些数据来主动改善世界所依赖的关键项目的安全状况。

**记分卡检查**

默认情况下，以下检查都针对目标项目运行:

| 名字 | 描述 |
| --- | --- |
| 活跃的 | 该项目在过去 90 天内有没有收到任何提交？ |
| 自动依赖关系更新 | 项目是否使用工具来自动更新其依赖项？ |
| 二元伪影 | 项目没有签入的二进制文件吗？ |
| 分支保护 | 项目是否使用分支保护？ |
| CI 测试 | 项目是否在 CI 中运行测试，例如 GitHub Actions、Prow？ |
| CII 最佳实践 | 该项目有 CII 最佳实践徽章吗？ |
| 代码审查 | 在代码合并之前，项目需要代码审查吗？ |
| 贡献者 | 项目是否有来自至少两个不同组织的参与者？ |
| 起毛 | 该项目是否使用模糊工具，如 OSS-模糊？ |
| 冷冻 Deps | 项目是否声明并冻结依赖项？ |
| 包装 | 项目是否从 CI/CD 构建并发布官方包，例如 GitHub Publishing？ |
| 拉式请求 | 项目是否对所有代码变更使用拉请求？ |
| SAST | 项目是否使用静态代码分析工具，例如 CodeQL、SonarCloud？ |
| 安全政策 | 项目是否包含安全策略？ |
| 签名发布 | 项目是否对发布进行加密签名？ |
| 带符号的标签 | 项目是否对发布标签进行加密签名？ |
| 令牌-权限 | 项目是否将 GitHub 工作流令牌声明为只读？ |
| 脆弱点 | 项目是否有未修复的漏洞？使用 OSV 服务。 |

要查看每个检查和补救步骤的详细信息，请查看检查文档页面。

**检查文档**

此页面包含有关每个检查如何工作的信息，并提供修复失败的补救步骤。目前，所有这些检查基本上都是“最佳猜测”,并基于一组试探法进行操作。

它们都是可以改变的，都有改进的空间！如果您有添加内容的想法，或者检测内容的新方法，请投稿！

**激活**

不活动的项目可能没有被修补，可能没有其依赖项被修补，或者可能没有被积极地测试和使用。所以这个检查试图确定项目是否仍然是“积极维护的”。它目前通过查找最近 90 天内的提交来工作，如果在最近 90 天内至少有 2 个提交，则成功。

**补救步骤**

*   这里不需要*任何*修复工作。这只是表明您的项目活动和维护承诺。

**自动依赖关系更新**

该检查尝试确定项目是否具有自动更新的依赖项。检查寻找依赖机器人或更新机器人。此检查仅查看它是否已启用，并不确保它正在运行，也不确保纳入请求。

**补救步骤**

*   使用 dependabot 或 renovatebot 注册自动依赖项更新，并将配置文件放在这些工具推荐的位置。

**二进制工件**

该检查试图确定项目在源存储库中是否有二进制工件。这些二进制文件可能是受损的藏物。建议从源代码开始构建。

**补救步骤**

*   从存储库中删除二进制工件。

**分支保护**

分支保护允许定义规则来强制分支的某些工作流，例如要求审查或通过某些状态检查。仅当令牌对存储库具有管理员访问权限时，此检查才有效。该检查确定默认和发布分支是否受保护。更具体地说，对允许强制推送(禁用)、允许删除(禁用)、强制管理(启用)、要求线性历史(启用)、要求状态检查(启用且必须启用非空上下文)、要求拉取请求审查(> =1)、消除过时审查(启用)、要求代码所有者审查(启用)的检查。

**补救步骤**

*   在您的源主机提供商中启用分支保护设置，以避免强制推送或删除您的重要分支。
*   对于 GitHub，查看这里的步骤。

**CI 测试**

该检查尝试确定项目是否在合并请求之前运行测试。它的工作原理是在 GitHub 的`**CheckRuns**`和 **`Statuses`** 中寻找最近提交的一组众所周知的 CI 系统名称(~30)。如果一个 CI 系统的名称包含以下任何一个，它就被认为是众所周知的:appveyor、buildkite、circleci、e2e、github-actions、jenkins、mergeable、test、travis-ci。如果至少 75%的成功拉取请求至少有一个相关联的成功检查，则检查成功。

**补救步骤**

*   运行存储库中所有测试的签入脚本。
*   将这些脚本与 CI/CD 平台集成，在每个拉请求(例如 GitHub 操作、Prow 等)上运行这些脚本。

**CII 最佳实践**

该检查试图确定项目是否有 CII 最佳实践徽章。它使用 Git repo 和 CII API 的 URL。该检查不考虑回购是否具有通过测试的解算器或黄金级别。

**补救步骤**

*   报名参加 CII 最佳实践计划。

**代码审查**

该检查试图在合并拉请求之前确定项目是否需要代码审查。首先，它检查默认分支上是否启用了分支保护，以及审阅者的数量是否至少为 1。如果失败，它检查最近的(~30)提交是否有 Github 批准的审查，或者合并是否不同于提交者(隐式审查)。如果至少有 75%的提交进行了如上所述的审查，则检查成功。如果失败，它会进行同样的检查，但会查找 Prow 的评论(标签为“lgtm”或“approved”)。如果失败了，它会做同样的事情，但是会寻找 gerrit 特有的提交消息(“Reviewed-on”和“Reviewed-by”)。

**补救步骤**

*   通过对每个新的拉请求执行严格的代码审查，遵循安全性最佳实践。
*   在您的存储库配置中强制进行“代码审查”。例如 GitHub。
*   对管理员/代码所有者也实施该规则。例如 GitHub

**投稿人**

这个检查试图确定一个项目是否有一组来自多个公司的参与者。它的工作方式是查看最近提交的作者，并检查 GitHub 用户配置文件上的`Company`字段。一个贡献者必须在过去的 30 个承诺至少有 5 个承诺。如果所有贡献者跨越至少两个不同公司，则检查成功。

**补救步骤**

*   这里不需要*任何*修复工作。这只是为了提供一些关于哪个(哪些)组织对项目做出了贡献的见解，并在此基础上做出信任决策。但是你可以要求你的贡献者加入他们各自的组织。

 **该检查试图确定项目是否已经声明并固定了它的依赖项。它的工作原理是(1)在根目录中查找以下文件:go.mod、go.sum (Golang)、package-lock.json、npm-shrinkwrap.json (Javascript)、requirements.txt、pipfile.lock (Python)、gemfile.lock (Ruby)、cargo.lock (Rust)、yarn.lock(包管理器)、composer.lock (PHP)、vendor/、third_party/、third-party/；(2)在 docker 文件、shell 脚本和 GitHub 工作流中查找未固定的依赖关系。如果(1)中的一个文件和(2)中的所有依赖项都已固定，则检查成功。

**补救步骤**

*   在您的包格式文件中声明您与特定版本的所有依赖关系(例如，`package.json`用于 npm，`requirements.txt`用于 python)。对于 C/C++，签入来自可信来源的代码，并在所使用的特定版本上添加一个`README`(以及归档 SHA 散列)。
*   如果包管理器支持锁文件(例如 npm 的`package-lock.json`),确保在源代码中也检查这些文件。这些文件维护整个依赖关系树的签名，并在包被破坏的情况下防止将来被利用。
*   对于 Dockerfiles 和 github 工作流，通过散列来固定依赖关系。参见 gitcache-docker.yaml 示例和 Dockerfile 示例。
*   为了在锁定依赖项后帮助更新它们，可以使用 Github 的 dependibo[t](https://github.blog/2020-06-01-keep-all-your-packages-up-to-date-with-dependabot/)或 renewal bot 等工具。

**起毛**

这项检查试图确定项目是否使用了模糊系统。它目前的工作方式是检查回购名称是否在 OSS-模糊项目列表中。

**补救步骤**

*   按照这里的说明，与 OSS-Fuzz 整合项目。

**拉取请求**

该检查试图确定项目是否需要对默认分支的所有更改进行 pull 请求。它通过查看最近的提交(第一页，大约 30 页)来工作，并使用 GitHub API 来搜索相关的 pull 请求。该检查会丢弃用户名包含“bot”或“gardener”的提交。该检查将包含字符串`Reviewed-on`的提交视为通过 gerrit 进行审查；并且不检查相应的 PR。

**补救步骤**

*   对于您打算进行的任何更改，无论是大是小，都要打开一个拉式请求。
*   在存储库配置中强制执行“拉请求”。例如 GitHub
*   对管理员/代码所有者也实施该规则。例如 GitHub

**SAST**

这项检查试图确定项目是否使用静态代码分析系统。它目前的工作方式是在 GitHub pull 请求中寻找众所周知的结果。更具体地说，检查首先在最近(~30 个)合并的 PRs 中寻找名为 github-code-scanning (codeql)和 sonarcloud 的 Github 应用程序。如果超过 75%的提交包含至少一个成功的检查(通过上面的任何应用程序)，则检查成功。如果上述操作失败，检查将在 github 工作流中查找“github/codeql-action”的使用。

**补救步骤**

*   按照这里的说明在您的 CI/CD 中运行 CodeQL 检查。

**安全政策**

该检查试图确定项目是否发布了安全策略。它通过在几个众所周知的目录中查找名为`SECURITY.md`(不区分大小写)的文件来工作。

**补救步骤**

*   将安全策略文件`SECURITY.md`放在您的存储库的根目录下。这使得漏洞报告者很容易发现它。
*   该文件应包含有关漏洞构成和安全报告方法的信息(例如，带有私人问题支持的问题跟踪器、带有公开公钥的加密电子邮件)。

**签售**

该检查试图确定项目是否对发布工件进行加密签名。它的工作原理是寻找文件名:*。minisign(https://github . com/jedisct 1/minisign)，*。asc (pgp)，*.sign .，用于最近 5 个 GitHub 版本。该检查不验证签名。

**补救步骤**

*   发布新闻稿。
*   生成签名密钥。
*   将该版本作为归档文件下载到本地。
*   用这个密钥签署发布档案(应该输出一个签名文件)。
*   将签名文件附加到发布归档文件旁边。
*   对于 GitHub，查看这里的步骤。

 **该检查在最后 5 个标签中寻找加密签名的标签。检查并不验证签名，而是依赖于 github 的验证。

**补救步骤**

*   生成新的签名密钥。
*   将您的密钥添加到您的源主机提供商。
*   在 git 中配置您的密钥和电子邮件。
*   发布标签，然后用这个密钥签名。
*   对于 GitHub，查看这里的步骤。

**令牌-权限**

该检查试图确定项目的 GitHub 工作流是否遵循最小特权原则，即 GitHub 令牌是否默认设置为只读。对于每个工作流 yaml 文件，该检查查找 permissions 关键字。如果对整个文件全局设置为只读，则检查成功。否则会失败。该检查无法检测是否启用了“只读”GitHub 权限设置，因为没有可用的 API。

**补救步骤**

*   按照 GitHub 文档中的描述，将权限设置为`read-all`或`contents: read`。

**漏洞**

该检查使用 OSV 服务确定项目中是否存在未修复的公开漏洞。

**补救步骤**

*   修复漏洞。每个漏洞的详细信息可以在 https://osv.dev 上找到。

**用途**

**使用存储库 URL**

该程序可以只使用一个参数运行，即回购的 URL:

**$去建造
$吧。/score card–repo = github . com/kubernetes/kubernetes
开始[已签名标签]
开始[自动-依赖-更新]
开始[冻结-Deps]
开始[模糊化]
开始[拉式请求]
开始[分支-保护]
开始[代码-审查]
开始[SAST]
开始[贡献者]
开始[已签名-发布]
开始[打包]
开始[令牌-令牌
完成【自动-依赖-更新】
完成【冻结-Deps】
完成【模糊】
完成【拉取-请求】
完成【签名-标记】
完成【分支-保护】
完成【代码-评审】
完成【SAST】
结果
回购:github.com/kubernetes/kubernetes
活动:通过 10
自动-依赖-更新:失败 3
二进制-工件:通过 10【通过**

有关检查失败原因的更多详细信息，请使用`**--show-details**`选项:

**。/score card–Repo = github . com/kubernetes/kubernetes–checks Frozen-Deps–show-details
开始【Frozen-Deps】
完成【Frozen-Deps】
结果
Repo:github.com/kubernetes/kubernetes
Frozen-Deps:Fail 10
…
！！freezed-deps/docker–cluster/addons/fluentd-elastic search/es-image/docker file 具有非固定依赖关系' golang:1.16.5'
…
！！frozen-deps/fetch-execute–cluster/GCE/util . sh 正在获取并执行非固定程序' curl https://sdk.cloud.google.com | bash '
…
！！frozen-deps/fetch-execute–hack/Jenkins/benchmark-dockerized . sh 正在获取一个非固定依赖项' go 111 module = on go install github.com/cespare/prettybench'
…**

**使用包管理器**

记分卡可以选择提供`**--npm**` / `**--pypi**` / `**--rubygems**`包名，它会对相应的 GitHub 源代码进行检查。

例如:

**。/score card–NPM = angular
Starting[Active]
Starting[Branch-Protection]
Starting[CI-Tests]
Starting[CII-最佳实践]
Starting[Code-Review]
Starting[Contributors]
Starting[freezed-Deps]
Starting[Fuzzing]
Starting[Packaging]
Starting[Pull-Requests]
Starting[SAST]
Starting[Security-Policy]
Starting[Signed-Releases]

完成【拉取请求】
完成【贡献者】
结果
活动:失败 10
分支-保护:失败 0
CI-测试:通过 10
CII-最佳实践:失败 10
代码-评审:通过 10
贡献者:通过 10
冻结-Deps:失败 0
模糊化:失败 10
打包:失败 0
拉取请求:失败 9【9】**

**运行特定检查**

要使用特定的检查，添加带有检查名称列表的`**--checks**`参数。

比如`**--checks=CI-Tests,Code-Revie**w`。

**认证**

在运行记分卡之前，您需要:

*   创建一个 GitHub 访问令牌并在环境变量`**GITHUB_AUTH_TOKE**N`中设置它。这有助于避免 GitHub 对未认证请求的 api 速率限制。

# **对于 posix 平台，如 linux、mac:
导出 GITHUB _ AUTH _ TOKEN =
#对于 windows:
设置 GITHUB_AUTH_TOKEN=**

可以提供多个`**GITHUB_AUTH_TOKEN**`，用逗号分隔，以循环方式使用。

*   为更高的速率限制配额创建一个 GitHub 应用程序安装。如果您已经安装了 GitHub 应用程序和密钥文件，您可以按照上面针对您的平台显示的命令，使用这三个环境变量。

**GITHUB _ APP _ KEY _ PATH =
GITHUB _ APP _ INSTALLATION _ ID =
GITHUB _ APP _ ID =**

这些可以从 GitHub 开发者设置页面获得。

**了解记分卡结果**

每次检查都返回一个**通过/失败**决定，以及一个在 **0 和 10** 之间的置信度得分。置信度为 0 应表示检查无法获得任何真实信号，结果应被忽略。置信度为 10 表示检查对结果完全有把握。

**格式化结果**

目前有三种格式:`**default**`、`**json**`、`**csv**`。将来可能会添加其他内容。

这些可以用`**--format**`标志来指定。

**公开数据**

如果您只对查看带有记分卡检查结果的项目列表感兴趣，我们会在 BigQuery 公共数据集中发布这些结果。

该数据在公共 BigQuery 数据集 **`openssf:scorecardcron.scorecard`中可用。**最新的结果可以在**的 BigQuery 视图中找到。**

您可以使用`**bq**`工具将 JSON 格式的最新结果提取到 Google 云存储中:

# **获取最新的 PARTITION _ ID
bq query–nouse _ legacy _ SQL ' SELECT PARTITION _ ID FROM
openssf . scorecardcron . information _ SCHEMA。分区顺序由 partition_id DESC
限制 1′
#提取到 GCS
bq 提取–destination _ format = NEWLINE _ DELIMITED _ JSON
' openssf:score cardcron . score card $ ' GS://bucket-name/filename . JSON**

在这个存储库中的 [`cron/data/projects.csv`](https://github.com/ossf/scorecard/blob/main/cron/data/projects.csv) 文件中可以找到被检查的项目列表。如果您希望我们跟踪更多信息，请随时向其他人发送拉取请求。

**注意**:目前，这些列表仅来自 GitHub 上托管的**项目**。我们确实计划在不久的将来扩展它们，以考虑托管在其他源代码控制系统上的项目。

**添加记分卡检查**

如果您想添加支票，请确保它符合以下标准，然后创建一个新的 GitHub 问题:

*   记分卡必须仅由可自动化的客观数据组成。例如，一个有 10 个贡献者的项目并不一定意味着它比一个有 50 个贡献者的项目更安全。但是，有两个维护者可能比只有一个更好——更大的总线因素和提供代码审查的能力客观上更好。
*   记分卡标准可以尽可能具体，而不局限于一般建议。例如，对于 Go，我们可以推荐/要求在代码库上运行特定的 linters 和分析器。
*   可以为任何开源项目填充记分卡，而无需维护人员的任何工作或交互。
*   必须为维护人员提供一种机制，以纠正他们认为错误的任何自动化记分卡发现，为我们不能自动检测的任何事情提供“提示”，甚至质疑给定记分卡发现对该存储库的适用性。
*   记分卡中的任何标准都必须是可操作的。在帮助下，任何项目都应该有可能“检查所有的框”。
*   任何编译记分卡的解决方案都应该可以被更大的开源社区用来监控上游安全。

[**Download**](https://github.com/ossf/scorecard)****