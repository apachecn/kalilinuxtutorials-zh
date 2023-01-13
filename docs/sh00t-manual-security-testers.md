# Sh00t:人工安全测试人员的测试环境

> 原文：<https://kalilinuxtutorials.com/sh00t-manual-security-testers/>

**Sh00t** 是人工安全测试人员的测试环境。安全测试不是右键>扫描那么简单。这是一场棘手的比赛。

如果你错过了测试这一件事，以后会后悔吗？Sh00t 是一个高度可定制的智能平台，它了解 bug 猎人的生活，并强调手动安全测试。

*   是一个任务管理器，让您专注于执行安全测试。
*   提供测试用例的**待办事项**清单
*   使用可定制的错误模板帮助创建错误报告

另请参阅: [Kube-Hunter:寻找 Kubernetes 集群中的安全弱点](https://kalilinuxtutorials.com/kube-hunter-security-weaknesses/)

**功能:**

*   动态任务管理器取代简单的编辑器或任务管理工具，不意味着安全
*   自动化、可定制的安全测试案例清单，取代 Evernote、OneNote 或其他非安全工具
*   管理不同用途的自定义错误模板并自动生成错误报告
*   支持多种评估和项目，从逻辑上区分您的不同需求
*   像纸张一样使用——一切都会自动保存
*   将自动生成的错误报告导出到 Markdown &在 HackerOne 上盲目提交！(在制品)
*   与 JIRA 集成，service now–即将推出
*   将错误报告导出到 Markdown–即将推出
*   定制发动机罩下的一切

**安装**:

Sh00t 需要 Python 3 和另外几个包。设置 Sh00t 最简单的方法是使用 Conda 环境。然而，如果你安装了 Python 3 和 pip，Anaconda 是可选的——你可以跳到下面的**步骤 4** 。

**先决条件–一次性设置:**

*   安装 Anaconda 的最小版本: [Miniconda](https://conda.io/miniconda.html) 并遵循[安装说明](https://conda.io/docs/user-guide/install/index.html)。
*   记住要重新加载 bash 概要文件或重启终端应用程序来使用 conda 命令。对于 windows，仅在该窗口中启动`Anaconda Prompt`并运行以下所有命令。
*   创建一个新的 Python 3 环境:`conda create -n sh00t python=3.6`
*   激活 *sh00t* 环境:`conda activate sh00t`。如果看到类似`CommandNotFoundError: Your shell has not been properly configured to use 'conda activate'.`的错误信息，就要手动启用 conda 命令。按照错误消息中显示的说明进行操作。您可能需要重新加载 bash 配置文件或重启终端。再次尝试激活 sh00t】。您应该会在终端上看到`(sh00t) XXXX$`。
*   将最新的项目克隆或下载到您选择的位置:`https://github.com/pavanw3b/sh00t`。`git clone`需要安装 Git。
*   导航到 sh00t 被克隆或下载并解压缩的文件夹:`cd sh00t`。注意，这是项目文件中最外层的 *sh00t* 目录。不是 *sh00t/sh00t* 。
*   安装 Sh00t 依赖包:`pip install -r requirements.txt`
*   设置数据库:`python manage.py migrate`
*   创建用户账号:`python manage.py createsuperuser`按照 UI 创建账号。
*   可选但推荐:Avail 174 安全测试案例来自 OWASP 测试指南(OTG)和 Web 应用黑客手册(WAHH): `python reset.py`。

第一次就这么多。每当您想要启动 Sh00t 时，请遵循以下步骤。

**开始 Sh00t:**

如果你的机器上安装了 Python 3，你可以跳到**步骤 3** 。

1.  对于 Linux/Mac，打开终端。对于 Windows，打开`Anaconda Prompt`。
2.  如果还没有激活 sh00t 环境:`conda activate sh00t`
3.  如果不在 sh00t 目录中，则导航到该目录:`cd sh00t`
4.  启动 Sh00t 服务器:`python manage.py runserver`
5.  在自己喜欢的浏览器上访问 [http://127.0.0.1:8000/](http://127.0.0.1:8000/) 。使用上面一次性设置中创建的用户凭据登录。
6.  欢迎来到 Sh00t！
7.  完成后，停止服务器:`Ctrl + C`
8.  [可选]停用 sh00t 环境以继续您的其他工作:`conda deactivate`。

**升级:**

*   导航到克隆 sh00t 的文件夹:`cd sh00t`
*   停止正在运行的服务器:`Ctrl + C`
*   通过 git: `git pull`拉最新的代码库或者从 github 下载源码，替换文件。
*   如果还没有激活 sh00t 环境:`conda activate sh00t`
*   设置任何附加依赖项:`pip install -r requirements.txt`
*   进行最新的数据库更改:`python manage.py migrate`
*   启动服务器:`python manage.py runserver`

**故障排除**:

Sh00t 用 Python 编写，由 Django Web Framework 提供支持。如果你遇到任何错误，谷歌一下错误信息，在大多数情况下会对你有所帮助。如果你不确定，请[在 github](https://github.com/pavanw3b/sh00t/issues/new) 上提交新一期。

**词汇:**

*   **标志:**标志是一个目标。这是一个需要测试的测试用例。标志是根据所选择的测试方法自动生成的。这个漏洞可能会被发现，也可能不会被发现——但是我们的目标是瞄准它。标志包含测试的详细步骤。如果 bug 被确认，那么就叫 sh0t。
*   **Sh0t:**Sh0t 是 bug。通常，Sh0t 包含错误的技术描述、受影响的文件/URL、重现步骤和修复建议。Sh0t 的大部分内容都是一键生成的，只有受影响的参数、步骤等动态内容需要更改。Sh0ts 可以属于评估。
*   **评估:**评估是一种测试性评估。它可以是对一个应用程序、一个程序的评估，取决于用户想要的管理方式。这是项目的一部分。
*   **项目:**项目包含评估。项目可以是你所做事情的逻辑分离。它可以是不同的工作，虫赏金，由你来决定。

**它是如何工作的？**

从创建新的评估开始。选择你想测试的方法。

今天有 330 个测试用例，分成 86 个标志，属于 13 个模块，它们是参照“Web 应用程序黑客手册”测试方法创建的。

模块和标志可以手工挑选和定制。一旦创建了带有标记的评估，现在测试人员必须手动测试它们，或者在扫描仪、工具的帮助下半自动测试，或者根据需要在完成时标记“完成”。

在执行评估时，我们经常会遇到特定于应用程序中特定场景的定制测试用例。任何时候都可以轻松创建新的标志。

只要一个标志被确认为有效的 bug，就可以创建一个 Sh0t。用户可以选择一个最匹配的 bug 模板，sh00t 会根据选择的模板自动填写 bug 报告。

【Sh00t 谁会用？

*   应用安全工程师:测试和漏洞评估
*   虫子赏金猎人
*   独立的安全研究人员
*   蓝队，修复的开发者
*   任何想黑的人

**实施细节:**

*   语言:Python 3
*   框架:Django Web 框架
*   依赖项:Django REST 框架，djnago-tables2:由/requirements.txt 管理
*   UI:引导-响应

**鸣谢:Hari Valugonda，Mohd Aqeel Ahmed，Ajeeth Rakkappan**

[**Download**](https://github.com/pavanw3b/sh00t)