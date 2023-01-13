# Kube-Hunter:寻找 Kubernetes 集群中的安全弱点

> 原文：<https://kalilinuxtutorials.com/kube-hunter-security-weaknesses/>

Kube-hunter 搜寻 Kubernetes 集群中的安全弱点。开发该工具是为了提高 Kubernetes 环境中安全问题的意识和可见性。

注意:您不应该在您不拥有的 Kubernetes 集群上运行 kube-hunter！

Kube-hunter 可以作为一个容器(aquasec/kube-hunter)使用，我们还在[kube-hunter.aquasec.com](https://kube-hunter.aquasec.com/)提供了一个网站，您可以在那里在线注册以获得一个令牌，允许您在线查看和共享结果。

您也可以自己运行 Python 代码，如下所述。

**也可阅读:**[Sitadel——网络应用安全扫描器](https://kalilinuxtutorials.com/sitadel-security-scanner/)

#### 你应该在哪里运行 kube-hunter？

在任何机器(包括你的笔记本电脑)上运行 kube-hunter，选择远程扫描并给出你的 Kubernetes 集群的 IP 地址或域名。这将给你一个攻击者视角的 Kubernetes 设置。

您可以直接在集群中的机器上运行 kube-hunter，并选择探测所有本地网络接口的选项。

您还可以在集群内的 pod 中运行 kube-hunter。这表明，如果您的一个应用程序容器受到危害(例如，通过软件漏洞)，您的集群将面临多大的风险。

#### **扫描选项**

默认情况下，kube-hunter 将打开一个交互式会话，您可以在其中选择以下扫描选项之一。您也可以从命令行手动指定扫描选项。这些是你的选择:

1.  **远程扫描**要指定远程机器进行搜索，选择选项 1 或使用`**--remote**`选项。示例:`**./kube-hunter.py --remote some.node.com**`
2.  **内部扫描**要指定内部扫描，可以使用`--internal`选项。(这将扫描机器的所有网络接口)示例:`**./kube-hunter.py --internal**`
3.  **网络扫描**要指定要扫描的特定 CIDR，请使用`--cidr`选项。示例:`**./kube-hunter.py --cidr 192.168.0.0/24**`

### 主动狩猎

主动搜索是一个选项，kube-hunter 将利用它发现的漏洞，以探索进一步的漏洞。

正常搜索和主动搜索的主要区别在于，正常搜索永远不会改变集群的状态，而主动搜索可能会对集群进行状态改变操作，**这可能是有害的**。

默认情况下，kube-hunter 不会主动狩猎。要主动搜索集群，请使用`**--active**`标志。示例:`**./kube-hunter.py --remote** **some.domain.com --active**`

#### **测试列表**

您可以通过`**--list**`选项查看测试列表:例如:`**./kube-hunter.py --list**`

要查看主动搜索测试和被动搜索测试:`**./kube-hunter.py --list --active**`

#### **输出**

要控制日志记录，您可以使用`--log`选项指定日志级别。示例:`**./kube-hunter.py --active --log WARNING**`可用的日志级别有:

*   调试
*   信息(默认)
*   警告

要仅查看节点网络的映射，请使用`**--mapping**`选项运行。示例:`**./kube-hunter.py --cidr 192.168.0.0/24 --mapping**`这将输出 kube-hunter 找到的所有 Kubernetes 节点。

#### **部署**

部署 kube-hunter 有三种方法:

##### **在机器上**

您可以直接在您的机器上运行 kube-hunter python 代码。

#### **先决条件**

您需要安装以下软件:

*   python 2.7
*   点
*   克隆存储库:

**git clone git @ github . com:aqua security/kube-hunter . git**

#### **安装模块依赖:**

**cd。/kube-hunter
pip 安装要求. txt**

如果默认路径中有 python 3.x，并且 python2 引用 python 2.7 可执行文件，请使用“python 2-m pip install-r requirements . txt”

#### **运行**

**。"库巴-亨特"**

#### **集装箱**

Aqua Security 在`**aquasec/kube-hunter**`维护着一个集装箱版本的 kube-hunter。

这个容器包括这个源代码，加上一个额外的(封闭源代码)报告插件，用于将结果上传到可以在 kube-hunter.aquasec.com 查看的报告中。

请注意，运行`aquasec/kube-hunter`容器和上传报告数据受附加[条款和条件](https://kube-hunter.aquasec.com/eula.html)的约束。

这个库中的 Dockerfile 允许您构建一个没有报告插件的容器化版本。

如果您在主机网络上运行 kube-hunter 容器，它将能够探测主机上的所有接口:

`**docker run -it --rm --network host aquasec/kube-hunter**`

*Docker for Mac/Windows 注意:*注意 Docker for Mac 或 Windows 的“主机”是 Docker 在其中运行容器的虚拟机。

因此，指定`--network host`允许 kube-hunter 访问该虚拟机的网络接口，而不是您的机器的网络接口。

默认情况下，kube-hunter 以交互模式运行。您还可以使用上述参数指定扫描选项，例如

`**docker run --rm aquasec/kube-hunter --cidr 192.168.0.0/24**`

#### 之下**之下**

此选项让您发现运行恶意容器会在您的集群上做什么/发现什么。

这提供了一个视角，如果攻击者能够危害一个 pod，可能通过软件漏洞，他们会做什么。这可能会暴露更多的漏洞。

`job.yaml`文件定义了一个将在 pod 中运行 kube-hunter 的作业，使用默认的 Kubernetes pod 访问设置。

*   使用 yaml 文件运行带有`kubectl create`的作业。
*   用`kubectl describe job kube-hunter`查找 pod 名称
*   用`kubectl logs <pod name>`查看测试结果

[**Download**](https://github.com/aquasecurity/kube-hunter)