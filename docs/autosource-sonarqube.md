# AutoSource:自动化源代码 SonarQube

> 原文：<https://kalilinuxtutorials.com/autosource-sonarqube/>

[![AutoSource : Automated Source Code SonarQube](img/45d779c0ed52130eab4811f582ae0215.png "AutoSource : Automated Source Code SonarQube")](https://3.bp.blogspot.com/-gfntC3n-4MQ/XNIhH6OrwYI/AAAAAAAAAJs/gNd58tP6na4I18SbdKKKMsuP6GtV5AY6gCLcBGAs/s1600/Screenshots-6%2B%25281%2529.png)

AutoSource 是一个自动化源代码审查框架，与 SonarQube 集成，能够执行静态代码分析/审查。

它可以在软件开发生命周期的早期有效地发现漏洞。用户只需将 GIT 库链接到框架中，就可以扫描代码。

AutoSource framework 能够在所有平台(MAC、Linux 和 Windows)上执行源代码审查。

**安装**

1.  将自动源存储库下载到您的系统中。
2.  阅读 prerequisites.txt 文件并安装依赖项(针对每个平台)
3.  执行 download sonar . py(python 3 download sonar . py)，这将下载并设置 SonarQube 框架，该框架可从' [http://127.0.0.1:9000](http://127.0.0.1:9000/) 访问
4.  之后，运行 execute scanner . py(python 3 execute scanner . py)，这将询问您想要扫描的 GIT 存储库。
5.  访问 SonarQube 门户网站( [http://127.0.0.1:9000](http://127.0.0.1:9000/) ')上的结果

**又读-[Bashter:网络爬虫，扫描器&分析器框架](https://kalilinuxtutorials.com/bashter/)**

**截图**

**下载 SonarQube 和 SonarScanner**

![](img/95735fa3de1a3e1c8f99365711687dce.png)

**sonar cube 启动并运行**

![](img/cde692f6ed7c31112ef221ce9c912eeb.png)

**执行扫描仪**

![](img/aefd2a1127e83e22aa000f49fe3c0a64.png)

**扫描开始**

![](img/aebccce07f1fecbaeb9496da2ef2e4e3.png)

**扫描仪执行成功**

![](img/d4d8d22c1a257ee4c6a57336efd5cea3.png)

**sonar cube 仪表盘中显示的结果**

![](img/a5cbadfc3556c6939c97927716639183.png)

**演职员表:**马尔基特·辛格&舒巴姆·舒班卡·夏尔马

[**Download**](https://github.com/Securityautomation/autoSource)