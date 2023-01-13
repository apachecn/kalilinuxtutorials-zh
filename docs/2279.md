# IAM 易受攻击:通过设计 AWS IAM 权限提升游戏场，使用 Terraform 创建您自己的易受攻击对象

> 原文：<https://kalilinuxtutorials.com/iam-vulnerable/>

[![](img/667149dbce5681012cbd7a6173efe0c9.png)](https://blogger.googleusercontent.com/img/a/AVvXsEj-8AeAu4Aq8OkoBWMOZyuqhBekfOlDpWpDtF2TQ7Iv4zNVbwz_ccjio80wSlr5fQnSzQFG5LaYSQm6KNqCKCfHniSGufhgHyDL8BgYUmBySKGXcYzVuWirgN3y7ArRzVI1heFQZVkGkj6UZGvBUAgOuik-UtCTj3eGNlcM9_amxSJz9j4-ECOyRmkR=s500)

**IAM Vulnerable** 是使用 Terraform 创建自己的*Vulnerable by design*AWS IAM 特权升级游乐场..IAM Vulnerable 使用 Terraform 二进制文件和您的 AWS 凭据将 250 多个 IAM 资源部署到您选择的 AWS 帐户中。几分钟内，您就可以开始学习如何识别和利用允许权限提升的易受攻击的 IAM 配置。

**推荐方法**

1.  **选择或创建一个 AWS 帐户**–不要使用包含任何生产资源或敏感数据的帐户。
2.  **创建易受攻击的游乐场**–使用此回购创建 IAM 主体和策略，以支持 31 个独特的 AWS IAM 特权路径。
3.  **做好你的功课**–了解斯潘塞·吉森开创的 21 条独创的私人道路。
4.  **Hacky，hack**–使用 Gerben Kleijn 的指南在你的新操场上练习开发。
5.  **升级**–针对您的新 IAM privesc playground 帐户(即 Cloudsplaining、AWSPX、Principal Mapper、Pacu)运行您的工具。

**快速启动**

这个快速入门概述了一个自以为是的方法，让 IAM 漏洞尽快在您的 AWS 帐户中运行。您可能已经完成了这些步骤中的许多步骤，或者您可能想要调整一些东西来与您当前的配置一起工作。查看该存储库中的其他用例部分，了解一些额外的配置选项。

1.  选择或创建 AWS 帐户。(不要使用拥有任何生产资源或敏感数据的帐户！)
2.  创建一个具有管理访问权限的非 root 用户，您将在运行 Terraform 时使用该用户。
3.  为该用户创建访问密钥。
4.  安装 AWS CLI。
5.  使用新创建的管理员用户作为默认配置文件来配置 AWS CLI。
6.  通过执行`**aws sts get-caller-identity**`，确认您的 CLI 正在按预期运行。
7.  安装 Terraform 二进制文件，并将二进制文件位置添加到您的路径中。
8.  `**git clone https://github.com/BishopFox/iam-vulnerable**`
9.  `**cd iam-vulnerable/**`
10.  `**terraform init**`
11.  (Optional)  `**export TF_VAR_aws_local_profile=PROFILE_IN_AWS_CREDENTIALS_FILE_IF_OTHER_THAN_DEFAULT**`
12.  (Optional)  `**export TF_VAR_aws_local_creds_file=FILE_LOCATION_IF_NON_DEFAULT**`
13.  (Optional)  `**terraform plan**`
14.  `**terraform apply**`
15.  (可选)将 IAM 易受攻击的配置文件添加到 AWS 凭据文件中，并更改帐号。
    *   以下命令会备份您当前的 AWS 凭据文件，然后从 repo 中获取示例凭据文件，并用您的目标帐号替换占位符帐户，最后将所有 IAM 易受攻击的 privesc 配置文件添加到您的凭据文件中，以便您可以使用它们:
    *   `**cp ~/.aws/credentials ~/.aws/credentials.backup**`
    *   `**tail -n +7 aws_credentials_file_example | sed s/111111111111/$(aws sts get-caller-identity | grep Account | awk -F\"** **'{print $4}')/g >> ~/.aws/credentials**`

**清理**

每当您想要删除所有由 IAM 漏洞创建的资源时，都可以运行以下命令:

1.  `**cd iam-vulnerable/**`
2.  `**terraform destroy**`

**刚刚创建了哪些资源？**

Terraform 二进制文件刚刚使用您的默认 AWS 帐户配置文件凭据来创建:

*   **31 个用户、角色和策略**,每一个都有一个独特的利用途径来管理访问游乐场帐户
*   完全实现某些利用途径所需的一些附加用户、组、角色和策略
*   测试其他工具检测能力的一些附加用户、角色和策略

默认情况下，此 Terraform 模块创建的每个角色都可以由您用来运行 Terraform 的用户或角色来承担。

*   如果您想让 Terraform 使用默认配置文件之外的配置文件，或者您想对`**assume_role_policy**` ARN 进行硬编码，请参见其他 [](https://github.com/BishopFox/iam-vulnerable#other-use-cases) 用例。

这个要花多少钱？

在默认配置下部署 IAM vulnerable 不会花费任何成本。请参阅下一节，了解如何启用会产生费用的非默认模块，以及如果部署每个模块，每个模块每月的费用是多少。

**模块化方法**

IAM 将某些易受攻击的资源组合在模块中。有些模块是默认启用的(没有任何成本影响的模块)，其他模块是默认禁用的(如果部署会产生成本的模块)。这样，您可以根据需要启用特定的模块。

例如，当您准备好使用像`**ssm:StartSession**`这样涉及 IAM 之外的资源的利用路径时，您可以通过取消对`**iam-vulnerable/main.tf**`文件中的模块的注释，并重新运行`**terraform apply**`来按需部署和拆除这些资源:

**取消下面四行的注释，创建一个 ec2 实例和相关资源
模块“ec2”{
source =。/modules/non-free-resources/ec2 "
AWS _ assume _ role _ arn =(var . AWS _ assume _ role _ arn！= "" ?var . AWS _ assume _ role _ arn:data . AWS _ caller _ identity . current . arn)
}**

取消对`**ec2**`模块的注释后，运行:

**地形初始化
地形应用**

现在，您已经部署了尝试 SSM 特权路径所需的组件。

**免费资源模块**

在`**free-resources**`内部署任何东西都是免费的:

| 名字 | 默认状态 | 预算造价 | 描述 |
| --- | --- | --- | --- |
| privesc-paths | 使能够 | 没有人 | 包含所有 IAM 权限路径 |
| 工具测试 | 使能够 | 没有人 | 包含评估不同 IAM 特权工具功能的测试用例 |

**非自由资源模块**

部署这些额外的模块会增加成本:

| 名字 | 默认状态 | 预算造价 | 描述 | 要求用于 |
| --- | --- | --- | --- | --- |
| EC2 | 有缺陷的 | 💲
$ 4.50/月 | 创建一个 EC2 实例和一个允许从任何地方使用 SSH 的安全组 | `**ssm-SendCommand**`
`**ssm-StartSession**`
 |
| 希腊字母的第 11 个 | 有缺陷的 | 🙂
每月费用取决于使用情况(费用应该为零) | 创建 Lambda 函数 | `**Lambda-EditExistingLambdaFunctionWithRole**` |
| 胶 | 有缺陷的 | 💲💲💲💲
$ 4/小时 | 创建一个粘合开发端点 | `**Glue-UpdateExistingGlueDevEndpoint**` |
| 著名的专业排版软件 | 有缺陷的 | 还不确定 | 创建 SageMaker 笔记本 | `**sageMakerCreatePresignedNotebookURL**` |
| 云的形成 | 有缺陷的 | 🙂通过 CloudFormation 创建的秘密每月 0.40 美元。对堆栈本身没有或几乎没有影响 | 创建一个 CloudFormation 堆栈，在 secret manager 中创建一个秘密 | `**privesc-cloudFormationUpdateStack**` |

**支持的权限提升途径**

| 路径名 | IAM 易受攻击的配置文件名称 | 需要非默认模块 | 开发参考 |
| --- | --- | --- | --- |
| **类别:其他用户的 IAM 权限** |  |  |  |
| IAM-CreateAccessKey | privesc4 | 没有人 | 🦊嗯，升级很快——Privesc 04
🔒s3cur 3 . it iam vulnerable–第 3 部分 |
| IAM-CreateLoginProfile | privesc5 | 没有人 | 🦊嗯，这种情况升级得很快🔒s3cur 3 . it iam vulnerable–第 3 部分 |
| iam-update log in 设定档 | privesc6 | 没有人 | 🦊嗯，那升级得很快——priv ESC 06
🔒s3cur 3 . it iam vulnerable–第 3 部分 |
| **类别:将角色传递给服务** |  |  |  |
| cloud formation-passexistingletcloudformation | privesc20 | 没有人 | 🦊嗯，升级很快——Privesc 20 |
| code build-CreateProjectPassRole | privesc-codeBuildProject | 没有人 |  |
| 数据管道-passexistingletorewdatapipeline | privesc21 | 没有人 | 🦊嗯，升级很快——Privesc 21 |
| EC2-CreateInstanceWithExistingProfile | privesc3 | 没有人 | 🦊嗯，升级很快——priv ESC 03
🔒s3cur 3 . it iam vulnerable–第 2 部分 |
| glue-PassExistingRoleToNewGlueDevEndpoint | privesc18 | 没有人 | 🦊嗯，升级很快——Privesc 18 |
| lambda-passexistingroletonewlambdateninvoke | privesc15 | 没有人 | 🦊嗯，升级很快——Privesc 15 |
| λ-PassRoleToNewLambdaThenTrigger | privesc16 | 没有人 | 🦊嗯，升级很快——Privesc 16 |
| SageMaker-CreateNotebookPassRole | privesc-sageNotebook | 没有人 | 🦏AWS IAM 权限提升–方法 2 |
| SageMaker-CreateTrainingJobPassRole | 私人培训 | 没有人 |  |
| SageMaker-CreateProcessingJobPassRole | privesc-sageProcessing | 没有人 |  |
| **类别:策略权限** |  |  |  |
| IAM-AddUserToGroup | privesc13 | 没有人 | 🦊嗯，升级很快——Privesc 13 |
| IAM-AttachGroupPolicy | privesc8 | 没有人 | 🦊嗯，升级很快——Privesc 08 |
| iam-阿塔赫里策 | privesc9 | 没有人 | 🦊嗯，升级很快——Privesc 09 |
| IAM-AttachUserPolicy | privesc7 | 没有人 | 🦊嗯，升级很快——Privesc 07 |
| IAM-CreateNewPolicyVersion | privesc1 | 没有人 | 🦊嗯，升级很快——Privesc 01
🔒s3cur 3 . it iam vulnerable–第 1 部分 |
| IAM-PutGroupPolicy | privesc11 | 没有人 | 🦊嗯，升级很快——Privesc 11 |
| iam-putrole 策略 | privesc12 | 没有人 | 🦊嗯，升级很快——Privesc 12 |
| IAM-PutUserPolicy | privesc10 | 没有人 | 🦊嗯，升级很快——Privesc 10 |
| IAM-SetExistingDefaultPolicyVersion | privesc2 | 没有人 | 🦊嗯，升级很快——priv ESC 02
🔒s3cur 3 . it iam vulnerable–第 2 部分 |
| **类别:使用 AWS 服务的权限提升** |  |  |  |
| EC 2 instance connect-SendSSHPublicKey | priesc-instance connect | EC2 |  |
| 云形成-更新堆栈 | priv ESC-cfupdate 堆栈 | 云的形成 |  |
| glue-updateexistingluedevendpoint | privesc19 | 胶 | 🦊嗯，升级很快——Privesc 19 |
| lambda-EditExistingLambdaFunctionWithRole | privesc17 | 希腊字母的第 11 个 | 🦊嗯，那升级很快——特权 17
🔒s3cur 3 . it iam vulnerable–第 4 部分 |
| SageMakerCreatePresignedNotebookURL | priv ESC-sagedate URL | 著名的专业排版软件 | 🦏AWS IAM 权限提升–方法 3 |
| SSM-发送命令 | privesc-ssm-command | EC2 |  |
| SSM 启动会话 | privesc-ssm-session | EC2 |  |
| STS-AssumeRole | privesc-assumerole | 没有人 |  |
| **类别:更新假设策略** |  |  |  |
| IAM-UpdatingAssumeRolePolicy | privesc14 | 没有人 | 🦊嗯，升级很快——Privesc 14 |

**其他用例**

#### 默认–未配置 **`terraform.tfvars` c**

*   使用您的默认 AWS 配置文件进行部署(默认)
*   所有创建的角色都可以由用于运行 Terraform 的主体承担(在您的默认配置文件中指定)

#### 使用非默认的配置文件运行 Terraform

*   将`**terraform.tfvars.example**`复制到`**terraform.tvvars**`
*   取消对行`**#aws_local_profile = "profile_name"**`的注释，并输入您想要使用的概要文件名
*   如果您正在使用一个非默认的概要文件，并且仍然想要使用`**aws_credentails_file_example**`文件，那么您可以使用这个命令来生成一个 AWS 凭证文件，该文件使用您的非默认概要文件名称(Thanks @scriptingislife)
    *   记住用您正在使用的配置文件名替换`**nondefaultuser**`):
    *   `**tail -n +7 aws_credentials_file_example | sed -e "s/111111111111/$(aws sts get-caller-identity | grep Account | awk -F\" '{print $4}')/g;s/default/nondefaultuser/g" >> ~/.aws/credentials**`

#### 使用一个 ARN 而不是调用者作为可以承担新创建角色的主体

*   将`**terraform.tfvars.exampl**e`复制到`**terraform.tvvars**`
*   取消对行`**#aws_assume_role_arn = "arn:aws:iam::112233445566:user/you"**`的注释，并输入您想要使用的 ARN

创建后，每个特权角色将由您指定的主体(ARN)来承担。

#### 在帐户 X 中创建资源，但是使用帐户 Y 中的 ARN 作为可以承担新创建角色的主体

如果您已经配置了承担其他帐户角色的 AWS CLI 配置文件，您将需要指定配置文件名称，并手动指定要用于承担不同角色的 ARN。

在下面的例子中，资源将在绑定到 **`"prod-cross-org-access-role"`、**的账户中创建，但是 Terraform 创建的每个角色都可以由属于另一个账户的`**"arn:aws:iam::112233445566:user/you"**`访问。

**AWS _ local _ profile = " prod-cross-org-access-role "
AWS _ assume _ role _ arn = " arn:AWS:iam::112233445566:user/you "**

[Download](https://github.com/BishopFox/iam-vulnerable)