# 理解情境化风险的工具

> 原文：<https://kalilinuxtutorials.com/vprioritizer/>

[![vPrioritizer : Tool To Understand The Contextualized Risk (vPRisk)](img/ce7ccb02e40e7fad9a9dd87e613e8282.png "vPrioritizer : Tool To Understand The Contextualized Risk (vPRisk)")](https://1.bp.blogspot.com/-3eP18oWkEBM/X4gpaShkyMI/AAAAAAAAHy8/cbQHbNfJrrMuOUtn-dEt3zwyXqNroGZgACLcBGAsYHQ/s728/vPrioritizer%25281%2529.png)

正如 vulndb & cve 等来源所指出的那样，每天大约有 50 个新的漏洞为业界所知，可以肯定的是，这个数字还会进一步增加。需要快速有效地评估和修复大量漏洞。因此，今天的组织正专注于(或应该专注于)降低风险，而不是消除风险，漏洞管理(几乎)等同于风险优先级排序，风险是一个由多种因素决定的可变动态概念。

从理论上讲，这种方法考虑了诸如基本 CVSS、资产可访问性、关键程度、利用可用性、业务敏感性等因素。看起来适合采用，但实际上不可能对影响每个组织的每个资产的每个漏洞都手动采用。

**目标&哲学**

为了克服上述挑战，vPrioritizer 的主要设计目标如下:

*   集中化—必须作为漏洞管理的单一平台
*   自动化——任何可以自动化的任务都必须自动化
*   社区分析–利用社区分析在一段时间内完善优先级算法

它是如何工作的？

vPrioritizer 使我们能够评估不同层面的风险，例如(并因此全面控制每个风险的粒度，如上文风险计算部分所述):

*   我们可以在每个资产的基础上分配重要性
*   我们可以在每个漏洞的基础上评估严重性
*   同时，我们可以在资产和漏洞关系级别调整这两个因素
*   最重要的是，社区分析提供了关于建议风险的见解

vPrioritizer 使我们能够通过组织中的每个漏洞了解与每个资产相关的上下文风险。它基于社区的分析为漏洞扫描器识别的每个漏洞提供了建议风险，并进一步加强了风险优先级排序流程。因此，在任何时间点，团队都可以根据统一和标准化的数据，就他们应该修复(或可以不修复)什么(漏洞/关系)和修复哪些(资产)做出有效和更明智的决策。

**快速入门**

*   **对于 Linux 用户:**

*   安装〔t0〕坞站〔T2〕坞站─化合物〔t1〕
    *   sudo apt-get 更新
    *   sudo apt-get install docker-ce docker-compose-复合式
*   wget【[】https://raw . githubusercontent . com/varchashva/vprioritzer/master/docker-compose . yml](https://raw.githubusercontent.com/varchashva/vPrioritizer/master/docker-compose.yml)
*   坞站-合成 up
*   浏览到 [http://localhost:7777/vp](http://localhost:7777/vp) ，您就可以开始探索这个工具了🙂

*   **针对 Windows & Mac 用户**

*   安装 [postgres](https://www.postgresql.org/docs/9.3/installation.html)
*   使用以下详细信息创建用户和数据库:
    *   用户名:vprioritizer
    *   密码:vprioritizer
    *   数据库名称:vprioritizer
*   https://github.com/varchashva/vPrioritizer.git
*   光盘优先权
*   python manage . py runserver 0 . 0 . 0 . 0:7777
*   浏览到 [http://localhost:7777/vp](http://localhost:7777/vp) ，您就可以开始探索这个工具了🙂

**演示**

[https://www.youtube.com/embed/P9IDpfJDoxI?feature=oembed&enablejsapi=1](https://www.youtube.com/embed/P9IDpfJDoxI?feature=oembed&enablejsapi=1)

[**Download**](https://github.com/varchashva/vPrioritizer)