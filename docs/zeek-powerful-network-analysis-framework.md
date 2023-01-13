# Zeek:一个强大的网络分析框架

> 原文：<https://kalilinuxtutorials.com/zeek-powerful-network-analysis-framework/>

[![Zeek : A Powerful Network Analysis Framework](img/1c423c77d0a0ba47c0e1b16ecc5d1f70.png "Zeek : A Powerful Network Analysis Framework")](https://1.bp.blogspot.com/-hGzXweCjfdg/XZ8CjdJaXwI/AAAAAAAAC4k/qQO_ePuECrocrsZCD_dtRZEh_-T4azwlwCLcBGAsYHQ/s1600/Zeek%25281%2529.png)

Zeek 是一个强大的网络分析框架，与你可能知道的典型 IDS 有很大不同。

**主要特征**

*   **深入分析**它附带了许多协议的分析器，支持应用层的高级语义分析。
*   **适应性强且灵活**其特定于域的脚本语言支持特定于站点的监控策略，这意味着它不限于任何特定的检测方法。
*   **高效**它以高性能网络为目标，用于各种大型站点的运营。
*   **高度状态化**它保存有关其监控的网络的大量应用层状态，并提供网络活动的高级存档。

**又读-[user recon-py:各种网站的用户名识别](https://kalilinuxtutorials.com/userrecon-py/)**

**入门**

找到入门信息的最好地方是我们的网站[www.zeek.org](https://www.zeek.org/)，特别是那里的[文档](https://www.zeek.org/documentation/index.html)部分。在网站上，您还可以找到稳定版本的下载、安装教程以及许多其他有用的资源。

你可以在[新闻](https://github.com/zeek/zeek/blob/master/NEWS)中找到发布说明，在[变化](https://github.com/zeek/zeek/blob/master/CHANGES)中找到所有变化的完整记录。

为了使用来自 it 开发分支的最新代码，克隆主 git 存储库:

**git 克隆–递归 https://github.com/zeek/zeek**

所有[依赖项](https://docs.zeek.org/en/stable/install/install.html#prerequisites)就绪后，构建并安装:

**。/configure&make&sudo make install**

编写您的第一个 Zeek 脚本:

# File "hello.zeek"
事件 zeek_init()
{
打印" Hello World！"；
}

并运行它:

**你好。你好**

要学习更多关于 it 脚本语言的知识，[try.zeek.org](http://try.zeek.org/)是一个很好的资源。

**发展**

它是由其社区在 GitHub 上开发的。我们欢迎投稿。从事像这样的开源项目会是一种令人难以置信的有益体验，并且一点一点地让互联网变得更安全。今天，由于无数的贡献，它被世界各地的大公司、教育和科学机构用于保护他们的网络基础设施。

如果你有兴趣参与，我们在 GitHub [这里](https://github.com/zeek/zeek/issues)收集功能请求和问题，你可能会发现[这些](https://github.com/zeek/zeek/labels/good%20first%20issue)是一个开始的好地方。关于它的发展的更多信息可以在[这里](https://www.zeek.org/development/index.html)找到，关于它的社区和邮件列表(相当活跃)的信息可以在[这里](https://www.zeek.org/community/index.html)找到。

[**Download**](https://github.com/zeek/zeek)