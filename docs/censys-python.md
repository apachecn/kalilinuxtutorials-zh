# Censys-Python:Censys 搜索引擎的一个易于使用的轻量级 API 包装器

> 原文：<https://kalilinuxtutorials.com/censys-python/>

[![Censys-Python : An Easy-To-Use & Lightweight API Wrapper For The Censys Search Engine](img/d423da375d5878e585483bc619786740.png "Censys-Python : An Easy-To-Use & Lightweight API Wrapper For The Censys Search Engine")](https://1.bp.blogspot.com/-1VslA1054r8/X-pNJUqIfxI/AAAAAAAAIOg/eYEL83d3ZiQMeWekVL2Wt_x1ijucNl88ACLcBGAsYHQ/s728/Censys%25281%2529.png)

**Censys-Python** 是 Censys 搜索引擎( [censys.io](https://censys.io/) )的一个易于使用的轻量级 API 包装器。目前支持 Python 3.6+版本。

**入门**

可以使用`pip`安装该库。

**$ pip 安装许可系统**

要配置您的凭证，运行`**censys config**`或者设置`**CENSYS_API_ID**`和`**CENSYS_API_SECRET**`环境变量。

**$ Censys config

Censys API ID:XXX
Censys API Secret:XXX
your@email.com 认证成功**

**开发**

**$ git 克隆 git @ github . com:censys/censys-python . git
$ pip install-e "。[dev]"**

**测试**

测试需要设置凭据。

**$ pytest**

[**Download**](https://github.com/censys/censys-python)