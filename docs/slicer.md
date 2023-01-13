# 切片器:自动化 APK 侦察的枯燥过程

> 原文：<https://kalilinuxtutorials.com/slicer/>

[![](img/d791f7f58a1d5c5ec7014f514cbe68d7.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj34l-IgP4V-RaKqQM36qUnpAyFenx6PN2yO12mhtZNlKcY4FbXxSOzHhqnnRNox7DXfEBrtx76pCgbbXeSbStYwdIJ68-Fy9UPAUb_uKdUqJARJDQSLys4VR7kptubnxPalYUXi7uXJ-ARmwBasJHCXL2xKIPkjVmq2ZAvt3NkoDf1E30qzQWc2Hl3/s1280/blody%20logo.png)

**切片器**接受一个路径到一个提取的 APK 文件，然后返回所有的活动、接收者和服务，这些活动、接收者和服务被导出并具有`**null**`权限，可以被外部激发。

**注意**:APK 必须通过`**jadx**`或`**apktool**`提取。

# 特征

*   检查 APK 是否已经将`**android:allowbackup**`设置为`**true**`
*   检查 APK 是否已经将`**android:debuggable**`设置为`**true**`。
*   返回所有已导出且具有空权限集的活动、服务和广播接收器。这是根据两件事决定的:
    *   `**android:exporte=true**`存在于任何组件中并且没有权限集。
    *   如果没有提到 exported，那么切片器检查是否为该组件定义了任何`**Intent-filters**`,如果是，这意味着默认情况下该组件被导出(这是 android 文档中给出的规则。)
*   通过测试`**.json**`技巧来检查 APK 的 Firebase URL。
    *   如果 firebase 的 URL 是 **`myapp.firebaseio.com`** ，那么它将检查`**https://myapp.firebaseio.com/.json**`是否返回某些东西或者拒绝给予许可。
    *   如果这个东西是开放的，那么可以报告为高严重性。
*   检查 google API 密钥是否可以公开访问。
    *   这可以在一些赏金程序中报告，但严重性较低。
    *   但是很多时候举报这种事情会带出`**Duplicate**`的痛苦。
    *   有时，公司可以将它作为`**not applicable**`关闭，并声称该密钥有一个`**usage cap**`–r/可疑的细节
*   返回出现在`**strings.xml**`和`**AndroidManifest.xml**`中的其他 API 键
*   列出`**/res/raw**`和`**res/xml**`目录中存在的所有文件名。
*   提取所有的 URL 和路径。
    *   这些可以和像 dirsearch 或者 ffuf 这样的工具一起使用。

# 安装

*   克隆此存储库

**git 克隆 https://github.com/mzfr/slicer**

*   `**cd slicer**`
*   现在你可以运行它了:`**python3 slicer.py -h**`

# 用法

用起来很简单。以下选项可用:

**从 APK 的清单和字符串中提取信息
用法:
切片器【选项】【提取的 APK 目录】
选项:
d，–jadx 输出目录的 dir 路径
o，–输出文件的输出名(未实现)**

我还没有实现`**output**`标志，因为我认为如果你能将切片器的输出重定向到一个 yaml 文件，它将是一个合适的格式。

# 用法举例

*   从 APK 中提取信息并显示在屏幕上。

**python 3 slicer . py-d path/to/extact/apk-c config . JSON**

[**Download**](https://github.com/mzfr/slicer)