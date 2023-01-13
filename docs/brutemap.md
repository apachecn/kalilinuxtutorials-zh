# Brutemap:让我们找到某人的帐户

> 原文：<https://kalilinuxtutorials.com/brutemap/>

[![Brutemap : Let’s Find Someone’s Account](img/baa710ba1ee04ea752c936ca89d0cc23.png "Brutemap : Let’s Find Someone’s Account")](https://3.bp.blogspot.com/-wRLX3xp8DVs/XOQsb3V1EBI/AAAAAAAAAZ8/V5d_gGImcqUnA5zzslaR8NeS9aJa2ut8gCLcBGAs/s1600/brutemap.png)

**Brutemap** 是一款开源渗透测试工具，基于**字典攻击**，自动测试网站登录页面的账户。

有了这个，你不再需要搜索其他的*暴力*工具，你也不再需要问 **CMS 这是什么？**只能找到*参数*的表格，因为它会自动完成。

它还配备了一种攻击方法，使您可以轻松地使用 SQL 注入旁路认证技术进行帐户检查或测试表单。

**也可阅读-[Pown Recon:由图论](https://kalilinuxtutorials.com/pown-recon-a-powerful-target-reconnaissance-framework-powered-by-graph-theory/)驱动的强大目标侦察框架 **

**安装**

**It** 使用 **selenium** 与网站交互。所以，你需要先为 selenium 安装 **Web 驱动**。见[此处](https://www.seleniumhq.org/docs/03_webdriver.jsp)。如果您已经安装了`git`包，那么您只需要克隆存储库 [Git](https://github.com/brutemap-dev/brutemap) 。像这样:

**git 克隆 https://github . com/bruemap-dev/bruemap . git**

并且，安装所需的模块:

**$ pip install-r requirements . txt**

**用法**

对于基本用途:

**$ python brute map . py-t http://www.example.com/admin/login.php-u admin-p 默认**

要显示可用选项列表:

**$ python brutemap.py -h**

[**Download**](https://github.com/brutemap-dev/brutemap)