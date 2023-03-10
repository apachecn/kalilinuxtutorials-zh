# XVNA–极端易受攻击的节点应用程序

> 原文：<https://kalilinuxtutorials.com/xvna/>

XVNA 是一个用 Nodejs(Expressjs)/MongoDB 编码的非常容易受到攻击的节点应用程序，它让安全爱好者开始学习应用程序安全性。不建议将此应用程序放在网上，因为它容易受到攻击。我们倾向于建议在本地设置中促进这种应用程序，并使用您自己选择的任何工具来磨练您的应用程序安全技能。阻碍或侵入这些都是合法的。这个想法是用最有可能是最好和最基本的方法向团队传播应用程序安全性。学习并获得这些能力是有原因的。尽管如此，你使用这些能力和物质并不是我们的职责。

# **警告**

极端易受攻击的节点应用程序(XVNA)是最易受攻击的，不要把它转移到你的主机提供商的公共文件夹或任何面向网络的服务器，因为它们会受到损害。建议使用 localhost。

#### **也读 [Evasi0n 苹果 iOS 7.x 的越狱工具& 6.x 用户](http://kalilinuxtutorials.com/evasi0n-jailbreaking/)**

# **设置 XVNA**

*   启动 mongoDB
*   在 mongoDB 中创建 DB xvna
*   将文件夹集合中给定的集合导入 mongoDB
*   使用命令从根文件夹启动 xvna:node index . js
*   我们准备好了，点击本地主机:3000/app
*   登录凭证:电子邮件-> admin@xvna.com 密码->密码

# **漏洞列表**

*   a1:2017-注射
    1.  口服注射
    2.  诺斯克注射液
    3.  服务器端 Js 注入

*   a2:2017-身份验证失败
*   a3:2017-敏感数据暴露
    1.  敏感数据
    2.  头球

*   a6:2017-安全错误配置
*   a7:2017-跨站点脚本
*   A8:2017-不安全的反序列化

更多信息请访问我们的博客

```
Created by Vegabird Team
```

[![](img/a51de913dc60eee505c4a68651ee8e4d.png)](https://github.com/vegabird/xvna#setup)