# CloudSpec:一个开源工具，用于使用逻辑语言验证云提供商的资源

> 原文：<https://kalilinuxtutorials.com/cloudspec/>

[![](img/73517b7b15653d8b4bd898aa3918c6f3.png)](https://blogger.googleusercontent.com/img/a/AVvXsEhcClqf0oFe4lFhY2Fo7wQZLjt3XKyeoVaM22DuW-N1H0gxlm08fKiwFZES8f-_5J0EgQ4Y_n-SkfF-LIHHU-QbxlDkfRFvmriDroEevJWn0Sm1LXhDjaNjuin_Kc0WWGpNgW2LSkSx_d31lOAsW-orvSniB8l-TSoyo92dUTRyqW6PUOFZbYDLMqzH=s2111)

CloudSpec 是一个开源工具，它使用每个人都能理解的逻辑语言来验证云提供商的资源。通过其相当简单的语法，您可以验证云资源的配置，避免可能导致可用性或保密性问题的错误。

**简介**

借助 CloudSpec，您可以验证云提供商的资源。资源可以是任何东西，从 EC2 实例到 SES 规则。CloudSpec 提供者实现的任何东西。

资源有属性和关联。属性定义资源的形状或配置，而关联定义它与其他资源的关系。使用 CloudSpec，您不仅可以验证资源的配置，还可以验证其相关资源的配置。例如，让我们以一个 EC2 实例为例。它有定义其形状的属性，如其唯一的实例 ID、名称、类型等。但是它也有关联，比如它所属的子网、它所连接的 EBS 卷、它所使用的 AMI 等等。您不仅可以验证 EC2 实例是否属于特定的实例类型，或者是否启用了删除终止标志，还可以验证其附加卷的大小、其子网的 CIDR 块或其关联资源中的任何其他属性，或者其关联资源的关联资源，等等。你跟着我。

你的云资源纠缠在一起，产生了一个图。一个图表，您可以根据您的最佳实践或法规遵从性策略来遍历和验证您认为合适的图表。这种能力，加上它的逻辑语言，就是 CloudSpec 的美妙之处。

**设置 aws:regions = ["us-east-1 "，" eu-west-1"]
use "。/my_module" as my_module
规则 aws 上的“bucket 必须启用访问日志”
:S3:bucket
assert access _ logs is enabled
end rule
规则“实例必须使用‘GP2’卷，并且至少有 50GiBs 大。”
在 aws 上:ec2:实例
，标签["环境"]等于"生产"
断言设备(
>)卷(
类型等于" gp2】，
大小 gte 50
)
)
结束**

您可以在 CloudSpec 参考文档中找到完整的语法。

**供应商**

CloudSpec 本身不支持任何资源。CloudSpec 的核心是规范文件的语法解释器及其验证引擎。然而，CloudSpec 确实使用了提供者，它们是 CloudSpec 的扩展，支持每种不同类型的资源。

提供者定义每个资源类型的形状、属性和关联，以及加载这些资源的逻辑。

您可以在 CloudSpec 参考文档中找到可用的提供者和他们提供的资源。

**运行 CloudSpec docker 镜像**

您可以自己构建并运行 CloudSpec jar，也可以直接从 docker Hub 注册表运行最新的 Docker 映像。

要使用 Docker 映像，您首先需要将您的规范文件(例如`**specs/my_module**`)放在一个目录中，以便将其安装到 Docker 容器中。否则，CloudSpec 将无法打开容器外部的规范文件。

**export AWS _ ACCESS _ KEY _ ID = * export AWS _ SECRET _ ACCESS _ KEY = *
export AWS _ REGION = eu-west-1
docker run-v "/my _ module:/my _ module "-e AWS _ ACCESS _ KEY _ ID-e AWS _ SECRET _ ACCESS _ KEY-e AWS _ REGION efoncuberta/cloudspec run-d my _ module**

如果您在 AWS 中运行 docker 容器并附加了一个专用的 IAM 角色，那么您可以省略 AWS 环境变量。

有关 CloudSpec 命令的更多选项，请参见帮助:

**坞站运行无孔不入/cloudspec**h

**构建 CloudSpec**

如果您想自己构建 CloudSpec，请遵循以下说明。

要求:

*   饭桶
*   maven3
*   OpenJDK 8
*   码头工人

提取源代码并构建 CloudSpec:

**克隆 git repo
git 克隆 https://github.com/efoncubierta/cloudspec
CD cloud spec
构建 CloudSpec
mvn 全新安装
运行 cloud spec
Java-jar runner/target/cloud spec-$ { VERSION }。jar -h**

[**Download**](https://github.com/efoncubierta/cloudspec)