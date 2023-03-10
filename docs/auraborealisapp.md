# AuraBorealisApp:一个可视化 Python 包注册中心安全审计数据的工具

> 原文：<https://kalilinuxtutorials.com/auraborealisapp/>

[![Open Group](img/afa7ddb32ed3e09a61524f52ec6f183a.png "Open Group")](https://1.bp.blogspot.com/-irdkUwGnVok/YSjjiPxGbUI/AAAAAAAAKlo/jnmYuxb1e3g96uy2XfPAOnOkbGqboaQrQCLcBGAsYHQ/s728/image.psd.png)

AuraBorealis 是一个 web 应用程序，用于可视化 Python 包注册表中的异常和潜在恶意代码。它使用通过 Aura 扫描 Python 包索引(PyPI)产生的安全审计数据，Aura 是一种为 Python 包的大规模安全审计而设计的静态分析。目前的工具是一个概念验证，包括一些现场光环数据，以及一些用于演示目的的模型数据。

当前功能包括:

*   扫描整个 python 包注册表以:
    *   列出安全警告数量最多的包，按先兆警告类型排序
    *   列出按警告总数和唯一警告数排序的包
    *   按总体严重性分数列出软件包
*   显示单个包的安全警告，按重要程度排序
*   可视化为特定包生成安全警告的文件中的行号和代码行
*   比较两个包的安全警告

**指令**

打开你的虚拟专用网(在 IQT)

克隆存储库。

**git 克隆 https://github.com/IQTLabs/AuraBorealisApp.git**

导航到 aura-borealis-flask-app 目录。

**光盘光环-蝴蝶-flask 应用程序**

安装依赖项。

**pip install-r requirements . txt**

运行应用程序。

**python app.py**

通过浏览器导航到 URL `**http://0.0.0.0:7000/**`。

[**Download**](https://github.com/IQTLabs/AuraBorealisApp)