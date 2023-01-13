# Shreder:一个强大的多线程 SSH 协议密码暴力工具

> 原文：<https://kalilinuxtutorials.com/shreder/>

[![Shreder : A Powerful Multi-Threaded SSH Protocol Password Bruteforce Tool](img/58bf603b1dd2597114939dfb25c694ca.png "Shreder : A Powerful Multi-Threaded SSH Protocol Password Bruteforce Tool")](https://1.bp.blogspot.com/-zS7qxaxQTnE/YN7l33k3X_I/AAAAAAAAJyI/rq3wNrq6TB4o2_XbCmvRqPc1ZbA_IorgACLcBGAsYHQ/s728/Shreder%25281%2529.png)

**Shreder** 是一个强大的多线程 SSH 协议密码暴力破解工具。

**特性**

*   非常快速的密码猜测，在`**0.1**`秒内只需一个密码。
*   针对大型密码列表进行了优化，Shreder 在 **`1`** 分钟和 **`40`** 秒内尝试 1000 个密码。
*   简单的 CLI 和 API 用法。

**安装**

**pip3 安装 git+https://github . com/enty sec/Shreder**

**基本用法**

要使用 Shreder，只需在终端中输入 **`shreder`** 。

**用法:shreder [-h] [-p 端口] [-u 用户名] [-l 列表]目标
Shreder 是一款功能强大的多线程 SSH 协议密码暴力工具。
位置参数:
目标
可选参数:
-h，–help 显示此帮助信息并退出
-p 端口，–PORT PORT SSH 端口。
-u 用户名，–用户名用户名
SSH 用户名。
-l 列表，–列表列表密码列表。**

**例题**

**强力攻击单个目标**

让我们暴力破解我的设备，只是为了好玩。

**shreder 192 . 168 . 2 . 109-u mobile-l passwords . txt**

**API 使用**

Shreder 也有自己的 Python API，可以通过将 Shreder 导入到您的代码中来调用。

**从 shreder 导入 Shreder**

**基本功能**

有各种 Shreder 基本函数可以用来暴力破解单个目标。

*   `**connect(host, port, username, password)**`–通过给定地址连接单个目标。
*   `**brute(host, port, username, dictionary)**`–根据给定地址强力攻击单个目标。

**例题**

**强力攻击单个目标**

**从 shreder 导入 Shreder
Shreder = Shreder()
password = Shreder . brute(192 . 168 . 2 . 109，22，' mobile '，' passwords . txt ')
print(password)**

[**Download**](https://github.com/EntySec/Shreder)