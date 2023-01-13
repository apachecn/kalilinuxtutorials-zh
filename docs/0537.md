# Flashmingo:基于一些启发的 SWF 文件自动分析

> 原文：<https://kalilinuxtutorials.com/flashmingo/>

FLASHMINGO 是一个 SWF 文件的分析框架。该工具自动对可疑的 Flash 文件进行分类，并指导进一步的分析过程，释放您团队中的宝贵资源。

您可以轻松地将 FLASHMINGO 的分析模块整合到您的工作流程中。

直到今天，法医调查人员和恶意软件分析师必须处理可疑的 SWF 文件。如果历史重演，闪存在 2020 年寿终正寝后，安全威胁甚至会变得更大。

系统将继续支持不再用安全补丁更新的传统文件格式。自动化是处理这个问题的最好方法，这也是 FLASHMINGO 可以帮助你的地方。

FLASHMINGO 是一个自动处理 SWF 文件的分析框架，使您能够标记可疑的 Flash 样本，并以最小的努力对它们进行分析。

它作为独立的应用程序或功能强大的库集成到各种分析工作流程中。用户可以通过定制的 Python 插件轻松扩展该工具的功能。

**也可阅读-[佩佩:从 Pastebin](https://kalilinuxtutorials.com/pepe-information-email-addresses/) 那里收集邮件地址信息**

**如何**

**架构**

FLASHMINGO 的设计考虑到了简单性。它读取一个 SWF 文件并创建一个代表其内容和结构的对象(`**SWFObject**`)。之后，FLASHMINGO 运行一系列插件来作用于这个`**SWFObject**`，并将它们的值返回给主程序。

下图为强制性 ASCII 艺术流程图:

![](img/66bcc0542647bbf74c7bd6bf485090a3.png)

当在您自己的项目中使用 FLASHMINGO 作为库时，您只需要关注两种对象:

*   一个或多个代表样品的`SWFObject`
*   一个`Flashmingo`物体。这实质上充当了连接插件和`SWFObject`的线束。

**外挂！**

FLASHMINGO 插件存储在它们自己的目录下…你猜对了:`**plugins**`当一个`**Flashmingo**`对象被实例化时，它会遍历这个目录并处理所有插件的清单。

如果这表明插件是活动的，那么它将被注册以备后用。在代码级别，这意味着一个小的`**plugin_info**`字典被添加到了`**plugins**`列表中。

插件是通过带有两个参数的`**run_plugin**` API 调用的:

*   插件的名称
*   `**SWFObject**`实例

可选地，大多数插件允许你传递你自己的用户数据。这是依赖于插件的(阅读文档),用一个例子可以更容易地解释。

默认插件`**SuspiciousNames**`将在所有常量池中搜索包含*可疑*子字符串的字符串(例如:‘溢出’，‘喷射’，‘外壳’等)。)插件中已经硬编码了一个公共子字符串列表，这样就可以使用它了`**as-is**`。

但是，您可以传递您自己定义的子字符串列表，在这种情况下通过`**names**` 参数。

代码示例:

**FM = Flashmingo()
print FM . run _ plugin(' DangerousAPIs '，swf=swf)
print FM . run _ plugin(' SuspiciousNames '，swf = swf，names=['幽灵'])**

**默认插件**

FLASHMINGO 自带一些有用的插件:

*   二进制数据
*   危险 _ apis
*   反编译程序
*   可疑常数
*   可疑循环
*   可疑姓名
*   模板🙂

**扩展 FLASHMINGO**

提供了一个模板插件，以便于开发。扩展 FLASHMINGO 相当简单。遵循以下简单步骤:

*   复制模板
*   编辑清单
*   覆盖`run`方法
*   添加您的自定义代码

你已经准备好了🙂

**作为库的 flash mingo**

**API**

*   参见`docs`目录，获取自动生成的文档
*   请看 FireEye 的博客文章中的例子

**前端**

*   安慰

**创建文档**

`**$ pip install sphinxcontrib-napoleon**`

在设置 Sphinx 来构建您的文档之后，在 Sphinx conf.py 文件中启用 napoleon:

在`**conf.py**`中，将拿破仑添加到扩展列表中

`**extensions = ['sphinxcontrib.napoleon']**`

使用 sphinx-apidoc 构建您的 API 文档:

`**$ sphinx-apidoc -f -o docs/source projectdir**`

这为 Sphinx 处理创建了`.rst`文件

`$ **make** html`

就是这样！🙂

[**Download**](https://github.com/fireeye/flashmingo)