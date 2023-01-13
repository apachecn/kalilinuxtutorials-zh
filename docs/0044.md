# Mozilla 为 Firefox 帐户增加了两步认证支持

> 原文：<https://kalilinuxtutorials.com/two-step-authentication/>

Mozilla 正在推进一个两步认证过程来支持 Firefox 账户。身份验证框架利用 Firefox Sync 的有用性来保护书签、密码、开放标签和其他设备间数据的同步。

按照 Mozilla build Vijay Budhram 的说法，这个组件不断被提升到客户端，它不依赖于 SMS 代码。

相反，该框架利用由标准 TOTP(基于时间的一次性密钥)应用程序和服务创建的验证码，如 Authy、Duo、Google Authenticator 等。

**又读[Droid Hunter——安卓应用漏洞工具](http://kalilinuxtutorials.com/droid-hunter/)**

随着功能的呈现，Firefox 客户端可以在未来几周内检查他们的记录倾向，并在可以访问时授权它。

此外，用户可以跳过等待，立即启用两步身份验证，方法是访问:

```
https://accounts.firefox.com/settings?showTwoStepAuthentication=true
```

当客户启用对**两步认证**的支持时，他们会额外获得一组恢复代码，以防失去对 TOTP 权益的访问。客户应将这些代码保存在受保护的地方(在线或离线),以便在危机中使用它们来重新访问他们的记录。

启用 2FA 帮助后，每次客户登录他们的 Firefox 帐户时，他们应该在第一步输入用户名和密钥，在第二步输入由 TOTP 福利产生的安全代码。

由于 Firefox 帐户存储非常敏感的数据(如密码)，特别建议客户在他们的记录倾向可访问时快速打开。

[![](img/a51de913dc60eee505c4a68651ee8e4d.png)](https://securityonline.info/mozilla-adds-two-step-authentication-support-for-firefox-accounts/)