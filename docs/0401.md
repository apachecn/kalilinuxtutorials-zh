# Modlishka:一个灵活而强大的反向代理工具

> 原文：<https://kalilinuxtutorials.com/modlishka-powerful-reverse-proxy/>

Modlishka 是一个灵活而强大的反向代理，它将把您的道德钓鱼活动提升到一个新的水平。它的发布旨在:

*   帮助渗透测试人员开展有效的网络钓鱼活动，并强调网络钓鱼可能会带来严重的威胁。
*   展示当前的 2FA 弱点，以便能够尽快创建和实施适当的安全解决方案。
*   提高社区对现代网络钓鱼技术和策略的认识。
*   支持其他需要通用反向代理的开源项目。

**也读作: [](https://kalilinuxtutorials.com/dfirtrack-tracking-application/)** [Dfirtrack:事件响应跟踪应用](https://kalilinuxtutorials.com/dfirtrack-tracking-application/)

**特性**

一些最重要的“Modlishka”功能:

*   支持大多数 2FA 认证方案(通过设计)。
*   没有网站模板(只需将 Modlishka 指向目标域-在大多数情况下，它会自动处理)。
*   完全控制来自受害者浏览器的“跨”源 TLS 流量(通过定制的新技术)。
*   通过配置选项灵活且易于配置的网络钓鱼场景。
*   基于模式的 JavaScript 有效负载注入。
*   剥离网站的所有加密和安全标题(回到 90 年代的 MITM 风格)。
*   用户凭据收集(使用基于 URL 参数传递的标识符的上下文)。
*   可以通过插件扩展你的想法。
*   无状态设计。可以针对任意数量的用户轻松扩展，例如通过 DNS 负载平衡器。
*   带有收集的凭据和用户会话模拟(测试版)摘要的 Web 面板。
*   借壳免费；-).
*   用 Go 写的。

**安装**

最新的源代码版本可以从这里(zip)或这里(tar)获得。

使用“go get”获取代码:

$ go get-u github.com/drk1wi/Modlishka

编译二进制文件，然后就可以开始了:

$ CD $ GOPATH/src/github . com/drk1wi/Modlishka/
$ make

。/dist/proxy -h

的用法。/dist/proxy:
-cert string base64 编码 TLS 证书
-certKey string base64 编码 TLS 证书密钥
-certPool string base64 编码证书颁发机构证书
-config string JSON 配置文件。方便而不是使用命令行开关。
-具有匹配组的 credParams 字符串凭据 regexp 收集器。例如:base64(username_regex)，base64(password _ regex)
-debug 打印调试信息
-disableSecurity 禁用反 SSRF 等安全功能。禁用风险自担。
-jsRules 字符串逗号分隔的 URL 模式列表和将被注入的 JS base64 编码的有效负载。
-listeningAddress 字符串监听地址(默认为“127 . 0 . 0 . 1”)
-Listening port 字符串监听端口(默认为“443”)
-获取的请求将被写入(追加)的日志字符串本地文件
-要创建的网络钓鱼字符串
网络钓鱼域-例如。:target.co
-插件字符串逗号分隔的已启用插件名称列表(默认为“全部”)
-postOnly 仅记录 HTTP POST 请求
-目标字符串主要目标到代理-例如。:https://target.com
-target rules 字符串逗号分隔的“字符串”模式及其替换列表。
-targetRes 字符串逗号分隔的需要通过代理的目标子域列表
-terminateTriggers 字符串逗号分隔的将触发会话终止的来自目标源的 Url 列表
-terminateUrl 字符串在会话终止触发后重定向客户端的 URL
-TLS
Enable TLS(默认为假)
-trackingCookie 字符串
用于跟踪受害者的 HTTP cookie 的名称(默认为“id”)
-tracking param 字符串【T24

**信用:朱塞佩·特洛塔**

[**Downlod**](https://github.com/drk1wi/Modlishka)