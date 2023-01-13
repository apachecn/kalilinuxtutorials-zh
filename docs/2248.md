# Kubernetes-Goat:是一个“设计脆弱”的 Kubernetes 集群

> 原文：<https://kalilinuxtutorials.com/kubernetes-goat/>

[![](img/df3822814da691546a05a28221f7614c.png)](https://blogger.googleusercontent.com/img/a/AVvXsEglOD8WHyMGBivE0B-6VMOYvPNgzXuoVuZ66Nurx9ZEFD6Uc4VCBZssE_esQz3zWh7oB5I951AlkgCw3DBMGQySujvuo1keSs88cUkdBOa3CgpkXi49axtNV_BMmg6qKMarKU8TdvjFwpeZNCUXgVklYQJar3qvvHs3oX15LvF9plZzVxttT3gEqGeK=s728)

**Kubernetes-Goat** 被设计成一个故意易受攻击的集群环境，用于学习和实践 Kubernetes 安全性。

**建立 Kubernetes 山羊**

在我们设置 Kubernetes Goat 之前，请确保您已经创建了 Kubernetes 集群，并且拥有该集群的管理员权限

**kubectl 版本–sh**ort

在你的路径中设置第二版头盔为`**helm2**`。有关设置的更多信息，请参考头盔版本

**helm 2–帮助**

最后，通过运行以下命令来设置 Kubernetes Goat

**git 克隆 https://github . com/madhuakula/kubriones-goat . git
kubriones-goat CD
bash setup-kubriones-goat . sh**

要在本地导出端口/服务以开始学习，请运行以下命令

**bash access-kubernetes-goat . sh**

建立库伯内特山羊利用种

如果你想使用 KIND(Docker 中的 Kubernetes)设置 Kubernetes 山羊，那么按照以下步骤操作

确保你已经完成了 Kubernetes 山羊中提到的先决条件。此外，您必须在系统中本地安装和设置 KIND。

*   要设置 KIND 集群，请运行以下命令

**bash setup-kind-cluster-and-goat . sh**

然后，要在本地访问 Kubernetes Goat，运行以下命令

**bash access-kubernetes-goat . sh**

要销毁该类集群，请运行以下命令

**bash teardown-cluster.sh**

[**Download**](https://github.com/madhuakula/kubernetes-goat)