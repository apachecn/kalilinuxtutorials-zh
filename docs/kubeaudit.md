# Kubeaudit:根据通用安全控制来审计您的 Kubernetes 集群的工具

> 原文：<https://kalilinuxtutorials.com/kubeaudit/>

[![](img/764c2d535ed6cf945e875c75db76a4cc.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiVpBqWVJkqA6TMhib8zPzRcqTTw9aXDaap28JLf_tJtBUqFMfbugKq5D7kMD2F5aOT3W1FoepZhSw_eFD4z9DraidcDmr_QIG867OxIMPaxHh4K_KtHb7rscm-eXjfbTVI6onvMuAtJATjii2vAwKoqzCD9eA1_Z1oTSPQ3-qCsCfi3kxwN0JgVJpv/s728/Kubeaudit-Tool-To-Audit-Your-Kubernetes-Clusters-Against-Common.png)

从 Kubernetes v.1.16 版本开始，Kubeaudit 不再支持不推荐使用的 API。所以，现在集群需要运行 Kubernetes > =1.16

`**kubeaudit**`是一个命令行工具和 Go 包，用于审计 Kubernetes 集群的各种不同的安全问题，例如:

*   以非根用户身份运行
*   使用只读根文件系统
*   放弃可怕的能力，不要增加新的能力
*   不要特权运行
*   还有更多！

**tldr。确保您部署了安全的容器！**

## 包装

要将 kubeaudit 用作 Go 软件包，请参阅软件包文档。

本自述文件的其余部分将重点介绍如何使用 kubeaudit 作为命令行工具。

## 命令行界面(CLI)

*   装置
*   快速启动
*   审计结果
*   命令
*   配置文件
*   覆盖错误
*   贡献的

## 安装

### 酿造

**brew 安装 kubeaudit**

### 下载二进制文件

Kubeaudit 有受祝福的稳定的官方版本:官方版本

### DIY 打造

Master 可能拥有比稳定版本更新的功能。如果您需要一个版本中尚未包含的新功能，请确保您使用的是 Go 1.17+并运行以下命令:

去找 github.com/Shopify/kubeaudit

使用`**kubeaudit**`快速启动或查看所有支持的命令。

### Kubectl 插件

先决条件:kubectl v1.12.0 或更高版本

随着 kubectl v1.12.0 引入外部函数的简单可插拔性，kubeaudit 可以通过

*   运行`**make plugi**n`并且在您的路径上有`**$GOPATH/bin**`可用。

或者

*   将二进制文件重命名为`**kubectl-audit**`，并在您的路径中提供它。

### 码头工人

我们还发布了一个 Docker 图片:`**shopify/kubeaudit**`。要在集群中将 kubeaudit 作为作业运行，请参见在集群中运行 kubeaudit。

## 快速启动

kubeaudit 有三种模式:

1.  清单模式
2.  本地方式
3.  集群模式

### 显示模式

如果使用`**-f/--manifest**`标志提供了 Kubernetes 清单文件，kubeaudit 将审计该清单文件。

命令示例:

**kube audit all-f "/path/to/manifest . yml "**

示例输出:

**$ kube audit all-f " internal/test/fixtures/all _ resources/Deployment-apps-v1 . yml "
——————————
API version:apps/v1
kind:Deployment
元数据:
name:Deployment
namespace:Deployment-apps-v1————————————————————
——【错误】AppArmoranotionmissing
消息:appmor 注释丢失。应该添加注释‘container . apparmor . securityβkubernetes . io/container’。
元数据:
容器:容器
缺失注释:container.apparmor.security.beta.kubernetes.io/container
—[错误]automountserviceaccountokentrueanddefaultsa
消息:已装入令牌的默认服务帐户。automountServiceAccountToken 应设置为“false ”,或者应使用非默认服务帐户。
—[错误] CapabilityShouldDropAll
消息:功能未设置为全部。理想情况下，您应该删除所有功能，并将您需要的特定功能添加到添加列表中。
元数据:
容器:容器
能力:AUDIT_WRITE…**

如果没有找到具有给定最低严重性的错误，则返回以下内容:

所有检查均已完成。发现 0 个高危漏洞

## 审计结果

Kubeaudit 产生三种严重程度的结果:

*   `**Error**`:安全问题或无效的 kubernetes 配置
*   `**Warning**`:最佳实践建议
*   `**Info**`:信息，不需要任何操作。这包括被覆盖的结果

可以使用`**--minSeverity/-m**`标志设置最低严重级别。

默认情况下，kubeaudit 将以人类可读的方式输出结果。如果打算对输出进行进一步处理，可以使用`**--format json**`标志将其设置为输出 JSON。使用`**--format logrus**`将结果输出为日志(之前的默认设置)。一些输出格式包括颜色，以使结果在终端中更容易阅读。要禁用颜色(例如，如果您将输出发送到文本文件)，您可以使用`**--no-color**`标志。

如果有严重级别`**error**`的结果，kubeaudit 将退出，退出代码为 2。这可以使用`**--exitcode/-e**`标志进行更改。

有关 kubeaudit 的所有自定义方式，请参见全局标志。

## 命令

| 命令 | 描述 | 证明文件 |
| --- | --- | --- |
| `**all**` | 运行所有可用的审计员，或者使用 kubeaudit 配置指定的审计员。 | 文件（documents 的简写） |
| `**autofix**` | 自动修复安全问题。 | 文件（documents 的简写） |
| `**version**` | 打印当前的 kubeaudit 版本。 |  |

### 审计人员

审计员也可以单独运行。

| 命令 | 描述 | 证明文件 |
| --- | --- | --- |
| `**apparmor**` | 发现集装箱运行时没有外观。 | 文件（documents 的简写） |
| `**asat**` | 使用自动安装的默认服务帐户查找 pod | 文件（documents 的简写） |
| `**capabilities**` | 查找不删除推荐功能或添加新功能的容器。 | 文件（documents 的简写） |
| `**deprecatedapis**` | 查找用不推荐使用的 API 版本定义的任何资源。 | 文件（documents 的简写） |
| `**hostns**` | 查找启用了 HostPID、HostIPC 或 HostNetwork 的容器。 | 文件（documents 的简写） |
| `**image**` | 查找不使用所需图像版本(通过标签)或使用无标签图像的容器。 | 文件（documents 的简写） |
| `**limits**` | 查找超过指定 CPU 和内存限制或未指定任何限制的容器。 | 文件（documents 的简写） |
| `**mounts**` | 查找装载了敏感主机路径的容器。 | 文件（documents 的简写） |
| `**netpols**` | 查找没有默认拒绝网络策略的命名空间。 | 文件（documents 的简写） |
| `**nonroot**` | 查找以根用户身份运行的容器。 | 文件（documents 的简写） |
| `**privesc**` | 查找允许权限提升的容器。 | 文件（documents 的简写） |
| `**privileged**` | 查找以特权身份运行的容器。 | 文件（documents 的简写） |
| `**rootfs**` | 查找没有只读文件系统的容器。 | 文件（documents 的简写） |
| `**seccomp**` | 查找不使用 Seccomp 运行的容器。 | 文件（documents 的简写） |

### 全球旗帜

| 短的 | 长的 | 描述 |
| --- | --- | --- |
|  | –格式 | 要使用的输出格式(“pretty”、“logrus”、“json”之一)(默认为“pretty”) |
|  | –kubeconfig | 本地 Kubernetes 配置文件的路径。仅在本地模式下使用(默认为`**$HOME/.kube/config**`) |
| -丙 | –背景 | 要使用的 kubeconfig 上下文的名称 |
| -f | –清单 | 要审核的 yaml 配置的路径。仅在清单模式下使用。您可以使用`**-**`从标准输入中读取数据。 |
| 同-EN | –名称空间 | 仅审核指定命名空间中的资源。清单模式下当前不支持。 |
| -g | –包含生成的 | 在扫描中包括生成的资源(如部署生成的 pod)。如果您希望 kubeaudit 为生成的资源生成结果(例如，如果您有自定义资源或者想要捕获所有者资源不再存在的孤立资源)，您可以使用这个标志。 |
| -m | –最小化 | 将最低严重级别设置为报告(“错误”、“警告”、“信息”之一)(默认为“信息”) |
| -e | –exitcode | 如果存在严重性为“错误”的结果，则使用退出代码。通常，0 表示成功，所有非零代码表示错误。(默认值为 2) |
|  | –无色 | 不要在输出中使用颜色(默认为 false) |

## 配置文件

kubeaudit 配置可用于两件事:

1.  仅启用部分审计员
2.  为审计员指定配置

可以使用各个审计员的标志来指定的任何配置都可以使用 config 来表示。

该配置具有以下格式:

**enabledAuditors:
#如果没有显式设置为" false "
apparmor:false
ASAT:false
capabilities:true
deprecated APIs:true
hostns:true
image:true
limits:true
mounts:true
net pols:true
nonroot:true
privesc:true
privileged:true
rootfs:true
CHOWN ']
deprecated API:
#如果未指定版本，并且启用了“deprecated API”审计器，将为使用已弃用的 API 定义的资源生成警告
#结果。
current version:' 1.22 '
targeted version:' 1.25 '
image:
#如果未指定图像且启用了“图像”审计器，将为使用无标记图像的容器生成警告结果
# image:' my image:mytag '
limits:
#如果未指定限制且启用了“限制”审计器，将为无 cpu 或内存的容器生成警告结果
#**

有关每个审计员的更多详细信息，包括配置中特定于审计员的配置的描述，请参见审计员文档。

**注意**:kube audit 配置不同于用`**--kubeconfig**`标志指定的 kubeconfig 文件，它指的是 Kubernetes 配置文件(见本地模式)。还要注意，只有 **`all`** 和`**autofix**`命令支持使用 kubeaudit 配置。它不能与其他命令一起使用。

**注意**:如果标志与配置文件一起使用，标志优先。

## 覆盖错误

通过添加覆盖标签，可以忽略特定容器或箱的安全问题。这意味着审计员将产生`**info**`结果，而不是`**error**`结果，并且审计结果名称将附加`**Allowed**`。标签记录在每个审计员的文档中，但是支持覆盖的审计员的一般格式如下:

覆盖标签由一个`**key**`和一个`**value**`组成。

`**key**`是覆盖类型(容器或 pod)和`**override identifier**`的组合，对于每个审计员来说是唯一的(参见特定审计员的文档)。根据覆盖类型，`**key**`可以采用两种形式之一:

1.  **容器覆盖**，覆盖特定容器的审计者，格式如下:

**container . audit . kubernetes . io/【容器名称】。【覆盖标识符】**

根据 Kubernetes 规范，`**value**`必须为 63 个字符或更少，并且必须为空或以字母数字字符(`**[a-z0-9A-Z]**`)开始和结束，中间有破折号(`**-**`)、下划线(`**_**`)、点(`**.**`)和字母数字字符。

可以将多个覆盖标签(针对多个审计员)添加到同一资源中。

有关示例，请参见您希望覆盖的审计员的特定审计员文档。

要了解有关标签的更多信息，请参见 https://kubernetes . io/docs/concepts/overview/working-with-objects/labels/

[**Download**](https://github.com/Shopify/kubeaudit)