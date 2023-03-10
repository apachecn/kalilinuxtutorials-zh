# DirSearch:DirSearch 的 Go 实现

> 原文：<https://kalilinuxtutorials.com/dirsearch/>

[![](img/b98c2e4ce47655db00e0e0b50d1709d2.png)](https://1.bp.blogspot.com/-kF9Q-jzLlkE/YU1mo4C41uI/AAAAAAAAK8A/gw5LY6pO69YjMaPumTDMO4_NeM28sYZHwCLcBGAsYHQ/s728/babygopher-badge%2B%25281%2529.png)

**DirSearch** 软件是`**Mauro Soria**`编写的原创 DirSearch 工具的 Go 实现。DirSearch 是我用 Go 编写的第一个工具，主要是为了试验 Go 的并发模型、通道等等。

**目的**

DirSearch 接受一个输入 URL ( **`-url`** 参数)和一个单词列表(`**-wordlist**`参数)，然后它将使用单词列表的行作为路径和文件执行并发的`**HEAD**`请求，最终在 web 服务器上强制执行文件夹和文件。

它支持自定义文件扩展名(`**-ext**`，默认为`**php**`)和其他可选参数:

**dirsearch 的用法:
-200only
如果启用，将只显示状态码为 200 的响应。
-消费者 int
并发消费者数量。(默认为 8)
-ext string
文件扩展名。(默认“PHP”)
-max errors int
在杀死程序之前得到的最大错误数。(默认为 20)
-url 字符串
开始枚举的基本 url。
-单词列表字符串
用于枚举的单词列表文件。(默认“dict . txt”)**

**编译**

**去拿 github.com/evilsocket/dirsearch
光盘目录搜索
制作 get_glide
制作 install_dependencies
制作构建**

[**Download**](https://github.com/evilsocket/dirsearch)