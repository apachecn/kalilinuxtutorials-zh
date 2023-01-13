# 电报刮刀:电报组刮刀工具

> 原文：<https://kalilinuxtutorials.com/telegram-scraper/>

[![TeleGram-Scraper : Telegram Group Scraper Tool](img/5fb99f091ff167efc01eb9d8c3568c92.png "TeleGram-Scraper : Telegram Group Scraper Tool")](https://1.bp.blogspot.com/-oDK0MHt9N5c/XinTaTxnsOI/AAAAAAAAEjU/GHCcylj2bC01QsE6nW8GzPHyWtjqv-pDgCLcBGAsYHQ/s1600/20191203_205322.png)

**电报刮刀**是一个电报群组刮刀工具，用于获取群组成员的所有信息。

**如何安装&设置 API ( Termux )**

https://youtu.be/I8oR9tuYyrU

**API 设置**

*   前往[http://my.telegram.org](http://my.telegram.org)并登录。
*   单击 API 开发工具并填写必填字段。
*   输入您想要的应用名称，并在平台中选择其他示例:
*   单击创建应用程序后，复制“api_id”和“api_hash ”(将在 setup.py 中使用)

**也可阅读-****[blue wall:专为进攻方设计的防火墙框架&防御方网络专业人士](https://kalilinuxtutorials.com/bluewall/)**

**如何安装和使用**

**$ pkg install -y git python**

**$ git 克隆 https://github.com/th3unkn0n/TeleGram-Scraper.git**

**$ cd 电报刮刀**

*   安装要求

**$ python3 setup.py -i**

*   安装配置文件(apiID，apiHASH)

**$ python3 setup.py -c**

*   生成用户数据

**$ python3 scrapr.py**

*   (members.csv 是默认值，如果您更改了名称，请使用它)
*   向收集的数据发送批量短信

**$ python 3 SMS bot . py members . CSV**

*   将用户添加到您的组中(开发中)

**$ python 3 add 2 group . py members . CSV**

*   更新工具

**$ python3 setup.py -u**

[**Download**](https://github.com/th3unkn0n/TeleGram-Scraper)