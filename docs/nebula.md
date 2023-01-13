# 星云:云 C2 框架，目前在 AWS 上提供侦察，枚举，开发，后期开发

> 原文：<https://kalilinuxtutorials.com/nebula/>

[![Nebula : Cloud C2 Framework, Which At The Moment Offers Reconnaissance, Enumeration, Exploitation, Post Exploitation On AWS](img/d8471909a3750d8a9f9012e8f6f2b13b.png "Nebula : Cloud C2 Framework, Which At The Moment Offers Reconnaissance, Enumeration, Exploitation, Post Exploitation On AWS")](https://1.bp.blogspot.com/-IKB5MiOkSbg/YMrsx_usxbI/AAAAAAAAJh8/_IKCmLZw0wIqshMmbhMYV5vlSbWSmIzgQCLcBGAsYHQ/s728/logo%2B%25281%2529.png)

**Nebula** 是一个云和(希望是)DevOps 渗透测试框架。它是用针对每个提供者和每个功能的模块构建的。截至 2021 年 4 月，它仅涵盖 AWS，但目前是一个正在进行的项目，有望继续发展，以测试 GCP、Azure、Kubernetes、Docker 或自动化引擎，如 Ansible、Terraform、Chef 等。

**目前覆盖**

*   S3 桶名 bruteforce
*   IAM、EC2、S3 和λ枚举
*   IAM、EC2 和 S3 剥削
*   自定义 HTTP 用户代理

**目前有 50 个模块涵盖**

*   侦察
*   列举
*   剥削
*   清除

**安装**

**码头工人**

**来自 Dockerhub**

从 Github 克隆 Nebula Repo 并提取 Nebula Docker 图像:

git 克隆 https://github . com/gl4 sses SBO 1/nebula
坞站 gl4 sses SBO 1/nebula:latest

然后通过以下方式运行 main.py:

**docker run-v Nebula:/app-ti GL 4 sesbo 1/Nebula:最新 main.py**

记住不要忘记-v 选项，因为它允许文件保存在系统上，即使在删除 docker 映像之后。

**使用 DockerFile**

从 Github 克隆 Nebula Repo 并在本地构建 Docker 映像:

git 克隆 https://github . com/gl4 sses SBO 1/nebula
dock build-t 星云。

然后通过以下方式运行 main.py:

**docker run-v Nebula:/app-ti Nebula main . py**

记住不要忘记-v 选项，因为它允许文件保存在系统上，即使在删除 docker 映像之后。

**安装在系统上**

Nebula 在 python3.8 编码，在 python3.8 和 3.9 上测试。它使用 boto3 库来访问 AWS。要安装，只需安装 python 3.8+并安装 *requirements.txt* 中所需的库

**python 3.8-m pip install-r requirements . txt**

然后安装会话管理器插件。这是 SSM 模块所需要的:

**curl " https://S3 . Amazon AWS . com/session-manager-downloads/plugin/latest/Ubuntu _ 64 bit/session-manager-plugin . deb "-o " session-manager-plugin . deb "
dpkg-I session-manager-plugin . deb**

在 windows 设备上，由于 less 没有安装，我从得到了一个，预构建的二进制文件保存在 less_binary 目录下。只需将该目录添加到 PATH 环境变量中，就可以了。

然后只需运行 *main.py*

**python3.8。/main.py**

**用途**

**python3.9.exe。\ main . py-b
————————
50 AWS 0 GCP 0 azure 0 office 365
0 docker 0 kubernetes
——————————
50 模块 2 清理 0 检测
41 enum 6 利用 0 持久性
0 监听者 0 横向移动 0 检测旁路
0 特权 1 侦察 0 stager**

**帮助**

运行 *help* 命令，会给你一个可以使用的命令列表:

**()()(AWS) > > >帮助
帮助命令:描述:
——————————
帮助显示所有命令的帮助
帮助凭证显示帮助凭证
帮助模块显示模块帮助
帮助工作区显示凭证帮助
帮助用户代理显示凭证帮助
模块命令描述
——————————
显示模块列表所有模块
显示枚举列表所有枚举模块
显示漏洞列表全部 模块
显示权限列表所有权限提升模块
显示侦察列表所有侦察模块
显示监听列表所有侦察模块
显示清理列表所有枚举模块
显示检测列表所有利用模块
显示检测绕过列表所有持久模块
显示 lateralmovement 列表所有权限提升模块
显示 stager 列表所有侦察模块
使用模块使用模块。
选项显示您选择的模块的选项。
运行运行您选择的模块。通过模式搜索一个模块。例如:“搜索 S3”
返回取消选择模块
设置模块的设置选项。需要先使用模块。
未设置模块的未设置选项。需要先使用模块。
用户代理命令描述
————————————
设置用户代理 windows 设置 windows 客户端用户代理
设置用户代理 linux 设置 linux 客户端用户代理
设置用户代理自定义设置自定义客户端用户代理
显示用户代理显示当前用户代理
取消设置用户代理使用 boto3 生成的用户代理
工作区命令描述
———————————【T38**

**模块**

**列表模块**

您可以列出所有模块或特定模块:

**()()(AWS) > > >显示模块
clean up/AWS _ iam _ Delete _ access _ key 通过提供
来删除用户的访问密钥。
clean up/AWS _ iam _ Delete _ log in _ profile 删除用户对管理
控制台
的访问权限 enum/aws_ec2_enum_elastic_ips 列出所提供实例的用户数据。
需要可以访问它的 IAM 的密钥和访问密钥
。
enum/aws_ec2_enum_images 列出所有 ec2 图像。需要具有描述图像权限的
IAM 的凭据。输出被转储到一个文件中。不幸的是，这要花很多时间。好家伙，这是一个
巨大的输出。
enum/AWS _ ec2 _ enum _ Instances 描述实例属性:实例、VCP、
区域、映像、安全组、快照、子网、标签、
卷。需要 IAM 的密钥和访问密钥，并且
有权访问所有或任何 API 调用:
描述可用性区域、描述图像、
描述实例、描述密钥对、描述安全组、
描述快照、描述子网、描述标签、
描述卷、描述个人计算机**

就像这样，你可以使用:

**显示模块**

**显示枚举**

**展示功勋**

**显示持久性**

**show privesc**

**显示侦察**

**显示收听者**

**显示清理**

**显示检测**

**显示检测旁路**

**显示侧向移动**

**表演舞台演员**

**搜索模块**

使用**搜索**命令搜索带有特定单词的模块:

**)()(AWS) > > >搜索实例
enum/aws_ec2_enum_instances 描述实例属性:实例、VCP、
区域、映像、安全组、快照、子网、标签、
卷。需要 IAM 的密钥和访问密钥，
有权访问所有或任何 API 调用:
describevailabilityzones，DescribeImages，
DescribeInstances，DescribeKeyPairs，DescribeSecurityGroups，
DescribeSnapshots，DescribeTags，
DescribeVolumes，describevcs
enum/AWS _ IAM _ List _ instance _ profiles 列出所有实例概要文件。
exploit/AWS _ ec2 _ create _ instance _ with _ user _ data 您必须在
IAM 中以 JSON 格式提供策略。然而，对于以
YAML 格式的 AWS CloudFormation 模板，您可以提供 JSON 或 YAML 格式的策略。AWS
CloudFormation 总是在将 YAML 策略提交给 IAM 之前将其转换为 JSON 格式
。
()()(AWS)>>>**

**使用模块**

要使用一个模块，只需键入*使用*和模块的名称。3 个括号将有模块的名称。

**((work 1)()(enum/AWS _ ec2 _ enum _ instances)>>>使用模块 enum/AWS _ iam _ get _ group
(work 1)()(enum/AWS _ ec2 _ enum _ instances)>>>**

**选项**

使用*选项*，我们可以列出模块上的信息:

**(work 1)()(enum/AWS _ ec2 _ enum _ Instances)>>>选项
描述:
描述实例属性:实例、VCP、区域、映像、安全组、快照、子网、标记、卷。需要能够访问所有或任何 API 调用的 IAM 的密钥和访问密钥:描述可用性区域、描述图像、描述实例、描述密钥对、描述安全组、描述快照、描述子网、描述标记、描述卷、描述 pcs
作者:
姓名:gl4 sesbo 1
推特:https://twitter.com/gl4ssesbo1
github:https://github.com/gl4ssesbo1
博客:https://www.pepperclipp.com/
AWS CLI 命令:
AWS ec2 describe-describe 这是无法改变的。
INSTANCE-ID:
必选:false
说明:要枚举的实例的 ID。如果未提供，将枚举所有实例。
(work 1)()(enum/AWS _ ec2 _ enum _ instances)>>>**

要设置选项，使用*设置*和选项名称:

**(work 1)()(enum/AWS _ ec2 _ enum _ Instances)>>>set INSTANCE-ID 1234
(work 1)()(enum/AWS _ ec2 _ enum _ Instances)>>>options
description:
描述实例属性:实例、VCP、区域、映像、安全组、快照、子网、标记、卷。需要能够访问所有或任何 API 调用的 IAM 的密钥和访问密钥:描述可用性区域、描述图像、描述实例、描述密钥对、描述安全组、描述快照、描述子网、描述标记、描述卷、描述 PC
作者:
姓名:GL 4 sesbo 1
推特:https://twitter.com/gl4ssesbo1
github:https://github.com/gl4ssesbo1
博客:https://www.pepperclipp.com/
需要凭据:True
AWSCLI 命令:【t 这是无法改变的。
INSTANCE-ID: 1234
必选:false
描述:要枚举的实例的 ID。如果未提供，将枚举所有实例。
(work 1)()(enum/AWS _ ec2 _ enum _ instances)>>>**

使用**取消设置**也可以取消设置它们。

**(work 1)()(enum/AWS _ ec2 _ enum _ instances)>>>unset INSTANCE-ID
(work 1)()(enum/AWS _ ec2 _ enum _ instances)>>>**

**运行模块**

要运行该模块，如果它需要凭据，您需要导入一组具有运行该模块所需权限的凭据。这在模块的选项上显示为:

**需要凭证:真**

要运行它，只需输入 **run** 。根据输出，它要么显示一个不完整的视图，要么直接打印出来。分页，使用较少的二进制，其中对于 Windows 使用来自【https://github.com/jftuga/less-Windows】[**的二进制。exe 的副本在 less_binary 目录中。输出也保存在工作空间目录下的文件中:**](https://github.com/jftuga/less-Windows)

 ****(work 1)()(enum/AWS _ ec2 _ enum _ instances)>>>运行
[*]内容转储到文件上’。/work spaces/work 1/16 _ 04 _ 2021 _ 18 _ 16 _ 48 _ ec2 _ enum _ instances。**

**凭证**

# # # #输入凭据 Nebula 可以使用 AccessKeyID + SecretKey 组合和 access keyid+secret key+session key 组合来验证基础架构。要插入一组凭据，请使用:

**()()(AWS)>>>set credentials test1
Profile Name:test1
Access Key ID:A*2 Secret Key ID:a7
Region:us-west-3
你也有会话令牌吗？【是/否】* 【凭证设置】。请使用“显示凭据”来检查它们。
[*]当前凭据配置文件设置为“test1”。使用“显示当前信用”来检查它们。**

你会得到一些允许你设置它们的输入。当输入凭证时，可以通过输入 **y** 来添加会话令牌，当被问到**你也有会话令牌吗？【是/否】**。

# # # #使用凭据要使用另一个凭据，只需输入:

**()()(AWS) > > >使用凭据 test1
[*]当前凭据配置文件设置为“test1”。使用“显示当前信用”来检查它们。**

# # # #当前凭据当您输入凭据时，它们会自动成为当前凭据，即您将用来进行身份验证的凭据。要检查当前凭据，请使用:

**()()(AWS)>>>show current-creds
{
【个人资料】:" test1 "，
" access _ key _ id ":" A*2 ", " secret _ key ":" A **7 ",
" region ":" us-west-3 "
}**

# # # #删除凭据如果您不想要凭据，可以使用以下方法删除它们:

**()()(AWS) > > >删除凭据 test1
您将要删除凭据“test1”。你确定吗？[y/N] y**

# # # #转储和导入凭据如果您希望将凭据保存在计算机上，可以使用:

**()()(AWS) > > >转储凭证
[*]凭证转储到文件上’。/credentials/16 _ 04 _ 2021 _ 17 _ 37 _ 59 '。**

并且它们将被保存在包含转储到目录*上的时间和日期的文件中，凭证*在 Nebula 目录上。要导入它们，只需输入:

**()()(AWS) > > >导入凭证 16 _ 04 _ 2021 _ 17 _ 37 _ 59
()()(AWS)>>>显示凭证
[
{
"profile": "test1 "，
" access _ key _ id ":" A*2 "" secret _ key ":" A *【T7 ",
" region ":" us***

**工作区**

Nebula 使用工作空间来保存每个命令的输出。输出保存为 json 数据(s3_name_fuzzer 除外，它保存为 XML)在目录 *workspaces* 上创建的文件夹中。

**创建工作区**

要创建一个，请输入:

**()()(AWS) > > >创建工作空间 work1
[ *]工作空间‘work 1’已创建。[* ]当前工作区设置为“工作 1”。
(work 1)()(AWS)>>>ls。/workspaces
目录:C:\ Users * * * \ Desktop \ Nebula \ work spaces
模式 LastWriteTime 长度名称
————————————
d——–4/16/2021 下午 5:42 工作 1
-a——-4/16/2021 下午 4:40 0 0 init . py**

创建后，第一个括号将包含您正在工作的工作空间的名称。如果您想使用现有的工作空间，只需键入:

**()()(AWS) > > >使用工作空间 work 1
(work 1)()(AWS)>>**

需要使用工作区，因此即使您目前没有使用任何工作区，在运行模块时，它也会要求您使用随机名称创建一个工作区，或者自己创建一个自定义名称的工作区。

**()()(enum/AWS _ ec2 _ enum _ instances)>>>运行
未配置工作区。将创建工作站“qxryiuct”。你确定吗？[y/N] n
[*]首先使用“创建工作站”创建一个工作站。
()()(enum/AWS _ ec2 _ enum _ instances)>>>**

**列出工作区**

要获取工作区列表，请使用:

**(work 1)()(enum/AWS _ ec2 _ enum _ instances)>>>显示工作区
工作区:
work 1
(work 1)()(enum/AWS _ ec2 _ enum _ instances)>>>**

**移除工作区**

要删除工作区，请输入:

**()()(AWS) > > >删除工作空间 work1
[*]确定要删除工作空间吗？【y/N】y
()()(AWS)>>>显示工作区
工作区:
()()(AWS) > > >**

**用户代理**

用户代理可以设置为 linux 代理、windows 代理或自定义代理。要显示它们，只需使用 *show* 即可。

**()()(AWS) > > >设置用户代理 linux
用户代理:boto 3/1 . 9 . 89 Python/3 . 8 . 1 Linux/4 . 1 . 2-34-generic 被设置
()()(AWS) > > >显示用户代理
[ *]用户代理为:boto 3/1 . 9 . 89 Python/3 . 8 . 1 Linux/4 . 1 . 2-34-generic > > >设置用户代理自定义
输入您想要的用户代理:sth
用户代理:sth 被设置
()()(AWS) > > >显示用户代理
[*]用户代理是:sth
()()(AWS)>>>***

要取消设置用户代理，请输入:

**()()(AWS) > > >未设置用户代理
[*]用户代理设置为空。**

它将拥有系统的用户代理。

[**Download**](https://github.com/gl4ssesbo1/Nebula)**