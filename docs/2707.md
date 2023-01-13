# ggshield:检测源代码中的秘密，扫描您的 repo 中的漏洞

> 原文：<https://kalilinuxtutorials.com/ggshield/>

[![](img/045363364d8654254a33ca42e638bc33.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjyA1L0nwhCzEOj_olfx-ly-ijkuHip3qYbqN34_7Lo9Wauyq54h8jX9QTvvSdlzj_-YalkSA_Nx2Yu5TL17J1g1RpETmEapmMf_nEK4ugH9FH5NbY-gFP-28WZ9ylJcE08WP260fD_FroTPFnTdrzbct05nwbQT050Y05wO4KYOZOeprwOhPKbuqXM/s728/68747470733a2f2f63646e2e6a7364656c6976722e6e65742f67682f676974677561726469616e2f6767736869656c642f646f632f6c6f676f2e737667-svg%20(1).png)

**ggshield** 是一款 CLI 应用程序，可在您的本地环境或 CI 环境中运行，帮助您检测 350 多种类型的秘密，以及其他潜在的安全漏洞或违反策略的情况。

ggshield 通过 py-gitguardian 使用我们的公共 API 来扫描和检测文件和其他文本内容上的潜在秘密。

使用 ggshield 进行扫描时，仅存储呼叫时间、请求大小和扫描模式等元数据，因此机密和违反策略事件不会显示在您的仪表板上，**您的文件和机密也不会被存储**。

# 装置

## 苹果电脑

### 使用自制软件

您可以通过运行以下命令使用 Homebrew 安装 ggshield:

**$ brew 安装 gitguardian/tap/ggshield**

## Linux 软件包

Cloudsmith 上有 Deb 和 RPM 包。

安装说明:

*   Deb 包
*   RPM 包

## 其他操作系统

### 使用画中画

使用`**pip**`安装和更新:

**$ pip 安装 ggshield**

ggshield 支持 **Python 3.7 及更新的**。

该软件包应该可以在 MacOS、Linux 和 Windows 上运行。

#### 更新

要更新 ggshield，您可以在 pip 安装命令中添加选项`**-U/--upgrade**`

**$ pip install -U ggshield**

# 初始设置

要使用 ggshield，您需要通过 GitGuardian 服务器的认证。为此，使用`**ggshield auth login**`命令。该命令自动提供个人访问令牌并在本地工作站上进行配置。

你可以从`**ggshield auth login**`文档中了解更多。

或者，您可以手动创建您的个人访问令牌，并将其存储在`**GITGUARDIAN_API_KEY**`环境变量中以完成设置。

一旦完成，您就可以使用 **`ggshield secret scan repo /path/to/your/repo`开始扫描存储库。**

# 命令参考

**用法:ggshield【选项】命令【ARGS】…
选项:
-c，–config-path 文件设置自定义配置文件。忽略本地和全局
配置文件。
-v，–Verbose 详细显示模式。
–允许-自签名忽略 ssl 验证。
–调试显示调试信息。
–版本显示版本并退出。
-h，–帮助显示此消息并退出。
命令:
api-status 显示 api 状态。
管理认证的 auth 命令。
安装安装一个预提交或预推送 git 挂钩(本地或全局)。
配额显示配额概述。
使用秘密的秘密命令。**

## 秘密扫描命令

`**ggshield secret scan**`命令组包含主要的 ggshield 命令，它有几个配置选项可用于覆盖输出行为。

用法:ggshield 秘密扫描[选项]命令[ARGS]…

**扫描各种内容的命令。
选项:
–JSON JSON 输出结果【默认:False】
–Show-secrets 以明文显示秘密，而不是隐藏
。
–exit-zero 始终返回 0(无错误)状态代码，即使发现事件也是如此
。env var
git guardian _ EXIT _ ZERO 也可以用来设置
这个选项。
–所有策略存在所有策略失败(文件名、
文件扩展名、秘密检测)。默认情况下，
只显示秘密检测。
-v，–Verbose 详细显示模式。
-o，–输出路径路由 ggshield 输出到文件。
-b，–banlist-detector 文本排除来自检测器的结果。
–排除路径不扫描指定的路径。
–Ignore-default-excludes 默认情况下忽略排除的模式。【默认:
假】
-h，–帮助显示此消息并退出。
命令:
存档扫描存档。
ci 环境中的 ci 扫描。
提交范围扫描 git 中定义的 COMMIT_RANGE。
docker 扫描 docker 图像。
路径扫描文件和目录。
作为预提交 git 挂钩的预提交扫描。
预推送扫描作为预推送 git 挂钩。
预接收扫描作为预接收 git 挂钩。pypi 扫描一个 pypi 包。
repo 在给定的 URL 或路径扫描存储库的提交。**

`**ggshield secret scan**`对每种类型的扫描有不同的子命令。

### `**secret scan ci**`:扫描 CI 中自上次构建以来的每次提交

**用法:ggshield secret scan ci【选项】
在 ci 环境下扫描。
选项:
-h，–帮助显示此消息并退出。**

`**secret scan commit-range**`:扫描给定提交范围内的每个提交

**用法:ggshield secret scan commit-range【选项】COMMIT_RANGE
扫描 git 中一个定义好的 COMMIT_RANGE。
git rev-list COMMIT_RANGE 列出几个要扫描的提交。示例:gg shield
secret scan commit-range HEAD ~ 1…
选项:
-h，–帮助显示此消息并退出。**

`**secret scan path**`:使用递归选项扫描文件或目录

**用法:ggshield 秘密扫描路径[选项]路径…
扫描文件和目录。
选项:
-r，–递归扫描目录递归
-y，–是确认递归扫描
-h，–帮助显示此信息并退出。**

`**secret scan pre-commit**`:扫描 git 存储库中已暂存的每个更改

**用法:ggshield secret scan 预提交[OPTIONS] [PRECOMMIT_ARGS]…
作为预提交 git 挂钩扫描。
选项:
-h，–帮助显示此消息并退出。**

`**secret scan pypi**`:扫描 pypi 包

**用法:gg shield secret scan pypi[OPTIONS]PACKAGE _ NAME
扫描一个 pypi 包。
选项:
-h，–帮助显示此消息并退出。**

这个命令使用`**pip download**`命令下载 python 包。

您可以使用**e**环境变量或配置文件来设置`**pip download**`参数，如 pip 文档中所述。

例如，您可以通过设置`**PIP_INDEX_URL**`环境变量来设置 **`pip` `--index-url`** 参数。

# 配置

ggshield 中的配置遵循`**global>local>CLI**`配置方案。

意味着`**local**`上的选项覆盖或扩展`**global**`以及 CLI 上的选项覆盖或扩展本地。

ggshield 将在用户的主目录中搜索一个`**global**`配置文件(例如:Linux 上的`**~/.gitguardian.yml**`和 Windows 上的`**%USERPROFILE%\.gitguardian**`)。

ggshield 还会识别用户工作目录中的`**local**`配置文件(例如:`**./.gitguardian.yml**`)。

您也可以使用主命令上的选项`**--config-path**`来设置另一个配置文件。在这种情况下，`**local**`和`**global**`配置文件都不会被评估(例如:`**ggshield --config-path=~/Desktop/only_config.yaml scan path -r .**`)

示例配置文件可以在. gitguardian.example 中找到

## 迁移 v1 配置文件

如果您有 v1 配置文件，您可以运行 **`ggshield config migrate`** 让 ggshield 为您迁移它。该命令就地修改配置文件，但是它将以前的版本保留为一个`**.gitguardian.yaml.old**`文件。

或者，您可以按照以下步骤手动迁移配置文件:

调试:false #默认值:false

*   添加一个`**version:** 2`条目。
*   如果配置文件包含一个`**all-policies**`键，删除它:它不再被支持。
*   如果配置文件包含一个`**ignore-default-excludes**`键，删除它:它不再被支持。
*   如果配置文件包含一个`**api-url**`键，用一个`**instance**`键替换它，指向*仪表板* URL。
*   如果配置文件包含下列关键字之一: **`paths-ignore`、`matches-ignore`、`show-secrets`、`banlisted-detectors`、**:
    *   创建一个`**secret**`键。
    *   将`**paths-ignore**`移动到`**secret.ignored-paths**`。
    *   将`**matches-ignore**`移动到`**secret.ignored-matches**`。如果有些匹配条目是字符串而不是(**、`match`、**)对象，那么把它们变成(**、`match`、**)对象。
    *   将`**banlisted-detectors**`移动到`**secret.ignored-detectors**`。
    *   将`**show-secret**s`移动到`**secret.show-secrets**`。

## 环境变量

也可以使用环境变量来配置 ggshield。

环境变量会覆盖在配置文件中设置的设置，但会被命令行选项覆盖。

启动时，ggshield 尝试按以下顺序从不同的环境文件中加载环境变量:

*   环境变量指向的路径`**GITGUARDIAN_DOTENV_PATH**`
*   在你当前的工作目录。
*   `**.env**`当前 git 目录的根目录

三个文件中只会加载一个。

ggshield 支持的当前环境变量引用:

*   `**GITGUARDIAN_API_KEY**`:git guardian API 的 API 密钥。如果您不想使用`**ggshield auth**`命令，请使用此选项。
*   `**GITGUARDIAN_INSTANCE**`:git guardian 仪表盘的自定义 URL。API URL 将从中推断出来。
*   `**GITGUARDIAN_API_URL**`:扫描 API 的自定义 URL。已弃用，请改用`**GITGUARDIAN_INSTANCE**`。
*   `**GITGUARDIAN_DONT_LOAD_ENV**`:如果设置为任意值，将不会从文件中加载环境变量。
*   `**GITGUARDIAN_DOTENV_PATH**`:如果设置为路径，ggshield 将尝试从指定文件加载环境。
*   `**GITGUARDIAN_TIMEOUT**`:如果设置为浮点型，`**ggshield secret scan pre-receiv**e`将在指定值后超时。置 0 禁用超时。
*   `**GITGUARDIAN_MAX_COMMITS_FOR_HOOK**`:如果设置为 int，`**ggshield secret scan pre-receive**`和`**ggshield secret scan pre-push**`在一次扫描中不会扫描超过指定值的提交。
*   `**GITGUARDIAN_CRASH_LOG**`:如果设置为 True，ggshield 将在崩溃时显示完整的回溯。

## 内部配置

ggshield 可以配置为在本地 GitGuardian 实例上运行。

首先，您需要通过在您的`**.gitguardian.yaml**`配置文件中定义`**instance**`键或者通过定义`**GITGUARDIAN_INSTANCE**`环境变量，将 ggshield 指向您的实例。

然后，您需要对您的实例进行身份验证，要么使用带有`**--instance**`选项的`**ggshield auth login --instance** **https://mygitguardianinstance.mycorp.local**`命令，要么从您的仪表板管理员那里获得一个 API 密匙并将其存储在`**GITGUARDIAN_API_KEY**`环境变量中。

## 忽略文件

默认情况下，ggshield 会忽略某些文件和目录。

这个列表可以在 **`IGNORED_DEFAULT_PATTERNS`下的 ggshield/core/utils.py 中找到。**

您也可以使用`**--exclude**`选项或`**.gitguardian.yaml**`中的`**ignored-paths**`键添加要忽略的自定义模式

## 预推

如果 push 中有超过 50 个提交，钩子将被跳过。

跳过钩子之前要扫描的提交数量可以通过 ggshield 配置文件中的键`**max-commits-for-hook**`来配置。

预推送挂钩就在`**git pus**h`向远程主机发送数据之前执行。它将拾取并扫描局部 ref 和原点 ref 之间的提交范围。

如果在此范围内检测到事件，推送将被取消。

### 使用预提交框架

为了在预提交框架中使用 ggshield，您需要执行以下步骤。

确保您安装了预提交:

**$ pip 安装预提交**

[**Download**](https://github.com/GitGuardian/ggshield#initial-setup)