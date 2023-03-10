# 用户名枚举和侦察套件

> 原文：<https://kalilinuxtutorials.com/osinteye/>

[![](img/0e73b0d077f754debedc713477bb112a.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj_Q5Y9TEVccbucoU98h_QM0voyqEp9wjdr-ppuVWHPsi7S5EWLR0knQCtG34rQMJbQngVAX5yJ6AiC4XGJOpcSRvFa2vn6W8jEt5fNgsnE8wrbqTEPD4qjfq41ONZIBtKPmDf7aJhPNmqJI6_DVhG_zUdkGQ8f_MMEY5-H1sfW7nu1YOGCg7cmmY0w/s728/eb99c602-c172-4602-85b9-5ec21f754daa.png)

**Osinteye** 是一个用于用户名枚举的工具&侦察套件。

# 支持的网站

*   好吧
*   开源代码库
*   TestPypi
*   About.me
*   照片墙
*   DockerHub

# 安装

克隆项目:

**git 克隆 https://github . com/rly 0 nhart/osinteye . git**

**$ cd osinteye**

**$ pip install-r requirements . txt**

## 使用

**$ python osinteye[–站点名称][用户名]**

**或者给 osintEye 执行权限**:

**$ chmod +x osinteye**

**$。/osinteye[–站点名称][用户名]**

**例 1.1**；

**$ python osinteye–insta gram[用户名]**

**例 1.2**；

**$。/osinteye–insta gram[用户名]**

# 可选参数

| 旗 | 使用 |
| --- | --- |
| `**--pypi**` | *从 pypi 获取目标的信息* |
| `**--testpypi**` | *从 testpypi 中获取目标的信息* |
| `**--about**` | *从 about.me* 获取目标信息 |
| `**--instagram**` | *从 instagram 获取目标的信息* |
| `**--github**` | *从 github 获取目标信息* |
| `**--dockerhub**` | *从 dockerhub* 获取目标的信息 |
| `**-v/--verbose**` | *启用详细度(返回网络日志、错误和警告)* |
| `**--version**` | *显示程序的版本号并退出* |

[**Download**](https://github.com/rly0nheart/osinteye)