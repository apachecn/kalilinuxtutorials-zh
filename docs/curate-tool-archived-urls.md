# 一个获取存档网址的工具

> 原文：<https://kalilinuxtutorials.com/curate-tool-archived-urls/>

Curate 是一个工具，用于获取存档的 URL 和要在 Go 中重写的。

## **始乱终弃初始调教俏皮话**

这将克隆这个库，然后将所有脚本移动到 **/usr/local/bin** 。

```
$ git clone git@github.com:EdOverflow/curate.git \
&& cp curate/curate /usr/local/bin/ \
&& echo "You can delete the ./curate/ folder now."
```

一旦你完成了这个一行程序，确保在你的**中包含你的 **VirusTotal API** 密钥。bashrc** 文件。该变量应命名为 **VIRUS_TOTAL_API_KEY** 。

**也读作 [使用 Cymothoa 维护对 Linux 机器的访问——后期利用](https://kalilinuxtutorials.com/cymothoa/)**

## **用途**

要获取存档的 URL，只需运行它并指定目标主机。

```
 **$ curate <host>
 $ curate example.com
```

如果您想在输出中直接搜索字符串，您也可以使用-r 标志来指定您的搜索词或正则表达式。

```
$ curate <host> -r <search term>
$ curate example.com -r example
```

## **搜索词列表**

Curate 将结果输出到一个 curate.txt 文件中，这样你就可以很容易地浏览关键字的 URL。以下是一些在 curate.txt 中 grep for things 的想法。

*   管理
*   密码
*   键
*   美国石油学会(American Petroleum Institute)
*   hmac
*   全球资源定位器(Uniform Resource Locator)
*   小路
*   雨后储水区
*   服务器端编程语言（Professional Hypertext Preprocessor 的缩写）
*   id=

建议通过将所有内容输入“grep -v”来排除搜索中的图像和样式表。

## **免责声明**

该项目仅用于教育和道德测试目的。未经双方
同意，使用此工具攻击目标是非法的。开发者不承担任何责任，也不对这些脚本造成的任何误用或损害负责
。

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/EdOverflow/curate)