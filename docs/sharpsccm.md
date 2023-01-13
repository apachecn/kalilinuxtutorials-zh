# SharpSCCM:一个与 SCCM 交互的 C#实用程序

> 原文：<https://kalilinuxtutorials.com/sharpsccm/>

[![](img/afe49b32e09a8984e0fd8acc34b4abb5.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhE-_kIMonOZCoDI3KN_aVuptFo3YXlvzb9x56voQxK-OJzRJKXYo5HTs_Gl6yRJAW8oz7IX8Bea6KKDV4OTxjqhtl7hA9h4IXgGR6XiVJqS2s_XirFb0rJKSvZVc8uGwK0fSpWLAi5ghdBDFO8iwqI6I5wAaTr7PvPxD3nFRMJQOSU6zqqTqXNNSeA/s728/h121.png)

SharpSCCM 是一款开发后工具，旨在利用 Microsoft Endpoint Configuration Manager(又名 ConfigMgr，以前为 SCCM)进行横向移动和凭据收集，而无需访问 SCCM 管理控制台 GUI。

SharpSCCM 最初是为了执行从 PowerSCCM(由@harmj0y、@jaredcatkinson、@enigma0x3 和@mattifestation)移植的用户搜索和横向移动功能而创建的，现在包含收集凭据和滥用新发现的攻击原语的附加功能，用于在启用了自动站点范围客户端推送安装的 SCCM 站点中强制进行 NTLM 身份验证。

请[访问 wiki](https://github.com/Mayyhem/SharpSCCM/wiki) 获取详细介绍如何构建和使用 SharpSCCM 的文档。

### 作者

克里斯·汤普森是这个项目的第一作者。Duane Michael (@subat0mik)和 Evan McBroom (@mcbroom_evan)也是积极的贡献者。请随时在 Twitter (@_Mayyhem)上提出问题和改进意见等。，以及 GitHub 上的问题和拉取请求。

### 警告

该工具是作为实验室环境中的概念验证而编写的，尚未经过全面测试。有很多未完成的部分，可怕的错误处理，以及我可能永远不会完成的功能。请谨慎使用，风险自担。

[Click Here To Download](https://github.com/Mayyhem/SharpSCCM)