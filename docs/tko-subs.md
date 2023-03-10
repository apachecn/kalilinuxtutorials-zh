# Tko-Subs:一个工具，可以帮助检测和接管死 DNS 记录的子域名

> 原文：<https://kalilinuxtutorials.com/tko-subs/>

[![OpenRelayMagic : Tool To Find SMTP Servers Vulnerable To Open Relay](img/2a6b340126f3b3a5b7b6a47cd419895f.png "OpenRelayMagic : Tool To Find SMTP Servers Vulnerable To Open Relay")](https://1.bp.blogspot.com/-RQRpG5cuPxY/XkcE23IRpzI/AAAAAAAAE-U/fO-AztmQ7Vkrf4K8Dx_rn6rL_u9lTR-fgCLcBGAsYHQ/s1600/screencast.gif)

**Tko-Subs** 允许:

*   检查子域是否可以被接管，因为它有:
    *   一个悬空的 CNAME 指向一个 CMS 提供商(Heroku，Github，Shopify，亚马逊 S3，亚马逊 CloudFront 等。)可以接手的。
    *   指向不存在的域名的悬空 CNAME
    *   一个或多个指向域名服务器的错误/输入错误的 d NS 记录，攻击者可以利用这些记录来控制子域的 DNS 记录
*   通过提供一个标志`**-takeover**`来实际接管这些子域。目前，只有 Github 页面和 Heroku 应用程序支持接管，默认情况下接管功能是关闭的。
*   指定您自己的 CMS 提供程序，并通过 providers-data.csv 文件检查它们。在该文件中，您将提到 CMS 名称、它们的 CNAME 值、它们想要查找的字符串以及它是否只在 HTTP 上工作。查看一些例子。

**先决条件**

我们需要去安装。一旦你进入，只需输入`**go get github.com/anshumanbh/tko-subs**`就可以下载该工具。

工具下载完成后，输入`**tko-subs -h**`。

接下来我们需要做的是获取以下信息:

*   Github 的个人访问令牌——确保这个令牌有权创建存储库、引用、内容等。您可以在这里创建这个令牌——https://github.com/settings/tokens
*   Heroku 用户名和 API 密钥
*   Heroku 应用程序名称–您可以按照此处的说明在 Heroku 上创建一个静态应用程序，使用您希望在其主页上显示的任何内容–https://gist.github.com/wh1tney/2ad13aa5fbdd83f6a489.一旦您创建了该应用程序，请在标志中使用该应用程序名称(见下文)。我们将使用该应用程序接管域名(将 CNAME 挂在另一个 Heroku 应用程序上)。

**注意**–如果你想接管子域，你只需要这些值。默认情况下，这不是必需的。

要构建的必需 Go 包。

**go get github . com/bgntry/heroku-go
go get github . com/gocarina/gocsv
go get github . com/Google/go-github/github
go get github . com/olekukonko/table writer
go get golang . org/x/net/public suffix
go**

**怎么跑？**

一旦你安装好了所有的东西，进入目录并输入:`**tko-subs -domains=domains.txt -data=providers-data.csv -output=output.csv**`

如果您也想接管，命令应该是:`**tko-subs -domains=domains.txt -data=providers-data.csv -output=output.csv -takeover -githubtoken=<github-token> -herokuusername=<heroku-username> -herokuapikey=<heroku-api-key> -herokuappname=<heroku-app-name>**`

如果您只想检查单个域，请键入:`**tko-subs -domain <domain-name>**`

如果您只想检查多个域，请键入:`**tko-subs -domain <domain-name-1>,<domain-name-2>**`

默认情况下:

*   `**domains**`标志被设置为`**domains.txt**`
*   `**data**`标志被设置为`**providers-data.csv**`
*   `**output**`标志被设置为`**output.csv**`
*   没有设置`**takeover**`标志，所以默认情况下没有接管
*   没有设置`**domain**`标志，所以它将总是检查在`**domains.txt**`文件中提到的所有域。如果提到了`**domain**`标志，它将只检查那个域并忽略`**domains.txt**`文件，即使它存在
*   `**threads**`标志被设置为`5`

因此，简单地运行`**tko-subs**`将使用上面提到的默认值。

**providers-data . CSV 是如何格式化的？**

名称，cname，字符串，http

*   名称:提供者的名称(例如 github)
*   cname:用于将网站映射到提供商内容的 CNAME(例如 github.io)
*   string:为无人认领的子域返回的错误消息(例如，“这里没有 GitHub Pages 站点”)
*   http:是否使用 http(不是默认的 https)连接到站点(对/错)

**输出如何格式化？**

域，CNAME，提供商，易受攻击，IsTakenOver，响应

*   域:检查的域
*   CNAME:领域中的 CNAME
*   提供者:发现域正在使用的提供者
*   IsVulnerable:是否发现域易受攻击(对/错)
*   IsTakenOver:域是否被接管(对/错)
*   响应:检查子域时所依据的消息

如果发现失效的 DNS 记录，`**Provider**`留空。如果发现一个行为不当的域名服务器，`**Provider**`和`**CNAME**`被留空

**引擎盖下是怎么回事？**

这将迭代 **`subdomains.txt`** 文件中的所有域(同时使用 GoRoutines ),并且:

*   看看他们是否有一个行为不端的权威域名服务器；如果有，我们会将该域标记为易受攻击。
*   看看他们是否有悬空的 CNAME 记录又名死亡的 DNS 记录；如果有，我们会将该域标记为易受攻击。
*   如果一个子域通过了这两个测试，它会尝试卷曲它们并得到一个响应，然后尝试查看该响应是否匹配 providers-data.csv 文件中提到的任何数据提供者字符串。
*   如果响应匹配，我们将该域标记为易受攻击。
*   接下来，根据是否提到了`**takeover**`标志，它将试图接管这个易受攻击的子域。
*   例如，要接管 Github 页面，代码将:
    *   创建一个回购
    *   在回购中创建一个分支`**gh-pages**`
    *   上传`**CNAME**`和`**index.html**`到该回购的`**gh-pages**`分行。这里，`**CNAME**`包含了需要接管的域。`**index.html**`包含当域名被接管时显示的文本`**This domain is temporarily suspended**`。
*   同样，对于 Heroku 应用程序，代码将:
    *   将悬空域添加到您的 Heroku 应用程序(您将在。环境文件)
*   而且，就是这样！

[**Download**](https://github.com/anshumanbh/tko-subs)