# PurplePanda:确定不同云内部和跨不同云的权限提升路径

> 原文：<https://kalilinuxtutorials.com/purplepanda/>

[![](img/c99d863bb3cd25f8448a8f16d02db4f6.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiwp2yhjTF-G-C_rfCO8weddV8iuR5qRHF7hsp_UY8eqXPoGB2_vl-ZHiqkaEodC6NPpGDv60BuU-KJH-sjzvNT6BpJAvyHXp9pXs56J-UVrJr_X33PTlSaryUFxlLzIso_oVU_-2YlGZ0ozMMFKP2v1VvKLk5mRJIuScu1BZa3pyu42fGLh-RN20T4/s728/logo%20(1).png)

**PurplePanda** 是一个从不同的云/saas 应用中获取资源的工具，专注于权限，以便**识别云/saas 配置中的权限提升路径和危险权限**。注意 PurplePanda 搜索平台内和跨平台的**权限提升路径**。

名字来源于动物**小熊猫**。这只熊猫吃豌豆，就像紫熊猫一样，可以摄取这些**豌豆**找到的 API 密匙/令牌。颜色改成紫色是因为这个工具主要是为**紫色团队**准备的(因为它对蓝色和红色团队都非常有用**)。**

## 如何使用

`**/intel**`中的每个文件夹定义了一个可以枚举的平台，而**包含一个 README.md 文件，解释如何使用那个特定的模块**。

下载 **Neo4jDesktop** 并创建数据库。然后**将 env 变量`PURPLEPANDA_NEO4J_URL`和`PURPLEPANDA_PWD`** 连同 URL 和密码一起导出到 neo4j 数据库。

如果您想让 **shodan** 与枚举**期间发现的公共 IP 一起使用，请导出一个名为 *SHODAN_KEY* 的 env 变量，该变量带有一个有效的 api 关键字 shodan** 。

然后只需安装并启动程序，指示您要枚举的平台，用逗号分隔，如下所示:

git 克隆 https://github.com/carlospolop/PurplePanda
CD purple panda
python 3-m venv。
source bin/activate
python 3-m pip install-r requirements . txt
export purple panda _ NEO4J _ URL = " bolt://NEO4J @ localhost:7687"
export purple panda _ PWD = " NEO4J _ pwd _ 4 _ purple panda "
python 3 main . py-h # Get help
python 3 main . py-e–Enumerate Google、github、k8s–github-only-org–k8s

PurplePanda 有 **2 种分析模式**:

*   **`-e`** ( *列举*):这是**主节点**，它会尝试收集数据并进行分析。
*   `**-a**` ( *分析*):对提供的凭证进行**快速分析。**

### 视频教程

查看如何使用和检查 PurplePanda 收集的数据:

![](img/9d0bb012eba5cfdfb9a220911e05fbcb.png)

### 对于蓝/紫队

为每个平台使用至少对平台的所有资源具有**管理员读取权限的凭证。这将有助于您准确地看到在每个平台和跨平台的配置中可能被滥用的**特权路径****

### 对于红队

PurplePanda 也是为红队设计的。一般来说，云/saas 平台**不会给每个人读取**平台配置的权限，这就是为什么 PurplePanda 支持**对同一个平台使用几个密钥**，以便尝试用你妥协的所有密钥枚举一切，并对平台的配置有最准确的看法。

## 如何使用数据

**使用`-d`参数**表示一个目录。然后， **PurplePanda 会在这个目录中以`**csv**`格式写下从所有平台获得的信息的几个有趣的分析**。建议是**在那些文件**中找到有趣和意想不到的东西，然后转到**用图表**分析那些有趣的案例。

`**/intel**`中的每个文件夹定义了一个可以被枚举的平台，**包含一个 README.md 文件，解释如何使用那个特定的模块**。而且，每个文件夹还包含一个`**HOW_TO_USE.md**`文件和一个`**QUERIES.md**`文件。

在`**HOW_TO_USE.md**`文件中，您可以找到**个最佳查询来调查如何提升特权**(紫队、蓝队和红队的*)。*

 *在`**QUERIES.md**`文件中你会发现**所有被提议的查询**来更容易地调查数据。

[**Download**](https://github.com/carlospolop/PurplePanda)*