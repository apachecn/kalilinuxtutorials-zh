# Natlas:缩放网络扫描

> 原文：<https://kalilinuxtutorials.com/natlas/>

[![Natlas : Scaling Network Scanning](img/8fa80826474876fa4716892c5470a63f.png "Natlas : Scaling Network Scanning")](https://1.bp.blogspot.com/-CiXPEAVFCv0/XxRF0ilp6sI/AAAAAAAAG9A/4-h4FvTUf7kh7eLKWHwOKjb8R-zoFHk5wCLcBGAsYHQ/s1600/natlas%25281%2529.png)

你有很多地图，它们变得很难控制。你是做什么的？你把它们放进一本书里，称之为地图册。就像那样，除了它是一个网站，它是一个 nmaps 的集合。Natlas 服务器同时也是代理的任务管理器，允许你在一个集中的地方控制扫描范围。

**入门**

要开始部署您自己的 Natlas，您至少需要一台服务器和一个代理。最快的方法是在服务器所在的主机上运行代理。服务器和代理的安装说明在其相关的阅读材料中链接如下。

截至 2020 年 6 月 15 日，natlas 已转向仅 docker 部署模式。下载和运行 docker 容器的说明可以在下面链接的相应组件自述文件中找到。

要开始开发，请参见[项目设置](https://github.com/natlas/natlas/blob/main/CONTRIBUTING.md#project-setup)。

**纳特拉斯-服务器**

natlas-server 是存储数据的地方，web 界面的存在使您可以搜索数据。

你可以在 [natlas-server/README.md](https://github.com/natlas/natlas/blob/main/natlas-server/README.md) 上阅读更多关于设置和运行服务器的信息

**纳特拉斯-代理人**

natlas-agent 从服务器获取工作并实际执行扫描。

您可以在 [natlas-agent/README.md](https://github.com/natlas/natlas/blob/main/natlas-agent/README.md) 上阅读有关设置和运行代理的更多信息

**投稿**

请查看[投稿](https://github.com/natlas/natlas/blob/main/CONTRIBUTING.md)，了解如何向 natlas 投稿的指南。

**行为准则**

本项目努力遵守 [CODE_OF_CONDUCT.md](https://github.com/natlas/natlas/blob/main/CODE_OF_CONDUCT.md) 中概述的行为准则。投稿前请阅读行为准则。

**安全**

关于该项目的安全报告指南以及安全相关功能的信息在 [SECURITY.md](https://github.com/natlas/natlas/blob/main/SECURITY.md) 中进行了概述

**致谢**

*   [Pinguino](http://www.pinguinokolb.com/)–创建了纳特拉斯标志/品牌。
*   迪安·皮尔斯(Dean Pierce)——创建了最初的项目 nweb，Natlas 就是在这个项目中建成的。
*   top her Tim Zen–测试、反馈、自动化支持。
*   [Adam Jacques](https://github.com/ajacques)——帮助研究弹性搜索理论，并帮助提高代码质量
*   [Ross Snider](https://github.com/rosswsnider)–为目标选择编写循环 PRNG
*   做出贡献的每一个人。

**免责声明**

Natlas 是一个利用许多其他开源项目的平台，其中许多项目都有自己的许可证。Natlas 没有声称对其使用的任何项目拥有所有权，也不代表任何上述项目。就 Natlas 作者所知，在 Natlas 平台中使用这些工具并没有违反任何许可。Natlas 是一个免费的开源项目，它不从其他开源工具的使用中获得任何收入，也不寻求获得任何收入。

有关许可的进一步询问，请参见各自项目的许可。

[**Download**](https://github.com/natlas/natlas)