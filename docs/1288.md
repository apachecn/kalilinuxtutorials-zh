# Richkit:领域丰富工具包

> 原文：<https://kalilinuxtutorials.com/richkit/>

[![Richkit : Domain Enrichment Toolkit](img/7f366491dd03b9a450fb6e470494f740.png "Richkit : Domain Enrichment Toolkit")](https://1.bp.blogspot.com/-OTD83MVtXuQ/XpNJRA8hXZI/AAAAAAAAF44/9CUrrpu8FEU64TeAMpVjegS-IDjggR-9QCLcBGAsYHQ/s1600/RichKit%25281%2529.png)

Richkit 是一个 python3 包，它提供了将域名作为输入的工具，并返回该域名的附加信息。它可以是对领域本身的分析，从数据库中查找，从其他服务中检索，或者它们的某种组合。

richkit 的目的是提供一个与域名相关的分析、查找和检索功能的可重用库，该库在奥尔堡大学的网络安全研究组内共享，也可供公众重用和修改。

**要求**

**Python > = 3.5**

**安装**

要安装 richikit，只需在终端中键入

**pip 安装 richkit**

**亦读-[寒鸦:聚聚聚](https://kalilinuxtutorials.com/jackdaw/)**

**用途**

以下代码可分别用于检索 TLD 和 URL 类别。

*   检索给定 url 的有效顶级域:

**> >从 richkit.analyse 导入 TLD
>>urls =[" www . AAU . dk "，" www.github.com "，" www . Google . com "]
>>
>>对于 URL 中的 URL:
…print(TLD(URL))
dk
com
com**

*   检索给定 url 的类别:

> > > from rich kit . retrieve . Symantec import fetch _ from _ Internet
>>>from rich kit . retrieve . Symantec import LocalCategoryDB
>>>
>>>URL =[" www . AAU . dk "，" www.github.com "，" www . Google . com "]
>>>
>>>local _ db = LocalCategoryDB()

**模块**

Richkit 定义了一组按以下模块分类的函数:

*   `**richkit.analyse**`:该模块提供了可以应用于域名的功能。与`**richkit.lookup**`类似，与`**richkit.retrieve**`相反，这是在不向第三方披露域名和违反保密性的情况下完成的。
*   `**richkit.lookup**`:该模块提供在本地资源中查找域名的能力，即域名不能发送给第三方。该模块可以获取资源，如列表或数据库，但这必须以保持域名机密的方式完成。将此与 **`richkit.retrieve`相对照。**
*   **`richkit.retrieve` :** 这个模块提供了检索任何种类的域名数据的能力。它没有`**richkit.lookup**`的“保密合同”。

**信用:** [独立完成](https://www.behance.net/independenthand)