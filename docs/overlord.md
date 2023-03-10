# 霸主:红队基础设施自动化

> 原文：<https://kalilinuxtutorials.com/overlord/>

[![Overlord : Red Teaming Infrastructure Automation](img/b2fc9bcd6fca582a422275352dffe7f4.png "Overlord : Red Teaming Infrastructure Automation")](https://1.bp.blogspot.com/-r5ND3Z9eKDc/YIiCCa65oFI/AAAAAAAAI3o/wqQdO93mNyYDNamjsv9yraaegUiJVbrigCLcBGAsYHQ/s728/Overlord%25281%2529.png)

**霸王**提供了一个基于 python 的控制台 CLI，用于以自动化方式构建 Red Teaming 基础架构。用户必须通过使用该工具的模块(如 C2、电子邮件服务器、HTTP 网络交付服务器、网络钓鱼服务器等)来提供输入。)并且完整的基础架构/模块和脚本将在选择的云提供商上自动生成。目前支持 AWS 和数字海洋。该工具仍在开发中，它的灵感来自于 Github 上的[红男爵](https://github.com/byt3bl33d3r/Red-Baron) Terraform 实现。

在我们的博客文章[https://blog.qsecure.com.cy/posts/overlord/](https://blog.qsecure.com.cy/posts/overlord/)中搭建了一个演示基础设施。

如需该工具的完整文档，请访问位于 https://github.com/qsecure-labs/overlord/wiki 的 Wiki 选项卡。

**安装**

**git 克隆 https://github.com/qsecure-labs/overlord.git
CD 霸王/配置
chmod +x install.sh
sudo。/install.sh**

**致谢**

如果没有 Marcello Salvati @byt3bl33d3r 在 RedBaron 项目中的出色工作，这个项目就无法完成。这也是我们在项目中引用 RedBaron 名称的原因。

正如 Marcello 在致谢中所述，进一步感谢:

*   @_RastaMouse 关于“使用 Terraform 自动部署红队基础设施”的两部分博客文章第 1 部分和第 2 部分
*   @bluscreenofjeff 在 Read Team Infrastucture 上的惊人 Wiki
*   @spotheplanet 关于红队基础设施的博文

**免责声明**

霸王无担保，旨在供渗透测试人员在批准的红队评估和/或社交工程评估中使用。霸王的开发者和 QSecure 拒绝承担任何责任，以防该工具被用于恶意目的或在任何非法的背景下。

[**Download**](https://github.com/qsecure-labs/overlord)