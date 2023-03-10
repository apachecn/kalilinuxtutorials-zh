# RepoPeek:一个 Python 脚本，无需克隆即可获得关于存储库的详细信息

> 原文：<https://kalilinuxtutorials.com/repopeek/>

[![RepoPeek : A Python Script To Get Details About A Repository Without Cloning](img/e76b8a5944a505d7f18a56067d825edc.png "RepoPeek : A Python Script To Get Details About A Repository Without Cloning")](https://1.bp.blogspot.com/-hTa6SeWIQHk/XtSUqyAcpPI/AAAAAAAAGhk/v_SgyiziF5ol2g382XToucCHYHV0qPx7ACLcBGAsYHQ/s1600/RepoPeek.gif)

**RepoPeek** 是一个 Python 脚本，用于获取关于存储库的详细信息，而无需克隆它。使用 [GitHub API](http://developer.github.com/v3/repos/) 检索所有信息。

**注意:**此模块发出的 API 请求没有使用基本认证或 OAuth。因此，速率限制允许每小时最多 60 个请求。未经身份验证的请求与原始 IP 地址相关联。

**提供的信息**

1.  **关于存储库的基本信息。**
    *   存储库名称
    *   默认分支
    *   储存库大小
    *   存储库许可证
    *   知识库描述
    *   存储库类型
2.  **存储库中使用的语言。**
3.  **知识库统计。**
    *   叉
    *   观察者
    *   开放的问题
    *   总星级
4.  **存储库的 URL。**
    *   GIT URL
    *   SSH URL
    *   SVN 网址
    *   克隆 URL
5.  **提交存储库的详细信息**
    *   上次提交日期
    *   上次提交消息

**也可阅读-[极简攻击性安全工具](https://kalilinuxtutorials.com/minimalistic/)**

**安装**

要安装这个脚本，以便可以从任何地方通过 Python 访问它，请将脚本复制到您选择的目录中，然后将该目录添加到您的`**PYTHONPATH**`

**用途**

**python -m repopeek**

[**Download**](https://github.com/sameera-madushan/RepoPeek)