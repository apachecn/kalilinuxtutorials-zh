# Django DefectDojo:开源应用程序漏洞关联和安全编排工具

> 原文：<https://kalilinuxtutorials.com/defectdojo/>

DefectDojo 是一个安全程序和漏洞管理工具。它允许您管理您的应用程序安全程序，维护产品和应用程序信息，安排扫描时间，筛选漏洞，并将发现结果推送到缺陷跟踪器中。用这个工具把你的发现整合成一个真实的来源。

**演示**

使用以下凭证在我们的[测试环境](https://defectdojo.herokuapp.com/)中试用它。

*   admin / defectdojo@demo#appsec
*   产品经理/defect Dojo @ demo #产品

**也读作——[混沌:允许生成有效载荷的 PoC&控制远程操作系统](https://kalilinuxtutorials.com/chaos-poc/)**

**快速启动**

**git 克隆 https://github . com/defect Dojo/django-defect Dojo
CD django-defect Dojo
docker-compose up**

导航到 [http://localhost:8080](http://localhost:8080) 。

**文档**

如需详细文档，请访问[阅读文档](https://defectdojo.readthedocs.io/)。

**安装选项**

*   [Kubernetes](https://github.com/DefectDojo/django-DefectDojo/blob/master/KUBERNETES.md)
*   [码头工人](https://github.com/DefectDojo/django-DefectDojo/blob/master/DOCKER.md)

**入门**

我们建议查看[关于](https://defectdojo.readthedocs.io/en/latest/about.html)的文档以了解该工具的术语，并查看[入门指南](https://defectdojo.readthedocs.io/en/latest/getting-started.html)以设置新的安装。

我们还创建了一些示例[工作流](https://defectdojo.readthedocs.io/en/latest/workflows.html),这应该会让你知道如何在你自己的团队中使用它。

**客户端 API**

*   通过`**pip install defectdojo_api**`安装 DefectDojo Python API 或者克隆[库](https://github.com/aaronweaver/defectdojo_api)。
*   浏览 [SwaggerHub](https://app.swaggerhub.com/apis/DefectDojo/defect-dojo_api_v_2/1.0.0) 上的 API。

**可用插件**

*   [参与度调查](https://github.com/grendel513/defectDojo-engagement-survey)–一个将可回答的调查添加到参与度的插件。
*   [LDAP 集成](https://django-auth-ldap.readthedocs.io/en/latest/)
*   [SAML 集成](https://pypi.python.org/pypi/djangosaml2/)
*   [多因素认证](https://django-mfa.readthedocs.io/en/latest/)

[**Download**](https://github.com/DefectDojo/django-DefectDojo)