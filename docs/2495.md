# Gitbleed_Tools:用于从镜像 Git 存储库中提取数据

> 原文：<https://kalilinuxtutorials.com/gitbleed_tools/>

[![](img/d8d52b324a4a836d77a5d32e309247a3.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgtuOZDfKsPrsgfhc6HP5zHS73PLMpotchL4YYVZYKEtpVuRH1HiPszfbk2CEo34uMjMQBcswxZqTHWg-EvYLKdKgbD3ZD3PwLy7_BFpeEyMf4Ga0SLYs7V8E5mHuJq_xYOpeTxa4Zqpw23b-F9-eC2O2ghtSVpuo4innIzlO59vIBQMyhI4XQRR5cM/s728/gitbleed_icon%20(1).png)

Gitbleed_Tools ，这个 repo 包含 shell 脚本，可用于下载和分析克隆和镜像 Git 存储库之间的差异。有关 Git 行为中潜在怪癖的更多信息，请访问阅读我们的博客文章。

## 这些脚本是做什么的？

这些脚本将克隆给定 Git 存储库的副本，包括常规克隆和镜像("–mirror ")选项。然后，它将在两者之间创建一个增量，寻找仅在镜像模式下可用的存储库部分。最后，将运行 gitleaks 来查看增量部分中是否存在任何秘密，并将使用“git log”来创建包含提交主体的单个文件，以便可以更容易地分析它们。

请注意，由于该脚本创建了存储库的三个副本，因此可能会消耗大量磁盘空间。

## 范例知识库

您可以在以下两个示例存储库上测试这些工具:

*   GB _ test repo _ delete–通过删除提交隐藏秘密的存储库
*   GB _ test repo _ reset–通过“git reset”隐藏秘密的存储库

## 要求

你需要 Git，Python 3。要安装 GitLeaks 和 git-filter-repo。以下是在 MacOS 上安装这些软件的示例:

**brew 安装 git python 3 git leaks git-filter-repo**

## 如何安装和运行

您可以对存储库运行此命令，如下所示:

**git 克隆 https://github . com/night watch cyber security/git bleed _ tools . git
CD git bleed _ tools
。/git bleed . sh https://github . com/night watch cyber security/git bleed _ tools . git 示例**

这将创建一个包含三个子文件夹的示例文件夹:

*   克隆–包含克隆的存储库
*   增量–包含镜像存储库减去“克隆”中的所有提交
*   镜像–包含使用“–mirror”选项克隆的镜像存储库

还创建了三个文件:

*   clone _ hashes . done . txt–克隆存储库中的哈希列表
*   gitleaks . JSON–运行 git leaks 的结果
*   git log . txt–delta 文件夹中的所有提交连接成一个文件

[**Download**](https://github.com/nightwatchcybersecurity/gitbleed_tools)