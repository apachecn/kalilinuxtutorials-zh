# 网络钓鱼模拟:通过提供直观的教程和定制的评估来提高网络钓鱼意识

> 原文：<https://kalilinuxtutorials.com/phishing-simulation/>

[![Phishing Simulation : Increase Phishing Awareness By Providing An Intuitive Tutorial & Customized Assessment](img/23ab6c380519bb774dd91edcc4159ac7.png "Phishing Simulation : Increase Phishing Awareness By Providing An Intuitive Tutorial & Customized Assessment")](https://1.bp.blogspot.com/-8lpPh0JKCnQ/XXTcUotaQ2I/AAAAAAAACaM/hTPIQUBz7WQOV22zpdOEIbcKoTPxMndDACLcBGAs/s1600/Untitled.png)

**网络钓鱼模拟**主要旨在通过提供直观的教程和定制的评估(无需任何实际设置——无域名、无基础设施、无实际电子邮件地址)来评估人们在任何给定情况下的行动，从而提高网络钓鱼意识，并提供了解当前意识状态的能力。

**什么？**

*   执行红队评估的组织的目标之一是了解 IT 生态系统(包括人员和网络)中的弱点。组织尽一切努力改善外围安全并修补发现的漏洞，但人员仍然是最薄弱的环节。网络钓鱼对了解员工的安全意识起着至关重要的作用。
*   通过利用引人入胜且直观的培训课程，网络钓鱼模拟使用户无需实际执行“实时”网络钓鱼攻击就能理解它。
*   工具将为您提供一个定制的环境，根据您的要求设计您的测试，使问题为每个组织量身定制，为每个人量身定制，接近实时网络钓鱼攻击，有针对性，难以回答，但所有这些都没有任何实际设置。一旦测试设计完成，所有目标受众都可以参加评估并提交答案。我们将在活动结束时进行分析，以了解当前的认知态势。
*   只需一次点击！因此，这将使我们在点击之前三思。

**为什么？**

*   在进行红队评估时，建立整个网络钓鱼活动是一项艰巨的任务。决定一个域名，购买它，建立一个钓鱼网站，设计一封电子邮件，选择目标受众跟踪点击，只知道谁点击了他们，并有意识。
*   这需要时间和专业知识来设置。
*   工具将帮助你做这一切，你只需点击几下(这些点击是合法的，并帮助你:))
*   人是最不可预测的，这个工具将帮助你了解他们和他们的点击模式。

**也可阅读-[Http 请求走私者:为打嗝套件](https://kalilinuxtutorials.com/http-request-smuggler-extension-burp-suite/)扩展 **

**功能及如何使用**

工具主要有两个模块:

1.  管理模块:有权访问设置测试和视图分析，可在[访问 http://localhost/admin panel/log in . PHP](http://localhost/AdminPanel/login.php)，默认登录凭证为 admin/admin
2.  客户端模块:只能访问教程和评估，可通过[http://localhost/phish client/](http://localhost/phishClient/)访问

*   教程(客户端模块)
    *   这将有一本介绍网络钓鱼和一般技术使用的教程，这将创造意识和教育。
*   评估(客户端模块)
    *   这将包括各种问题，可能是钓鱼电子邮件或钓鱼网站或场景，用户必须选择他们是否会点击它，忽略它或报告它。
    *   即使在相同的测试代码下，每个用户的问题也是不同的。
    *   问题将有一个正面和负面问题的公平组合。
    *   要通过测试，所有答案必须正确，因为只需点击一下！
*   设置测试(管理模块)
    *   工具会在这里向您询问一些基本信息。举几个例子，
        *   域名:在这里你将输入你的合法域名，工具将创建一组看起来像是敌人可以用来攻击你的域名。您可以选择其中一个在您的网络钓鱼模拟评估中使用。
        *   URL:在这里，您将输入您常用的网站 URI，我们将创建一个外观相似的钓鱼网站，该网站将显示在您选择的外观相似的域下，以在评估期间创建现实生活场景，也称为“域名抢注”。
        *   测试代码:您可以为每个部门创建一个测试代码，并为他们创建不同的测试配置，这样每个人都会得到不同的钓鱼网站，从而使评估更加困难。即使在相同的测试中，每个员工的问题集也是不同的。
        *   预览:您可以预览外观和感觉的钓鱼网页，我们已经创建了看起来像你的原始网站。
        *   电子邮件 id:您应该在这里添加一个官方电子邮件 Id，它通常用于大众传播，我们将生成更多这样的电子邮件 Id 组合，并在评估过程中使用它们。
*   分析(管理模块)
    *   这将有一个基于员工回答问题的模式的不同场景的分析图。
    *   这将有助于了解组织当前的意识状态。

**好处**

*   这将消除手动设置整个网络钓鱼活动和“实时”网络钓鱼环境的需要。
*   评估是定制的，这将使它对目标用户进行有针对性的攻击。
*   一个直观的交互式界面来练习整个过程。
*   不需要有笔测试或顾问来进行网络钓鱼运动，你可以自己做一些点击。
*   了解你的员工并让他们意识到。

**安装指南**

**码头工人**

即将更新

**手动安装适用于 Windows(类似的应该适用于 Linux)**

*   从–[https://www.apachefriends.org/download.html](https://www.apachefriends.org/download.html)下载 XAMPP，并按照屏幕上的安装流程进行操作。它将为您安装 webserver 和 MySQL。
*   如果你不想和 XAMPP 一起去，你可能有的任何网络服务器和 MySQL 的独立安装应该足够了。
*   根据您的选择，完成第 1 步或第 2 步后，在 XAMPP 控制面板上启动“Apache”和“MySQL”服务。
*   在浏览器上打开[http://localhost/phpmyadmin/](http://localhost/phpmyadmin/)或 [http://IP/phpmyadmin/](http://ip/phpmyadmin/) 。
*   单击“数据库”创建名为“phishadmin”的数据库
*   单击“Import ”,将此处附带代码的文件导入/sql/ folder phishadmin.sql 下
*   将源代码复制到 C:\xampp\htdocs\ folder 下(路径因 linux 用户而异),安装就完成了。

[**Download**](https://github.com/jenyraval/Phishing-Simulation)