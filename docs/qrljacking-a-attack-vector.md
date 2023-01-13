# QRLJacking:一种新的社会工程攻击载体

> 原文：<https://kalilinuxtutorials.com/qrljacking-a-attack-vector/>

QRLJacking 或快速响应代码登录劫持是一种简单的社会工程攻击媒介，能够进行会话劫持，影响所有依赖“使用 QR 代码登录”功能作为安全登录帐户方式的应用程序。

简而言之，受害者扫描攻击者的二维码，从而导致会话劫持。

**也读-[MySQL 魔法:从内存中转储 MySQL 客户端密码](https://kalilinuxtutorials.com/mysql-magic-dump-mysql/)**

**技术论文**

澄清 QRLJacking 攻击媒介的技术论文可以直接通过我们的 Wiki 找到。
易受攻击的 Web 应用程序和服务

在我们撰写本文之前，许多知名的 web 应用程序和服务都容易受到这种攻击。以下是一些例子(我们已经报道过)，包括但不限于:

**聊天应用**

WhatsApp，微信，Line，微博，QQ 即时通讯

**邮寄服务**

QQ 邮件(个人和企业)、Yandex 邮件

**电子商务**

阿里巴巴，速卖通，淘宝，天猫，1688.com，阿里妈妈，淘宝旅行

**网上银行**

支付宝，Yandex Money，财付通

**护照服务“关键”**

Yandex Passport (Yandex 邮件、Yandex 货币、Yandex 地图、Yandex 视频等)

**手机管理软件**

机械人

**其他服务**

MyDigiPass、Zapper & Zapper WordPress 通过二维码插件、可信应用、Yelophone、阿里巴巴尤诺斯登录

**演示视频**

攻击 WhatsApp 网络应用程序并执行 MITM 攻击，以注入包含 WhatsApp 二维码的虚假广告

https://www.youtube.com/watch?v=JCoPSdQvESc

信用:穆罕默德·阿卜杜勒·巴赛特·埃尔努比

[Download](https://github.com/OWASP/QRLJacking)