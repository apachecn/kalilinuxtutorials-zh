# 反垃圾邮件:检测一次性电子邮件地址

> 原文：<https://kalilinuxtutorials.com/antidisposmail-detecting-disposable-email-addresses/>

[![AntiDisposmail : Detecting Disposable Email Addresses](img/960dc2e87fb4b9e8ed3070a2269ff723.png "AntiDisposmail : Detecting Disposable Email Addresses")](https://1.bp.blogspot.com/-wrLGsImUw5w/Xe1SRBnlD5I/AAAAAAAAD2M/UOxV7CceK4AOUkA3AcKOXUWzVPTASkzrQCLcBGAsYHQ/s1600/AntiDisposmail.png)

**AntiDisposmail** 是一款检测一次性电子邮件地址的工具。Antbot.pw 提供了一个免费的、开放的 API 端点，用于根据频繁更新的可任意使用的域列表来检查域或电子邮件地址。所有原始域都启用了 CORS，因此您可以直接从客户端代码调用 API。

**获取 https://antibot.pw/api/disposable?email=radenvodka@0815.su HTTP/1.1**

响应将是带有一个布尔属性的 JSON，例如`**{"disposable":false}**`

**也可阅读-[CodeCat:在 code review](https://kalilinuxtutorials.com/codecat-manual-analysis-codereview/)T3 中帮助手动分析的工具**

**使用 jQuery**

**<脚本>
$( "#email ")。change(function(){
var val = $(" # email ")。val()；
$。get(' https://anti bot . pw/API/disposable？email='+val，
函数(data，text status){
if(data[' disposable ']= = true){
alert(" email disposable ")；
}
})；
})；
</脚本>**

[**Download**](https://github.com/anti-bot/AntiDisposmail)