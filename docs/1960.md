# Cariddi:获取域列表，抓取 URL 并扫描端点、秘密、Api 密钥、文件扩展名、令牌等等…

> 原文：<https://kalilinuxtutorials.com/cariddi/>

[![Cariddi : Take A List Of Domains, Crawl Urls And Scan For Endpoints, Secrets, Api Keys, File Extensions, Tokens And More…](img/732197decd59ab1a8ad2f124700e4dbc.png "Cariddi : Take A List Of Domains, Crawl Urls And Scan For Endpoints, Secrets, Api Keys, File Extensions, Tokens And More…")](https://1.bp.blogspot.com/-cL6XNf8ZIy4/YOm_NRjirEI/AAAAAAAAJ8o/57zeE6fG3zw8Jg7EGsob3HgD8DG0t10dQCLcBGAsYHQ/s728/logo%2B%25281%2529.png)

Cariddi 是一个获取域名列表、抓取 URL 并扫描端点、秘密、api 密钥、文件扩展名、令牌等的工具。

**安装**

你需要去。

**Go** 是一种开源编程语言，它使得构建**简单**、**可靠**和**高效**软件变得容易。

*   **Linux**
    *   `**git clone https://github.com/edoardottt/cariddi.git**`
    *   `**cd cariddi**`
    *   `**go get**`
    *   `**make linux**`(安装)
    *   `**make unlinux**`(卸载)或一行:`**git clone https://github.com/edoardottt/cariddi.git; cd cariddi; go get; make linux**`
*   **Windows** (可执行文件只能在 cariddi 文件夹下运行。)
    *   `**git clone https://github.com/edoardottt/cariddi.git**`
    *   `**cd cariddi**`
    *   `**go get**`
    *   `**.\make.bat windows**`(安装)
    *   `**.\make.bat unwindows**`(卸载)

**开始使用**

`**cariddi -h**`在命令行中打印帮助。

**car iddi 的用法:
-c int
并发级别。(默认为 20)
-缓存
使用。cariddi_cache 文件夹作为缓存。
-d int
抓取的页面与另一个页面之间的延迟。寻找有趣的终点。
-ef string
使用外部文件(txt，每行一个)使用自定义参数进行端点搜索。
-示例
打印示例。寻找有趣的文件扩展名。从 1(多汁)到 7(不多汁)的整数。
-h 打印帮助。
-i string
忽略包含该数组至少一个元素的 URL。
-it string
忽略包含该文件至少一行的 URL。
-oh string
将输出写入 HTML 文件。
-ot 字符串
将输出写入 TXT 文件。
-普通
仅打印结果。
-s 猎取秘密。
-sf string
使用一个外部文件(txt，每行一个)来使用自定义正则表达式进行秘密搜索。
-t int
设置请求超时。(默认 10)
-版本
打印版本。**

**例题**

*   **`cariddi -version`** (打印版)
*   **`cariddi -h`** (打印帮助)
*   `**cariddi -examples**`(打印示例)
*   `**cat urls | cariddi -s**`(寻找秘密)
*   `**cat urls | cariddi -d 2**`(两次抓取页面间隔 2 秒)
*   `**cat urls | cariddi -c 200**`(将并发级别设置为 200)
*   `**cat urls | cariddi -e**`(寻找有趣的终点)
*   `**cat urls | cariddi -plain**`(只打印有用的东西)
*   `**cat urls | cariddi -ot target_name**`(txt 文件中的结果)
*   `**cat urls | cariddi -oh target_name**`(html 文件中的结果)
*   `**cat urls | cariddi -ext 2**`(寻找多汁的(第 2 级，共 7 级)文件)
*   `**cat urls | cariddi -e -ef endpoints_file**`(搜寻自定义端点)
*   `**cat urls | cariddi -s -sf secrets_file**`(寻找风俗秘密)
*   `**cat urls | cariddi -i forum,blog,community,open**`(忽略包含这些单词的 URL)
*   `**cat urls | cariddi -it ignore_file**`(忽略输入文件中至少包含一行的 URL)
*   `**cat urls | cariddi -cache**`(使用。cariddi_cache 文件夹作为缓存)
*   `**cat urls | cariddi -t 5**`(设置请求超时)
*   对于 Windows，使用`**powershell.exe -Command "cat urls | .\cariddi.exe"**`

[**Download**](https://github.com/edoardottt/cariddi)