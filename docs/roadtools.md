# road tools:Azure 广告探索框架

> 原文：<https://kalilinuxtutorials.com/roadtools/>

[![ROADTools : The Azure AD Exploration Framework](img/baf10783630173a04c9768f976339c22.png "ROADTools : The Azure AD Exploration Framework")](https://1.bp.blogspot.com/--XPO6vwhrXk/XqsUhc1UrhI/AAAAAAAAGIQ/xS-rRC5_-28VSH2o212tAdQWGKpJ8EA6wCLcBGAsYHQ/s1600/Roadtools-svg.png)

**ROADtools** 是一个与 Azure AD 交互的框架。它目前由一个库(roadlib)和 ROADrecon Azure AD exploration 工具组成。

**ROADlib**

**ROADlib** 是一个库，可用于通过 Azure AD 进行身份验证，或者构建与包含 ROADrecon 数据的数据库集成的工具。ROADlib 中的数据库模型是基于 Azure AD 内部 API 的元数据定义自动生成的。ROADlib 位于 ROADtools 名称空间中，因此要在脚本中导入它，请使用`**from roadtools.roadlib import X**`

**道路平面图**

ROADrecon 是一个从红队和蓝队的角度探索 Azure AD 中信息的工具。简而言之，它是这样做的:

*   使用自动生成的元数据模型在磁盘上创建 SQLAlchemy 支持的数据库。
*   使用 Python 中的异步 HTTP 调用将 Azure 广告图中的所有可用信息转储到该数据库。
*   提供插件来查询这个数据库，并将其输出到一个有用的格式。
*   提供 Angular 内置的扩展接口，直接查询离线数据库进行分析。

ROADrecon 使用`async` Python 特性，只兼容 Python 3.6-3.8(开发是用 Python 3.8 完成的)。

**安装**

安装 ROADrecon 有多种方法:

*   **使用 PyPi 上的已发布版本**

稳定版本可以用`**pip install roadrecon**`安装。这将自动将`**roadrecon**`命令添加到您的路径中。

*   **使用 GitHub 的版本**

对 master 的每一次提交都是通过 Azure 管道自动构建到发布版本中的。这确保了您可以安装最新版本的 GUI，而不必安装 **`npm`** 及其所有依赖项。只需从 Azure Pipelines 工件中下载 **`roadlib`** 和 **`roadrecon`** zip 文件，然后解压缩这两个文件并按照正确的顺序安装它们(首先是 **`roadlib`** ):

**pip 安装 roadlib/
pip 安装 roadrecon/**

也可以用 **`pip install -e roadlib/`在开发模式下安装。**

*   **开发前端**

如果你想改变前端的角度，你需要安装`node`和`npm`。然后从 git 安装组件:

**git 克隆 https://github.com/dirkjanm/roadtools.git
pip install-e road lib/
pip install-e road recon/
CD road recon/frontend/
NPM install**

您可以从`**roadrecon/frontend/**`目录使用 Angular CLI 用`**npm start**`或`**ng serve**`运行 Angular 前端。要将 JavaScript 文件构建到 ROADrecon 的`**dist_gui**`目录中，运行`**npm build**`。

[**Download**](https://github.com/dirkjanm/ROADtools)