# AWSPX:一个基于图形的可视化有效访问工具

> 原文：<https://kalilinuxtutorials.com/awspx/>

[![AWSPX : A Graph-Based Tool For Visualizing Effective Access](img/037fd2226105fcd3b9c0ba1baa519a80.png "AWSPX : A Graph-Based Tool For Visualizing Effective Access")](https://1.bp.blogspot.com/-Lkxu70IOhz0/XojBEjQQGvI/AAAAAAAAF0E/WSHSlgiEgtc6yIfdiSMUNbZt2SvG2bEhACLcBGAsYHQ/s1600/awspx-svg.png)

AWSPX 是一个基于图形的工具，用于可视化 AWS 中的有效访问和资源关系。它解析策略信息以确定*哪些*动作影响*哪些*资源，同时考虑这些动作如何组合以产生攻击路径。

与 Bloodhound 等工具不同，awspx 需要权限才能运行。在没有授予这些特权的情况下，预计它不会有用。

**快速启动**

安装(参见安装)，加载示例数据库，并搜索攻击:

**AWS px db–load-zip sample . zip
AWS px 攻击**

或者在您自己的环境中运行它(在这种情况下，默认包含攻击信息):

**awspx 摄取**

浏览到本地主机，看看你能找到什么！

![](img/13bf628a3cc63795b2cd1b052386b549.png)

**安装**

awspx 需要 Docker。

**git 克隆 git @ github . com:FSecureLABS/AWS px . git
CD AWS px&&。/安装**

**如果开箱后不工作，以下是一些需要检查的事项:**

*   docker 容器运行 Neo4j 数据库，该数据库将 TCP 端口 7687、7373 和 7474 转发到本地主机上的这些相同端口。如果存在现有的 Neo4j 安装(如 BloodHound) `**awspx**`将会失败。在继续之前，您需要禁用此服务。或者，您可以通过编辑`**INSTALL**`来修改网络映射。
*   docker 容器也转发到 TCP 端口 80，导致类似的问题。
*   SELinux 可能会阻止 docker 容器做它需要做的一切。如果您正在运行 SELinux (props)并遇到问题，请检查 SELinux。
*   Docker 对 iptables 进行修改。您可能需要调整 iptables 配置来让 awspx 工作。

**AWS 权限**

可以使用以下 AWS 管理的策略。

*   允许你摄取除了 S3 以外的任何东西。
*   添加`**ReadOnlyAccess**`也摄取 S3 对象(警告:这可能会非常慢)。

**数据收集**

一旦安装了 awspx，您就可以通过运行`**awspx profile --create my-account**`来创建一个概要文件，或者通过在命令行上运行`**awspx ingest**`来调用 ingestor。默认情况下，吸入器将使用名为*默认*的配置文件，除非您使用`**--profile**`指定其他内容:

**awspx 摄取–个人资料我的其他帐户**

如果配置文件*我的其他账户*不存在，系统会提示您输入 AWS 访问密钥 ID 和密码。还会提示您一个输出格式(可以忽略)和一个区域(对于 IAM 不重要，但对于其他服务是必需的)。您也可以使用`**awspx profile**`创建一个不包含任何数据的配置文件:

**awspx 配置文件–创建工作**

提供了更多命令和参数，用于调整摄取和攻击路径计算，以及管理 AWS 配置文件和 Neo4j 数据库。跑`**awspx -h**`和**T1 到**了解更多。

**支持的服务:** IAM、EC2、S3、Lambda

**例题**

**awspx 摄取–个人资料我的帐户–服务 S3**

ingestor 将使用`**my-account**`配置文件仅提取 S3 数据，并将其存储在名为`**my-account.db**`的数据库中。将自动处理基于资源的策略(以及本例中的 Bucket ACLs)。基于标识的策略将被忽略，因为 IAM 已从该服务列表中省略。

**awspx 摄取–配置文件我的帐户–服务 IAM EC2–数据库 db-for-ec2**

ingestor 将使用`**my-account**`配置文件仅提取 IAM 和 EC2 数据，并将其存储在名为`**db-for-ec2.db**`的数据库中。由于 IAM 包括基于身份的策略和承担角色策略文档，此信息将包含在`**db-for-ec2.db**`中

**awspx 摄取–配置文件我的帐户\
–except-类型 AWS::S3::对象\
–except-arns arn:AWS:S3:::breaked-bucket arn:AWS:ec2:eu-west-1:123456789012:instance/I-1234**

awspx 将使用`**my-account**`配置文件提取所有受支持服务的数据，但不会尝试加载 S3 对象。它还将跳过名为`**broken-bucket**`的 bucket 和名为`**i-1234**`的 EC2 实例。在`**lib/aws/resources.py**`中可以找到认可资源类型的完整列表。

**awspx 摄取–剖析我的帐户–跳过攻击**

awspx 将使用`**my-account**`配置文件提取所有受支持服务的数据，但不会计算攻击。这对于大型环境非常有用。稍后可以通过运行`**awspx attacks**`单独计算攻击。

**awspx 攻击——仅攻击作为一个角色创建一个组**

使用当前数据库，awspx 将只计算承担角色并创建组攻击。

**AWS px db–load-zip sample . zip**

awspx 将从示例 ZIP 文件创建一个名为`**sample**`的新数据库。文件必须放在`**/opt/awspx/data**`中，以便 docker 容器可以访问它们。请注意，攻击信息不包含在 zip 数据中。要包含这些信息，必须在加载一个 zip 文件后运行`**awspx attacks**`。

**AWS px db–使用我的其他账户**

awspx 会将数据库切换到`**my-other-account**`。您需要刷新浏览器才能看到更改。

**使用前端**

一旦加载了数据库(提示:通过运行`**awspx db --load-zip sample.zip**`加载示例数据)，您可以通过在浏览器中访问 localhost 来浏览它。

首先，找到您感兴趣的资源(或操作),并查看路径将您带到何处(右键单击资源以显示上下文菜单，左键单击以查看其属性)。

**动作颜色**

*   **动作效果调色板:**
    *   **允许:**绿色边缘
    *   **否认:**红边
    *   **条件:**虚线边缘

*   **动作访问类型调色板:**
    *   **列表:**黄色
    *   **阅读:**粉色
    *   **写:**靛蓝
    *   **标签:**蓝绿色
    *   **权限管理:**紫色

使用由效果和访问颜色(按此顺序)组成的线性渐变直观地表示动作。条件攻击用虚线表示。

**快捷键**

| 钥匙 | 行动 |
| --- | --- |
| Alt + Enter | 重新运行布局 |
| 标签 | 在操作和资源搜索视图之间切换 |
| Ctrl +拖动 | 框选 |
| Ctrl +左键单击 | 切换选择 |
| 删除 | 移除选定的节点 |
| 逃跑 | 关闭属性 |
| Ctrl + C | 复制选择属性(JSON) |
| Ctrl + A | 全选 |
| Ctrl + S | 打开搜索栏 |

[**Download**](https://github.com/FSecureLABS/awspx)