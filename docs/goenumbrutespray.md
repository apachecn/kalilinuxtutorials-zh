# goenumbrutesplay:Azure、ADFS、OWA、O365 上的用户枚举和密码暴力，以及在 Linkedin 上收集电子邮件

> 原文：<https://kalilinuxtutorials.com/goenumbrutespray/>

[![](img/0c04504c8985cc369fd3f0f7f5e3172b.png)](https://blogger.googleusercontent.com/img/a/AVvXsEj3A498XzZjmDGDE2qQmrI1iX5qLExuFUOkdW7vXO3gKIT7-9di4zYyk8d11632WXlnSDJJcloYSqCxWanMiM4yxsgY-gfUnJE8_Y3Ql09TwaOMW3524ZgkHmGFLcPi-v-ldmY6ErV7DC1LFPWbgmgO3ycbvqgi6jtsU_TN-zpOy3KMk15cL7IUiU5s=s728)

对于用户枚举和密码强制/喷射，建议模块为 o365。可以检索附加信息以避免帐户锁定，了解密码有效但已过期，MFA 已启用，…

**Linkedin**

在通过用户枚举模块验证电子邮件地址之前，应该使用该模块来检索电子邮件地址列表。将在 Linkedin 上搜索该公司，并以指定的格式返回在这些公司工作的所有人员。

Linkedin 的会话 cookie `li_at`是必需的。

![](img/0db708d343db712bd07e4f99f5c40388.png)

**搜索引擎**

在通过用户枚举模块验证电子邮件地址之前，应该使用该模块来检索电子邮件地址列表。公司名称会带着呆瓜在 Google 和 Bing 上搜索，找到在公司工作的人(`site:linkedin.com/in+"%s"`)。结果标题将被解析为指定格式的输出电子邮件地址。

![](img/29cc5bbe59411e1d70ace4e57f5023b3.png)

**蔚蓝色**

**用户枚举**

Azure 模块仅可用于枚举租户的用户。认证请求将在`https://autologon.microsoftazuread-sso.com`提出，详细的响应显示如果账户不存在，需要 MFA，如果账户被锁定，…

![](img/78abaa6812fb6b29c17176ea43e53c19.png)

**ADFS**

**密码暴力/喷雾**

ADFS 模块只可用于暴力或喷射密码。认证请求被发送到`https://<target>/adfs/ls/idpinitiatedsignon.aspx?client-request-id=<randomGUID>&pullStatus=0`。如果密码过期，错误消息会通知用户

![](img/02763005c9ccb78da1843c7404527dd4.png)

**O365**

该模块允许枚举用户和暴力/喷射密码。

**用户枚举**

有几种模式可用:office、oauth2 和 onedrive(尚未实现)。建议使用办公模式，因为不进行身份验证。Oauth2 可以通过 [AADSTS 错误代码](https://docs.microsoft.com/en-us/azure/active-directory/develop/reference-aadsts-error-codes)检索附加信息(MFA 启用、锁定帐户、禁用帐户)

![](img/ffe7d4c34b2c9a50300de3bcc709bfc2.png)

**密码暴力/喷雾**

至于用户枚举，有两种模式可用:oauth2 和 autodiscover(尚未实现)。Oauth2 是推荐的模式，由于有了 [AADSTS 错误代码](https://docs.microsoft.com/en-us/azure/active-directory/develop/reference-aadsts-error-codes)，它可以获得更多信息。

![](img/950e19ea2d1f11da7d5c28c72d584a6c.png)

**OWA**

该模块允许枚举用户和暴力/喷射密码。

**用户枚举**

通过身份验证请求进行枚举。对不存在的用户进行身份验证比对有效用户进行身份验证需要更长的时间。首先，计算无效用户的平均响应时间，然后比较每个身份验证请求的响应时间。

![](img/2b7c2ad9842245a08cc3d44ab26206bf.png)

**密码暴力/喷雾**

请注意，不能实现任何帐户锁定机制，因为没有关于它的信息被返回。

![](img/da8fd1cf7a959dde2a66250683a583fb.png)[**Download**](https://github.com/nodauf/GoMapEnum)