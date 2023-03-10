# Haklistgen:将任何垃圾文本转换成可用于暴力破解的单词列表

> 原文：<https://kalilinuxtutorials.com/haklistgen/>

[![](img/c3711039da8757bb9fc544ebf9186181.png)](https://1.bp.blogspot.com/-Sw_XNGZVkII/YU8el3Mik2I/AAAAAAAAK9I/AY_X2ESe0msU9m3pN_blie4T2OBm4YJEgCLcBGAsYHQ/s728/images%2B%25281%2529.png)

Haklistgen 将任何垃圾文本转化为可用于暴力破解的单词列表。

**安装**

**去安装 github.com/hakluke/haklistgen@latest**

**用法举例**

从 HTTP 响应中提取所有单词以构建目录结构 force 单词列表:

**下载 https://维基百科. org \搜索日志**

通过管道将一个子域列表传递给它，以生成一个单词列表，用于强制更多子域:

**sub finder-silent-d example.com | haklistgen**

自定义 JavaScript 文件中的管道可能会产生一些有趣的结果:

科尔·https://example.com/app.js |哈克利斯特根

您可以为大范围的目标创建一个很好的自定义单词列表，如下所示:

**sub finder-silent-d hakluke.com | anew sub domains . txt | httpx-silent | anew URLs . txt | hak rawler | anew endpoints . txt | while read URL；do curl $ URL–不安全| haklistgen | anew wordlist.txtdone
cat subdomains . txt URLs . txt endpoints . txt | haklistgen | anew word list . txt；**

这会将子域名保存到`**subdomains.txt**`，然后将 httpx 输出保存到 **`urls.txt`，**然后抓取每个 url 并将 hakrawler 输出保存到`**endpoints.txt**`，然后获取`**endpoints.txt**`中的每个 URL 并制作一个单词列表，将所有单词列表连接到 **`wordlist.txt`。然后，它获取所有的子域和 URL，并在其中添加单词。**

[**Download**](https://github.com/hakluke/haklistgen)