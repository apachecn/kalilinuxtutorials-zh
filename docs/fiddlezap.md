# FiddleZAP:OWASP ZAP 的简化版 EKFiddle

> 原文：<https://kalilinuxtutorials.com/fiddlezap/>

[![](img/db351e9f47ed06b1daed38eaaf2f0c14.png)](https://blogger.googleusercontent.com/img/a/AVvXsEgea1DCZHeaciT8-4ObMXCQvNhcaJWz_INwxQ5L8zD06UockO_xJb8rpXpwLHksCh1U6ruOPOnkHyuDpGTQyjOrFipBv9j75FwJVtLI6wJ_0vw7kHhmAPmgV_zw1XNAcLrlwFLKpXS1Qr7KNX38RRvsMTFjT-qfWAz7EMHB5kYx2IJVb5PVNIjf-Hzo=s639)

**FiddleZAP** 是 OWASP ZAP 的简化版 EKFiddle。

使用 ZAP 作为您的 web 代理，您可以基于预定义的正则表达式标记恶意流量。

示例:当正则表达式与受损网站的 HTML 源代码中的字符串匹配时，发出警报、突出显示和标记

![](img/a5c303ff79f64e6ff984da2aa0e7fd95.png)

**安装**

*   下载并安装 ZAP:https://www.zaproxy.org/download/
*   将 FiddleZAP 目录下载或克隆到 Documents 文件夹中。

它应该具有以下结构:

![](img/a2173978b1efbd912cf61695d9fc6196.png)

有 2 个脚本(独立的、被动的规则)。前者用于在当前加载的会话(web 流量)上手动运行，后者在记录流量时自动运行。

**独自一人**

首先，安装独立脚本:

*   单击加载脚本图标:

![](img/c48f635e6105da074688a1428ac89a40.png)

*   选择以下参数:

![](img/daa52a5a9392fbb8702de5ac47314363.png)

*   它现在显示在“独立”下:

**被动规则**

接下来，安装被动规则脚本:

*   单击加载脚本图标:

![](img/2d43b52bf43cebce02768869fed69dc2.png)

*   选择以下参数:

![](img/cada4c3986f66fbf4f377b5454da80ae.png)

*   FiddleZAP 脚本现在应该显示在被动规则下。如果没有启用，右键单击它并选择 Enable script。

![](img/378e2d0cbc4f9f1c44024745fc997bfe.png)

**特性**

**检测恶意流量的正则表达式(规则)**

FiddleZAP 的规则可以寻找 URI 模式和源代码模式(会话体)。

*   一个`**community_rules.txt**`文件提供了一些例子。
*   `**user_rules.txt**`是您自己的规则文件。

规则会自动加载并用于扫描传入流量(如果启用了被动规则脚本)。如果您想要对以前捕获的流量运行规则，您需要运行独立脚本。

![](img/3a21aaad920d0a4bae1015e9b86aeaf8.png)

**匹配 web 会话的颜色编码和标记**

(此功能需要 neonmarker 附件)

![](img/4d450f3245d62d8c7c304ea4fd15df3f.png)

**详细警报**

![](img/7466bd259e73c6998ccfc39d03aa0e4f.png)[**Download**](https://github.com/malwareinfosec/FiddleZAP)