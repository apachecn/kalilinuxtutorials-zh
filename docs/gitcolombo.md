# Gitcolombo:从 Git Repos 中提取和分析贡献者信息

> 原文：<https://kalilinuxtutorials.com/gitcolombo/>

[![](img/e7928b3734eff24016bbff440868d845.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjqT2BxmXdjdz2yRY8xePM4IzJMfnUzuDZC833ehGQ8pAjnmJAp1kfNo-XJc2e1teMWXSIlBSYFsvbfQeYH89WDBNK70SRiJ-zCnKfy9UAp9jFKotULCE5VDD3qzBrQKNxtwOVd89ZvDCcgdGJkBgi4-F9GR07aobTkChZ2MmwRMiWeKTK3BEpKGdzQ/s728/1%20(1).png)

Git colombo 是一个 OSINT 工具，用于从 Git 仓库中提取关于个人的信息:普通的名字、电子邮件、不同(看起来)账户之间的匹配。

### 使用

*   **安装 git**
*   运行:

**来自任何 git url
。/git Colombo . py-u https://github.com/Kalanchyovskaia16/newlps
从目录，递归
。/gitcolombo.py -d ./newlps -r
来自所有 GitHub 个人/组织回购的昵称
。/git Colombo . py–昵称 LubyRuffy**

对于从 Gitlab 和 Bitbucket 组 repos 进行批量克隆，您可以使用 ghorg。

输出:

*   详细的人员信息
    *   名字
    *   电子邮件
    *   作为作者/提交者出现的次数
    *   那个人可以是其他人
*   用于相同名称的电子邮件
*   同一个人的不同名字
*   一般统计

### git 作者和提交者有什么区别？

TL；速度三角形定位法(dead reckoning)

*   作者编写代码(制作补丁)
*   commiter 将它提交给 repo(重写历史，发出拉/合并请求…)

很好的解释:https://stack overflow . com/questions/18750808/difference-between-author-and-committer-in-git

开发人员经常使用一个名称/电子邮件(例如工作帐户)进行不准确的提交，然后更改到右边(例如个人帐户)并进行`**git commit --amend**`，但忘记更改提交的作者。这样我们就可以用它来匹配 git 历史中的名字/邮件。

[**Download**](https://github.com/soxoj/gitcolombo)