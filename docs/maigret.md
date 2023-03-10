# Maigret : OSINT 用户名检查器

> 原文：<https://kalilinuxtutorials.com/maigret/>

[![Maigret : OSINT Username Checker](img/8c1dacf6be8e8c4e7880c76d49b390a2.png "Maigret : OSINT Username Checker")](https://1.bp.blogspot.com/-nrTD02LmJoY/YG-B0U2ZthI/AAAAAAAAIsc/r08Pngxf2KAxQ7ddQ1DYUp7e6dkrQfikACLcBGAsYHQ/s728/Maigret%25281%2529.png)

目的**Maigret**–**仅通过用户名收集一个人的档案**，检查大量网站上的账户。

这是一款[夏洛克](https://github.com/sherlock-project/)叉，在重度开发下具有很酷的特性。别忘了定期从 repo 更新源代码。

目前支持超过 2000 个网站([完整列表](https://github.com/soxoj/maigret/blob/main/sites.md))，默认情况下，搜索是针对 500 个受欢迎的网站按受欢迎程度降序排列。

**主要特点**

*   个人资料页面解析、[提取](https://github.com/soxoj/socid_extractor)个人信息、到其他个人资料的链接等。
*   通过找到的新用户名进行递归搜索
*   按标签搜索(网站类别、国家)
*   审查和验证码检测
*   非常少的误报

**安装**

**注意** : Python 3.6 以上，需要 pip。

*   **推荐 Python 3.8。**

**包装安装**

**#从 pypi**
pip3 安装 maigret

#或者手动克隆安装
git 克隆 https://github.com/soxoj/maigret&&CD maigret
pip 3 安装。

**克隆存储库**

**git 克隆 https://github . com/soxoj/maigret&&maigr CD**

您可以使用您的一个免费虚拟机，回购将自动克隆:

[![Open in Cloud Shell](img/ebb6cc0760a889d64f02cce548724ee9.png)](https://console.cloud.google.com/cloudshell/open?git_repo=https://github.com/soxoj/maigret&tutorial=README.md)[![Run on Repl.it](img/d9fc1eb7063b39d7984bbf8d2148adeb.png)](https://repl.it/github/soxoj/maigret)[![Open In Colab](img/b1c68d826e306b0535d6565daa2cecb1.png)](https://colab.research.google.com/gist//soxoj/879b51bc3b2f8b695abb054090645000/maigret.ipynb)

**pip 3 install-r requirements . txt**

**使用示例**

**#为克隆回购**
。/maigret . py user

**# for a package**
maigret user

*   **特性**

**#制作 HTML 和 PDF 报告**
maigret 用户–HTML–PDF

**#在标记有照片标签的网站上搜索&约会**
maigret 用户–标记照片标签

**#在所有可用网站上搜索三个用户名**
maigret 用户 1 用户 2 用户 3 -a

运行`maigret --help`以获取参数描述。选项也记录在[Maigret Wiki](https://github.com/soxoj/maigret/wiki/Command-line-options)中。

*   **与 Docker:**

**#手动构建**
码头构建-t mairiet。& &【码头运行 mairie 用户】

**#官方形象**
【码头运行 soxoj/maigret:最新用户

**页面解析演示&递归用户名搜索**

[PDF 报告](https://github.com/soxoj/maigret/blob/main/static/report_alexaimephotographycars.pdf)， [HTML 报告](https://htmlpreview.github.io/?https://raw.githubusercontent.com/soxoj/maigret/main/static/report_alexaimephotographycars.html)

![animation of recursive search](img/8f4d45f79e339481f3561ee818319e30.png)[**Download**](https://github.com/soxoj/maigret)