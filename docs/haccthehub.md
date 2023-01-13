# Hacc The Hub:开源自托管网络安全学习平台

> 原文：<https://kalilinuxtutorials.com/haccthehub/>

[![](img/14dac769246a5271549ddf67f68d156b.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhcslqcKrUtXwVlQ7EZbErg5HejmH7rTpkQ3biv0ANdpW3Vxiz9D83dW9JQvSO2zXXS1asbr06CU_p3fsR_l1lv2nA-0i5MZ-X3lagBR0DDFGS4EXalRyg6Ds8R_jydmEJG0iPsgyaMSp9K5fehWe4UXNgNRf83Ujw4S9kEe5q6lMo4HbGS7WEA5mwW/s728/download%20(1).png)

Hacc The Hub 是一个提供网络安全的开源项目

Hacc Hub 系统由 3 个主要部分组成:

*   Docker:包含所有创建我们将要学习的环境的盒子。
*   后端:控制 Docker，负责启动/销毁系统中的单个盒子，并管理将它们连接成统一系统的网络。
*   前端:用户通过 web 浏览器与系统交互的 GUI。

### 建有

*   烧瓶-RESTX
*   Next.js

## 入门指南

要启动并运行 HaccTheHub，您需要设置以下内容

### 先决条件

*   Docker(参考 Docker 的文档进行设置)
*   Python 3(下载)或者从你的包管理器安装`**python3**`。
*   Node.js 16(下载)或使用您的包管理器

### 安装

*   克隆回购

**git 克隆 https://github . com/j4 fsec/haccthehub . git**

*   为后端安装依赖项

**CD hacthehub/back end
python 3-m pip install-r requirements . txt**

*   和对前端的依赖性

**cd../客户端
npm 安装**

## 使用

*   启动码头工人
*   启动后端

**cd../backend
python3 main.py**

前端呢

**cd../客户端
npm 开始**

现在应该可以通过 http://localhost:8080 访问 WebUI 了。

[**Download**](https://github.com/J4FSec/HaccTheHub)