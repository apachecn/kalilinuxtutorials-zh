# DeimosC2:一个用于后期开发的 Golang 命令和控制框架

> 原文：<https://kalilinuxtutorials.com/deimosc2/>

[![DeimosC2 : A Golang Command & Control Framework For Post-Exploitation](img/7927c017e35832085d988563801ae391.png "DeimosC2 : A Golang Command & Control Framework For Post-Exploitation")](https://1.bp.blogspot.com/-iyp_FlNLZU8/XyyCaCUnfyI/AAAAAAAAHQI/cpMmr9x8eEY3dxN9dkWUIkN1b3g60x92QCLcBGAsYHQ/s728/c2%25281%2529.png)

**DeimosC2** 是一个利用后命令&控制(C2)工具，它利用多种通信方法来控制已经被入侵的机器。

DeimosC2 服务器和代理可以在 Windows、Darwin 和 Linux 上运行，并且已经过测试。完全用 [Golang](https://golang.org/) 写，前端用 [Vue.js](https://vuejs.org/) 写。

**监听器功能**

*   每个侦听器都有自己的 RSA Pub 和私钥，用于包装加密的代理通信。
*   动态生成代理
*   与其相关联监听器和代理的图形地图

**代理功能**

*   提供高级概述的代理列表页面
*   代理交互页面包含代理的信息，能够对代理运行作业，文件浏览器，loot 数据，并能够添加评论

**支持的代理**

*   传输控制协议（Transmission Control Protocol）
*   HTTPS
*   DoH(HTTPS 域名系统)
*   QUIC
*   以 TCP 为中心

**前端功能**

*   具有管理员和用户角色的多用户支持
*   与听众和代理的图形和可视化交互
*   密码长度要求
*   使用 Google MFA 的 2FA 认证
*   Websocket API 调用

**入门和帮助**

你可以下载最新的[版本](https://github.com/DeimosC2/DeimosC2/releases)并查看 [wiki](https://github.com/DeimosC2/DeimosC2/wiki) 以获得任何关于开始或运行 C2 的帮助。

**提交问题**

我们欢迎开放的问题，以帮助改善这个项目，让它继续下去。对于 bug 请使用[模板](https://github.com/DeimosC2/DeimosC2/blob/master/.github/ISSUE_TEMPLATE/bug_report.md)。

**作者**

*   Chase Dardaman ( [@CharlesDardaman](https://twitter.com/CharlesDardaman) )
*   昆汀·罗德-埃雷拉( [@paragonsec](https://twitter.com/paragonsec) )
*   埃尔韦拉·谢娜( [developeruz](https://github.com/developeruz)
*   blase Brignac([@ Blaise Brignac](https://twitter.com/BlaiseBrignac))

**学分**

为了开发这个，我们使用了一些其他人的优秀作品。下面是我们使用过他们的代码或者受到他们启发的人的列表。如果我们错过了你，请让我们知道，以便我们可以添加你的名字！

*   [lsassy](https://github.com/Hackndo/lsassy)by[@ hack Ando](https://twitter.com/HackAndDo)用于部分 Windows 模块
*   [goDoH](https://github.com/sensepost/goDoH) 作者 [@leonjza](https://twitter.com/leonjza) 来自 SensePost 用于 DoH
*   一些地方使用毕肖普福克斯银，因为他们已经做了一项统计工作
*   [Merlin](https://github.com/Ne0nd0g/merlin) 用于反射 dll 支持
*   [dgoogauth](https://github.com/dgryski/dgoogauth) 用于 2FA 功能
*   [棕褐色](https://github.com/unixpickle/gobfuscate)用于支持代理混淆
*   [栈溢出](https://stackoverflow.com/)因为我们现在不就是这样发展的吗？

**免责声明**

该程序只应在您拥有或明确许可的环境中使用。无论是作者还是 Critical Start，Inc .都不对任何非法使用本程序的行为负责。

[**Download**](https://github.com/DeimosC2/DeimosC2)