# 域名提醒:每天提醒当一个新的域名注册，并包含您的关键字

> 原文：<https://kalilinuxtutorials.com/domain-alerting/>

[![](img/559b12ed72ae468ca7b1331d277e1dbf.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgLDTVhchB_rUOONV9A0ux8-2dRscaqAOqT6hdXVtUa4x50UKebeK6h5Kmkoz8KjcSnz03_dzt7GFiknCiWQY23DFkIX4SOB6IrKETa_D1MhT4MHZYU4yX_Oy5wgSu7AyeX5Za_aGTS0y_fqkQnAR4Pk6BaA_ljZ7c_8is0dsbxuUsa8Og_-J_TuZfJ/s728/1%20(1).png)

**域名提醒**是当新域名注册并包含您的关键字时的每日提醒。

域警报工具允许您执行两个主要操作(仅用于教育目的):

*   下载新注册的域名

![](img/ec8a4f31a2986a380415f73d6281cc51.png)

*   发送自动电子邮件提醒

![](img/64e67ac15729935318e71cbef6664fdc.png)

# 先决条件

**apt 安装邮件程序
pip 3 install-r requirements . txt**

## 配置

在文件“launcher.sh”中，完成:

*   您的关键字(需要完成的关键字数量)
*   您的收件人(需要填写的电子邮件数量)

然后，创建一个每日 crontab 作业:

**crontab-e #编辑用户的 crontab
0 8 * * */path/launcher . sh #设置每日 crontab(这里以早上 8 点为例)**

[**Download**](https://github.com/pixelbubble/DomainAlerting)