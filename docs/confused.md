# 混淆:检查依赖性混淆漏洞的工具

> 原文：<https://kalilinuxtutorials.com/confused/>

[![Confused : Tool To Check For Dependency Confusion Vulnerabilities](img/01871438050ddf42bb0f5c8c1dc87a2c.png "Confused : Tool To Check For Dependency Confusion Vulnerabilities")](https://1.bp.blogspot.com/-LCGPt2tLpDQ/YFGmtT5g9OI/AAAAAAAAIkg/3dkuSFPmjTAasWuwP9r8L5wX6UVHtUe0gCLcBGAsYHQ/s728/Confused%25281%2529.png)

**迷糊**是一个为 Python (pypi) `**requirements.txt**`、JavaScript (npm) `**package.json**`、PHP (composer) `**composer.json**`或 MVN (maven) **`pom.xml`的依赖配置中引用的私有包名检查逗留自由命名空间的工具。**

这是怎么回事？

2021 年 2 月 9 日，安全研究员 Alex Birsan [发表了一篇文章](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610),触及了多种编程语言生态系统中存在的依赖管理工具中不同的解决顺序缺陷。

微软[发布了一份白皮书](https://azure.microsoft.com/en-gb/resources/3-ways-to-mitigate-risk-using-private-package-feeds/)描述了减轻影响的方法，而根本原因仍然存在。

**解释工具输出**

简单地通读一个应用程序的依赖定义文件，并检查该文件中每个依赖条目的公共包存储库。它将继续报告所有在公共存储库中找不到的包名——这种状态意味着一个包可能容易受到这种攻击，而这个向量还没有被利用。

然而，这并不意味着应用程序没有被积极开发。如果您知道您的软件正在使用私有包存储库，那么您应该确保您的私有包的名称空间已经被一个可信任的团体(通常是您自己或您的公司)所声明。

**已知误报**

像 npm 这样的一些包装生态系统有一个称为“范围”的概念，它可以是私有的，也可以是公共的。简而言之，它意味着一个名称空间有一个更高的层次——作用域。作用域本身并不是公开可见的，这意味着`confused`无法可靠地检测到它是否已被声明。如果您的应用程序使用限定了作用域的包名，您应该确保一个可信方已经在公共存储库中声明了作用域名称。

**安装**

*   [从](https://github.com/visma-prodsec/confused/releases/latest)[发布页面](https://github.com/visma-prodsec/confused/releases/latest)下载一个预构建的二进制文件，解压并运行！*或*
*   如果你安装了最新的 go 编译器:`go get -u github.com/visma-prodsec/confused`(同样的命令用于更新)*或*
*   git 克隆[https://github.com/visma-prodsec/confused](https://github.com/visma-prodsec/confused)；cd 迷茫；去拿；去建吧

**用途**

**用法:**
。/confused[-l language name]depfilename . ext

**的用法。/糊涂:**
-l 串
包库系统。可能值:" pip "、" npm "、" composer "、" mvn "(默认为" npm")
-s string
以逗号分隔的已知安全名称空间列表。支持通配符
-v 详细输出

**例子**

**Python (PyPI)**

**。/confused-l pip requirements . txt

发现问题，以下软件包在公共软件包库中不可用:
[！] internal_package1**

**JavaScript (npm)**

。/confused -l npm package.json
发现问题，以下软件包在公共软件包库中不可用:
[！]internal_package1
[！]@ my company/internal _ package 1
[！]@mycompany/internal _ package 2
#示例当@ my company 私有作用域已经在 npm 中注册，使用-s
。/confused-l NPM-s ' @ my company/* ' package . JSON
发现问题，以下软件包在公共软件包库中不可用:
[！]internal_package1

**梅文(mvn)**

**。/confused -l mvn pom.xml

发现问题，以下软件包在公共软件包库中不可用:
[！]内部
[！]内部/package1
[！]internal/_package2**

[**Download**](https://github.com/visma-prodsec/confused)