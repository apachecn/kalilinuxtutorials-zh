# Checkov:防止 Terraform 构建期间的云错误配置

> 原文：<https://kalilinuxtutorials.com/checkov/>

[![](img/6538fd7f12b45f56008d2c96b3faf839.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgvgNI4G-ZJQl3AnVfu40DEG7EKI9pwXcV_HgmRgybszC5iYsKS-ZNh4u4gse-MnjWWa4VM61by_SbbyCvgEIpUIOhjvgoFRzkmUTlySg--AWc-O_oO54kmov6qpT2SuPmj6SrPX-Y9gmsyGR5aXYXgw5R0Bnm2T8ULjDQ4_OPna8H3Gu_VE2nyECd7/s728/checkov_by_bridgecrew%20logo%20(1).png)

Checkov 是一个静态代码分析工具，用于基础设施即代码。

它扫描使用 Terraform、Terraform plan、Cloudformation、AWS SAM、Kubernetes、Helm charts、Kustomize、Dockerfile、Serverless、Bicep 或 ARM 模板调配的云基础架构，并使用基于图形的扫描检测安全性和合规性错误配置。

Checkov 还支持 Bridgecrew，这是一个开发者至上的平台，在整个开发生命周期中编纂和简化云安全。Bridgecrew 识别、修复并防止云资源和基础架构代码文件中的错误配置。

## 特征

*   超过 1000 项内置策略涵盖了 AWS、Azure 和 Google Cloud 的安全性和合规性最佳实践。
*   扫描 Terraform、Terraform Plan、CloudFormation、AWS SAM、Kubernetes、Dockerfile、无服务器框架、Bicep 和 ARM 模板文件。
*   支持基于内存中基于图形的扫描的上下文感知策略。
*   属性策略支持 Python 格式，属性和复合策略支持 YAML 格式。
*   检测 EC2 用户数据、Lambda 环境变量和 Terraform 提供程序中的 AWS 凭据。
*   使用正则表达式、关键字和基于熵的检测来识别秘密。
*   评估 Terraform 提供商设置，以规范通过 Terraform 管理的 IaaS、PaaS 或 SaaS 的创建、管理和更新。
*   策略支持将变量评估为可选的默认值。
*   支持内嵌抑制可接受的风险或误报，以减少重复扫描失败。还支持使用 CLI 进行全局跳过。
*   输出目前以 CLI、CycloneDX、JSON、JUnit XML、SARIF 和 github markdown 的形式提供，并链接到补救指南。

## 截屏

CLI 中的扫描结果

Jenkins 中的预设扫描结果

## 入门指南

### 要求

*   Python >= 3.7(数据类适用于 Python 3.7 以上版本)
*   地形> = 0.12

### 安装

**pip3 安装 checkov**

安装在 Alpine 上:

**pip3 安装–升级 pip & & pip3 安装–升级安装工具
pip3 安装检查**

在 LTS Ubuntu 18.04 上安装:

Ubuntu 18.04 随 Python 3.6 一起发布。安装 python 3.7(从 ppa 存储库中)

**sudo apt 更新
sudo apt 安装软件-属性-通用
sudo add-apt-资源库 PPA:deadssnakes/PPA
sudo apt 安装 python3.7
sudo apt 安装 python 3-pip
sudo python 3.7-m pip install-U****checkov #安装或升级 checkov)**

或者使用自制软件(仅限 MacOS)

**brew 安装 c** heckov

或者

**brew 升级检查**

**启用 bash 自动完成功能**

**来源<(register-python-arg complete checkov)**

### 提升

如果您用 pip3 安装了 checkov

**pip3 install -U checkov**

**pip3 install -U checkov**

**配置输入文件夹或文件**

**checkov–目录/用户/路径/to/IAC/代码**

或者特定的一个或多个文件

**checkov–file/user/TF/example . TF**

或者

**check ov-f/user/cloud formation/example 1 . yml-f/user/cloud formation/example 2 . yml**

或 json 格式的 terraform 计划文件

**terra form init
terra form plan-out TF . plan
terra form show-JSON TF . plan>TF . JSON
checkov-f TF . JSON**

注意:`**terraform show**`输出文件`**tf.json**`将是单行。因此，checkov 会将所有发现报告为第 0 行

**检查:资源:AWS _ S3 _ bucket . customer
File:/TF/TF . JSON:0-0
向导:https://docs.bridgecrew.io/docs/s3_16-enable-versioning**失败:CKV_AWS_21:“确保 S3 桶中存储的所有数据都启用了版本控制”

如果您已经安装了`**jq**`，您可以使用以下命令将 json 文件转换成多行:

' terraform show -json tf.plan | jq '> tf.json

扫描结果将更加用户友好。

**checkov-f TF . JSON
Check:CKV _ AWS _ 21:"确保存储在 S3 桶中的所有数据都启用了版本控制"
资源失败:AWS _ S3 _ bucket . customer
File:/TF/tf1 . JSON:224-268
Guide:https://docs.bridgecrew.io/docs/s3_16-enable-versioning
225 " values ":{
226 " acceleration _ status ":"，
227 "acl": "private "，
222**

或者，使用`**--repo-root-for-plan-enrichment**`标志指定用于生成计划文件的 hcl 文件的 repo 根，以使用适当的文件路径、行号和资源的代码块丰富输出。一个额外的好处是检查抑制将被相应地处理。

**check ov-f TF . JSON–repo-root-for-plan-enrichment/user/path/to/IAC/code**

**扫描结果样本(CLI)**

**检查通过:1，检查失败:1，检查被抑制:0
检查:“确保 s3 存储桶中存储的所有数据在静态时都被安全加密”
/main.tf:
检查资源通过:AWS _ S3 _ bucket . template _ bucket
检查:“确保 S3 存储桶中存储的所有数据在静态时都被安全加密”
/../regionStack/main.tf:
对资源失败:AWS _ S3 _ bucket . SLS _ deployment _ bucket _ name**

**使用 Docker**

**docker pull bridge crew/checkov
docker run–tty–RM–volume/user/TF:/TF–workdir/TF bridge crew/checkov–directory/TF**

注意:如果您使用的是 Python 3.6(Ubuntu 18.04 中的默认版本)，checkov 将无法工作，并且会出现错误消息`**ModuleNotFoundError: No module named 'dataclasses'**`。在这种情况下，您可以使用 docker 版本。

注意，在某些情况下，将`**docker run --tty**`输出重定向到一个文件——例如，如果您想将 Checkov JUnit 输出保存到一个文件——会导致打印额外的控制字符。这可能会破坏文件解析。如果遇到这种情况，请移除 **`--tty`** 标志。

`**--workdir /tf**`标志是可选的，用于将工作目录更改为挂载的卷。如果您正在使用 SARIF 输出`**-o sarif**`，这将输出结果。sarif 文件到挂载的卷中(在上面的例子中是`**/user/tf**`)。如果不包含该标志，工作目录将为“/”。

### 运行或跳过检查

使用命令行标志，您可以指定仅运行命名检查(允许列表)或运行除列出的检查之外的所有检查(拒绝列表)。如果您通过 API 密钥使用平台集成，您还可以指定要跳过和/或包含的严重性阈值。有关这些标志如何一起工作的更多详细信息，请参见文档。

## 例子

只允许运行两个指定的检查:

checkov–目录。–检查 CKV_AWS_20，CKV_AWS_57

运行除指定检查之外的所有检查:

**check ov-d .——跳过检查 CKV_AWS_20**

运行除指定模式检查之外的所有检查:

**checkov-d .——跳过检查 CKV_AWS***

运行所有中等或更高严重性的检查(需要 API 密钥):

**check ov-d .–检查介质–BC-API-key…**

运行所有中严重性或更高严重性的检查，以及检查 CKV_123(假设这是低严重性检查):

**check ov-d .–检查介质，CKV _ 123–BC-API-key…**

跳过所有中严重性或更低严重性的检查:

**check ov-d .–跳过检查介质–BC-API-key…**

跳过所有严重性为中或更低的检查，并检查 CKV_789(假设这是一个高严重性检查):

**checkov-d .–跳过检查介质，CKV _ 789–BC-API-key…**

运行所有中等或更高严重性的检查，但跳过检查 CKV_123(假设这是中等或更高严重性的检查):

**check ov-d .–check MEDIUM–skip-check CKV _ 123–BC-API-key…**

### 抑制/忽略检查

像任何静态分析工具一样，它受到其分析范围的限制。例如，如果手动管理资源，或者使用后续的配置管理工具，抑制可以作为简单的代码注释插入。

#### 抑制注释格式

要跳过对给定 Terraform 定义块或 CloudFormation 资源的检查，请在其范围内应用以下注释模式:

`**checkov:skip=<check_id>:<suppression_comment>**`

*   `**<check_id>**`是【可用的支票扫描仪】(docs/5。政策索引/all.md)
*   `**<suppression_comment>**`是包含在输出中的可选抑制原因

#### 举例

下面的注释跳过了对由`**foo-bucket**`标识的资源的`**CKV_AWS_20**`检查，其中扫描检查 AWS S3 桶是否是私有的。在本例中，存储桶配置了公共读访问权限；添加抑制注释将跳过适当的检查，而不是检查失败。

**resource " AWS _ S3 _ bucket " " foo-bucket " {
region = var . region
# checkov:skip = CKV _ AWS _ 20:bucket 是公共静态内容主机
bucket = local . bucket _ name
force _ destroy = true
ACL = " public-read "
}**

输出现在将包含一个`**SKIPPED**`检查结果条目:

**…
…
检查:“S3 桶定义了一个允许公共访问的 ACL。”
跳过资源:aws_s3_bucket.foo-bucket
抑制注释:bucket 是公共静态内容主机
File:/example _ skip _ ACL . TF:1-25**

为了抑制 Kubernetes 清单中的检查，使用了以下格式的注释:`**checkov.io/skip#: <check_id>=<suppression_comment>**`

例如:

**API version:v1
kind:Pod
元数据:
name: mypod
注释:
checkov.io/skip1: CKV _ K8S _ 20 =我不关心特权升级:-O
checkov.io/skip2: CKV _ K8S _ 14
checkov.io/skip3: CKV _ K8S _ 11 =我没有按照我想要的那样设置 CPU 限制 bestfortion QoS
spec:
容器:
…**

#### 记录

为了详细记录到标准输出，设置环境变量`**LOG_LEVEL**`到`**DEBUG**`。

默认为**T0。**

#### 跳过目录

要跳过文件或目录，请使用参数`**--skip-path**`，该参数可以指定多次。此参数接受相对于当前工作目录的路径的正则表达式。您可以使用它来跳过整个目录和/或特定文件。

默认情况下，所有名为`**node_modules**`、**、`.terraform`、**和`**.serverless**`的目录都将被跳过，此外还有任何以`**.**`开头的文件或目录。取消跳过以`**.**`开头的目录覆盖`**IGNORE_HIDDEN_DIRECTORY_ENV**`环境变量`**export IGNORE_HIDDEN_DIRECTORY_ENV=false**`

您可以通过设置环境变量`**CKV_IGNORED_DIRECTORIES**`来覆盖要跳过的默认目录集。请注意，如果您想要保留该列表并向其中添加内容，则必须包含这些值。例如， **`CKV_IGNORED_DIRECTORIES=mynewdir`** 只会跳过那个目录，而不会跳过上面提到的其他目录。此变量是传统功能；我们建议使用`**--skip-file**`旗。

#### VSCODE 扩展

如果您想在 vscode 中使用 checkov，请尝试在 vscode 中使用 vscode 扩展

### 使用配置文件进行配置

可以使用 YAML 配置文件来配置 Checkov。默认情况下，checkov 按照优先顺序在以下位置查找`**.checkov.yaml**`或`**.checkov.yml**`文件:

*   对其运行 checkov 的目录。(`**--directory**`)
*   调用 checkov 的当前工作目录。
*   用户的主目录。

**注意**:checkov 配置文件的最佳做法是从由经过验证的身份组成的可信来源加载，以便扫描的文件、支票 id 和加载的自定义支票符合要求。

用户也可以通过命令行传递配置文件的路径。在这种情况下，其他配置文件将被忽略。例如:

**checkov–配置文件路径/to/config.yaml**

用户也可以使用 **`--create-config`** 命令创建一个配置文件，该命令获取当前的命令行参数并将它们写到给定的路径中。例如:

**checkov–compact–directory test-dir–docker-image sample-image–DOCKER file-path DOCKER file–download-external-modules True–external-checks–dir sample-dir–no-guide–quiet–repo-id bridge crew/sample-repo–skip-check CKV _ DOCKER _ 3、CKV _ DOCKER _ 2–skip-fixes–skip-框架 DOCKER 文件机密–skip-suppressions–soft-fail–branch develop–check CKV _ DOCKER _ 1–create-config/Users/sample/config . yml**

将创建一个`**config.yaml**`文件，如下所示:

**分公司:开发
检查:**

*   **CKV_DOCKER_1
    紧凑:真实
    目录:**
*   **test-dir
    docker-image:sample-image
    docker file-path:docker file
    download-external-modules:true
    evaluate-variables:true
    外部检查-dir:**
*   **样本目录
    外部模块下载路径:。外部 _ 模块
    框架:**
*   **all
    no-guide:true
    output:CLI
    quiet:true
    repo-id:bridgecrew/sample-repo
    skip-check:**
*   ckv _ docker _ 3
*   **CKV _ 码头 _2
    跳过修复:真
    跳过框架:**
*   **dockerfile**
*   **秘密
    跳过抑制:真
    软故障:真**

用户还可以使用`**--show-config**`标志来查看所有的参数和设置以及它们的来源，即命令行、配置文件、环境变量或默认值。例如:

**checkov–显示配置**

将显示:

**命令行参数:–show-Config
环境变量:
BC_API_KEY: your-api-key
配置文件(/Users/sample/. checkov . yml):
soft-fail:False
branch:master
skip-check:[' CKV _ DOCKER _ 3 '，' CKV_DOCKER_2']
默认值:
–output:CLI
–框架:[' all ']
–下载-外部模块:False【T8 外部模块
–评估变量:真**

[**Download**](https://github.com/bridgecrewio/checkov#enabling-bash-autocomplete)