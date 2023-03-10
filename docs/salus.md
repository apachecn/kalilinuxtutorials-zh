# Salus:安全扫描仪协调员

> 原文：<https://kalilinuxtutorials.com/salus/>

[![Salus : Security Scanner Coordinator](img/cd14ab75ce140f9e478aafd03bf8111b.png "Salus : Security Scanner Coordinator")](https://1.bp.blogspot.com/-0rCT7XvYIb8/YOfLguE5aYI/AAAAAAAAJ7I/uD1oQpRiNdMunAZtARwqnArQ9eEofDPBwCLcBGAsYHQ/s728/logo%2B%25281%2529.png)

**Salus**(Security Automation 作为一款轻量级通用扫描仪)，以罗马保护女神命名，是一款协调安全扫描仪执行的工具。您可以通过 Docker 守护进程在存储库上运行 Salus，它将确定哪些扫描器是相关的，运行它们并提供输出。大多数扫描仪是我们直接包含在容器中的其他成熟的开源项目。

Salus 对于 CI/CD 管道特别有用，因为它成为一个集中的地方来协调跨大型存储库的扫描。通常，扫描器是在每个项目的存储库级别配置的。这意味着当在组织范围内对扫描器的运行方式进行更改时，必须更新每个存储库。相反，你可以更新 Salus，所有的构建都会立即继承这个改变。

Salus 支持强大的配置，允许全局默认和局部调整。最后，Salus 可以报告每个存储库的度量，比如包含什么包或者存在什么问题。可以在您的基础架构中集中评估这些报告，以便进行可扩展的安全跟踪。

**使用 Salus**

# **在
cd /path/to/repo
中导航到您想要运行 Salus 的项目的根目录#在根目录中运行下面一行(无需编辑)
docker Run–RM-t-v $(pwd):/home/repo coin base/Salus**

**支持的扫描仪**

*   Bandit——Bandit 1 . 6 . 2 的执行，寻找 Python 代码中常见的安全问题。
*   brake man——执行 Brakeman 4.10.0，寻找 Rails 项目中易受攻击的代码。
*   SEM grep——执行 **`semgrep`** 0.36.0，在 AST 级别查找代码中的语义和语法模式。
*   bundle audit——执行 bundle-audi [t](https://github.com/rubysec/bundler-audit) 0.8.0，在 ruby gem 依赖项中寻找 CVE。
*   gosec——执行 gosec 2.7.0，寻找 go 代码中的安全问题。
*   npm 审计–执行 **`npm audit`** 6.14.8，在节点模块依赖关系中查找 CVE。
*   yarn audit–执行`**yarn audit**` 1.22.0，在节点模块依赖关系中查找 CVE。
*   pattern search——执行`**sift**` 0.9.0，在项目中寻找某些可能有危险或者可能需要某些字符串存在的字符串。
*   货物审计-执行货物审计 0.14.0 审计货物锁文件，检查向 RustSec 咨询数据库报告的存在安全漏洞的板条箱

**依赖跟踪**

Salus 还解析依赖文件并报告哪些库和版本正在被使用。这对于跟踪整个车队的依赖关系非常有用。

目前支持的语言有:

*   红宝石
*   节点. js
*   计算机编程语言
*   去
*   锈

**配置**

Salus 被设计成高度可配置的，因此它可以在许多不同类型的环境和许多不同的扫描仪中工作。它支持环境变量插值和级联配置，并可以通过 HTTP 读取配置和发布报告。

有时需要忽略某些 CVE、规则、测试、组、目录，或者修改扫描仪的默认配置。docs/scanners 目录解释了如何为 Salus 支持的每个扫描仪执行此操作。

如果您想构建自定义扫描仪或支持更多当前不支持的语言，您可以使用这种方法构建自定义 Salus 映像。

**CircleCI 集成**

Salus 可以通过使用公共 Orb 与 CircleCI 集成。支持所有 Salus 配置选项，默认值与 Salus 本身相同。

示例 CircleCI `**config.yml**`:

**版本:2.1
orbs:
salus:federacy/salus @ 3 . 0 . 0
工作流:
main:
jobs:
–salus/scan**

**Orb 文档**

**塞卢斯的圆形球体**

**参数**

| 属性 | 描述 | 系统默认值 | 选择 |
| --- | --- | --- | --- |
| salus_executor | circleci 执行程序使用指定 salus 环境 | `**coinbase/salus:latest**` | 参见 [e](https://circleci.com/docs/2.0/configuration-reference/#executors-requires-version-21) xecutor 参考 |
| 活动 _ 扫描仪 | 要运行的扫描仪 | 全部 | 布雷克曼，模式搜索，联邦审计，NPMAudit |
| 强制 _ 扫描仪 | 阻止生成的扫描器 | 全部 | 布雷克曼，模式搜索，联邦审计，NPMAudit |
| 报告 _uri | 向何处发送 Salus 报告 | 文件://../salus-report.json | 有 URI 吗 |
| 报告格式 | 报告使用什么格式 | json | json，yaml，txt |
| 报告 _ 详细程度 | 是否启用详细报告 | 真实的 | 真，假 |
| 配置文件 | repo 中配置文件的位置(覆盖除 salus_executor 之外的所有其他参数) | "" | 任意文件名

 |

**注意** : active_scanners 和 enforced_scanners 必须为 Salus 配置文件的 yaml 格式。

**CircleCI 环境变量**

存储在 Salus 扫描的`**custom_info**`中。

| 钥匙 | CircleCI 变量 | 描述 |
| --- | --- | --- |
| sha1 | SHA1 圈 | 构建中最后一次提交的哈希 |
| ci _ 项目 _ 用户名 | CIRCLE _ PROJECT _ 用户名 | 项目的 SCM 用户名 |
| reponame | 圆圈 _ 项目 _ 报告名称 | 存储库的名称 |
| 树枝 | 圆形 _ 分支 | 正在构建的 git 分支的名称 |
| 标签 | 圆圈 _ 标签 | 标签名称 |
| 存储库 _url | 圆圈 _ 存储库 _URL | Github 或 Bitbucket 存储库的 URL |
| 比较 _url | 圆形比较网址 | 在构建中比较提交的 URL |
| 构建 _url | CIRCLE_BUILD_URL | 该版本的 URL |
| 外部构建标识 | 圆圈 _ 构建 _ 编号 | CircleCI 或其他构建标识符 |
| 拉取请求 | 圆 _ 拉 _ 请求 | 以逗号分隔的拉请求列表 |
| ci _ 用户名 | CIRCLE _ 用户名 | 触发构建的用户的 SCM 用户名 |
| pr _ 用户名 | CIRCLE _ PR _ 用户名 | 创建拉取/合并请求的用户的 SCM 用户名 |
| pr_reponame | CIRCLE_PR_REPONAME | 创建拉/合并请求的存储库的名称 |
| 请购单编号 | 圈 _PR_NUMBER | 拉/合并请求的编号 |

**例题**

**。circi/config . yml〔t1〕**

**阻止所有扫描仪扫描**

**版本:2.1
orbs:
salus:federacy/salus @ 3 . 0 . 0
工作流:
main:
jobs:
–salus/scan**

**使用所有扫描仪进行无阻塞扫描**

**版本:2.1
orbs:
salus:federacy/salus @ 3 . 0 . 0
工作流:
main:
jobs:
–salus/scan:
enforced _ scanners:" none "**

**仅使用制动员阻止扫描**

**版本:2.1
orbs:
salus:federacy/salus @ 3 . 0 . 0
工作流:
main:
jobs:
–salus/scan:
active _ scanners:" \ n–brake man "
enforced _ scanners:" \ n–brake man "**

**用自定义 Salus 执行器扫描**

**版本:2.1
orbs:
salus:federated/salus @ 3 . 0 . 0
执行者:
salus _ 2 _ 4 _ 2:
dock:
–image:coinbase/salus:2 . 4 . 2
工作流程:【t】**

**未使用的 CircleCI 环境变量**

CI，CI_PULL_REQUEST，CI_PULL_REQUESTS，CIRCLE_INTERNAL_TASK_DATA，CIRCLE_JOB，CIRCLE_NODE_INDEX，CIRCLE_NODE_TOTAL，CIRCLE_PREVIOUS_BUILD_NUM，CIRCLE_PULL_REQUEST，CIRCLE_WORKING_DIRECTORY，CIRCLECI，HOME。

**Github 动作集成**

Salus 也可以和 Github 动作一起使用。

例子 **`.github/workflows/main.yml` :**

**on:[push]
jobs:
Salus _ Scan _ job:
runs-on:Ubuntu-latest
name:Salus 安全扫描示例
步骤:
–uses:actions/check out @ v1
–name:Salus Scan
id:Salus _ Scan
uses:federacy/Scan-action @ 0 . 1 . 1**

**Github 动作文档**

**Salus 安全扫描处理措施**

此操作利用比特币基地的 Salus 来运行 SAST 和依赖性扫描。

Bundle Audit、Brakeman、NPM Audit 和 Yarn Audit 报告可以选择由 Federacy 发送到 Secure Development 进行分析。

**支持的扫描仪**

| 名字 | 语言 |
| --- | --- |
| 捆绑审计 | 红宝石 |
| 司闸员 | 红宝石 |
| npm 审计 | Java Script 语言 |
| 纱线审计 | Java Script 语言 |
| 戈塞克 | 去 |
| 强盗 | 计算机编程语言 |
| 货物审计 | 锈 |
| 塞姆格雷普 | 许多 |
| 模式搜索 | 不适用(使用 Sift) |

**示例用法**

**默认值**

**on:[push]
jobs:
Salus _ Scan _ job:
runs-on:Ubuntu-latest
name:Salus 安全扫描示例
步骤:
–uses:actions/check out @ v1
–name:Salus Scan
id:Salus _ Scan
uses:federacy/Scan-action @ 0 . 1 . 1**

**单扫描仪**

**on:[push]
jobs:
Salus _ Scan _ job:
runs-on:Ubuntu-latest
name:Salus Security Scan Example
steps:
–uses:actions/check out @ v1
–name:Salus Scan
id:Salus _ Scan
uses:federacy/Scan-action @ 0 . 1 . 1
with:
active _ scanners:" \ n–brake man "
enforced _ scanners**

**没有强制扫描器**

**on:[push]
jobs:
Salus _ Scan _ job:
runs-on:Ubuntu-latest
name:Salus 安全扫描示例
步骤:
–uses:actions/check out @ v1
–name:Salus Scan
id:Salus _ Scan
uses:federacy/Scan-action @ 0 . 1 . 1
with:
enforced _ scanners:“none”**

**自定义配置**

**on:[push]
jobs:
Salus _ Scan _ job:
runs-on:Ubuntu-latest
name:Salus 安全扫描示例
步骤:
–uses:actions/check out @ v1
–name:Salus Scan
id:Salus _ Scan
uses:federacy/Scan-action @ 0 . 1 . 1
env:
Salus _ CONFIGURATION:" file://../salus-configuration . YAML file://config/pattern _ search . YAML "**

**输入**

| 属性 | 描述 | 系统默认值 | 选择 |
| --- | --- | --- | --- |
| 活动 _ 扫描仪 | 要运行的扫描仪 | 全部 | 布雷克曼，PatternSearch，BundleAudit，NPMAudit，GoSec |
| 强制 _ 扫描仪 | 阻止生成的扫描器 | 全部 | 布雷克曼，PatternSearch，BundleAudit，NPMAudit，GoSec |
| 报告 _uri | 向何处发送 Salus 报告 | 文件://../salus-report.json | 有 URI 吗 |
| 报告格式 | 报告使用什么格式 | json | json，yaml，txt |
| 报告 _ 详细程度 | 是否启用详细报告 | 真实的 | 真，假 |
| salus _ 配置 | 在哪里可以找到 Salus 配置 | 文件://../salus-configuration.yaml | 有 URI 吗 |

**注意** : active_scanners 和 enforced_scanners 必须为 Salus 配置文件的 yaml 格式。

**输出**

没有。

**Github 环境变量**

存储在 Salus 扫描的 custom_info 中。

| 钥匙 | Github 变量 | 描述 |
| --- | --- | --- |
| sha1 | GITHUB_SHA | 构建中最后一次提交的哈希 |
| reponame | GITHUB_REPOSITORY | 存储库的名称 |
| 裁判员 | GITHUB_REF | 引用触发流(分支或标签) |
| ci _ 用户名 | GITHUB_ACTOR | 触发构建的用户的 Github 用户名 |
| github_action | GITHUB_ACTION | 动作的名称 |
| github _ 工作流 | GITHUB _ 工作流 | 工作流的名称 |
| github _ 事件 _ 名称 | GITHUB _ 事件 _ 名称 | 触发工作流的事件的名称 |
| github _ 事件 _ 路径 | GITHUB _ 事件 _ 路径 | 事件负载的路径 |
| github_workspace | GITHUB_WORKSPACE | 工作区目录路径 |
| github_head_ref | GITHUB_HEAD_REF | 如果分叉，则引用主存储库 |
| github_base_ref | GITHUB_BASE_REF | 基本存储库的引用(如果分叉) |
| github_home | 家 | Github 使用的主目录的路径 |

**向仪表板发送报告**

步骤:

*   创建联邦安全开发的免费帐户
*   点击导航栏中的“应用程序”
*   点击“创建应用程序”
*   将示例作业复制到`**.github/workflows**`中的工作流程中

**在回购中使用 Salus**

对于给定的配置项，更新配置文件以运行 salus。在圆圈中，它看起来像这样:

**码头运行–RM-t-v $(pwd):/home/repo coinbase/salus**

协联/salus pulls the docker image

[**Download**](https://github.com/coinbase/salus)