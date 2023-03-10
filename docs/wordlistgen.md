# Wordlistgen:从 URL 或路径列表中快速生成用于内容发现的特定于上下文的单词列表

> 原文：<https://kalilinuxtutorials.com/wordlistgen/>

[![](img/59b1e417b25311fa8c234505b56c65f5.png)](https://1.bp.blogspot.com/-xYPOC1wfyTg/YU16VAuQetI/AAAAAAAAK8Q/4d7ZCUXyZ7cc-0GIj4wVkYdhDNL54nkFQCLcBGAsYHQ/s1390/words%2B%25281%2529.png)

Wordlistgen 是一个传递 URL 列表并为你的单词列表获取相关单词列表的工具。当你考虑应用程序的上下文时，单词表会更有效。wordlistgen 提取 URL 组件，如子域名、路径、查询字符串等。并将它们放回 stdout，这样您就可以轻松地将它们添加到您的单词列表中。

**安装**

如果你还没有安装 go，那就“Go”吧！

**去 get-u github . com/ameman Ali/word listgen**

**用途**

wordlistgen 从 stdin 中获取 URL 和路径，您很可能希望将它们放在一个文件中，例如:

**$ cat file . txt
https://google.com/home/?q=2&d = ASD
http://my . site
/API/v2/auth/me？id=123**

从 URL 和/或路径文件中获取唯一的 URL 组件:

**cat hosts.txt | wordlistgen**

从 URL 和/或路径文件中获取唯一的 URL 组件，包括查询字符串值，并保存到文件中:

**cat hosts . txt | wordlistgen-qv>URL components . txt**

wordlistgen 与其他工具结合使用时效果最佳，例如@ tonnomnom 的 waybackurls:

**cat hosts . txt | wayback URLs | wordlistgen**

[**Download**](https://github.com/ameenmaali/wordlistgen)