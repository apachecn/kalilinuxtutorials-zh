# 检查你的域名转发是否正常

> 原文：<https://kalilinuxtutorials.com/chkdfront-domain-fronting/>

Chkdfront 通过对您的域前端域测试目标域(前端域)来检查您的域前端是否正常工作。

**特性**

*   检查你的域名正面对域名正面。
*   在响应中搜索期望的字符串以指示成功。
*   根据故障性质显示测试失败时的故障排除建议。
*   测试失败时检查 HTTP 请求和响应。(如果成功，可选)。
*   测试失败时，通过各种检查(ping、http、nslookup)进行故障排除。(如果成功，可选)。
*   通过代理支持测试

**也可阅读-[pocsuite 3:开源远程漏洞测试框架](https://kalilinuxtutorials.com/pocsuite3-open-sourced-remote-vulnerability/)**

**安装**

**$ gem 安装 chkdfront**

**用途**

**帮助菜单:** -f，–前置目标 URL 前置目标域或 URL。
例如 images.businessweek.com
-d，–域前域 DomainFront domain。
例如 df36z1umwj2fze.cloudfront.net
-e，–Expect STRING 期待一个指示成功的给定字符串。(区分大小写)例如，它工作
-p，–提供商编号选择 CDN /域前端提供商:
[0]自动(默认–自动调整请求。

**检测额外请求)**
【1】Amazon(针对 Amazon 域前端的调优请求)
【2】Azure(针对 Azure 域前端的调优请求)
【3】Alibaba(针对 Alibaba 域前端的调优请求)

【t】，–trouble shooting[DOMAIN]强制故障排除过程。对所有参与方(可选:CDN 转发的原始域，包括在检查中)执行故障排除程序(ping、http、nslookup)，例如 c2.mydomain.com
–代理用户:PASS@HOST:PORT 如果您在代理之后，请使用代理设置。例如 user 1:pass 123 @ localhost:8080
–debug 强制调试。显示响应正文和低级请求和响应调试跟踪。(测试失败时默认启用。)
-h，–帮助显示此消息。 **用法:** /usr/local/bin/chkdfront
示例:
/usr/local/bin/chkdfront-f images.businessweek.com-d df36z1umwj2fze.cloudfront.net
/usr/local/bin/chkdfront-f images.businessweek.com-d df36z1umwj2fze.cloudfront.net-debug-t c2.mysite.com

[**Download**](https://github.com/KINGSABRI/chkdfront#usage)