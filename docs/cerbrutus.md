# Cerbrutus:网络暴力工具，用 Python 写的

> 原文：<https://kalilinuxtutorials.com/cerbrutus/>

[![](img/16343e47f6bf6e438daf8c91152d5110.png)](https://1.bp.blogspot.com/-hNAN5nOHtHE/YSh3IB5rzhI/AAAAAAAAKlU/OP5K_HZDXTUnty-mloMO5pgD4jOtWH4qgCLcBGAsYHQ/s674/3.png)

Cerbrutus 是一个用 Python 编写的模块化暴力工具，用于非常快速的密码喷射 SSH、FTP 以及不久的将来的其他网络服务。

即将推出: **SMB、HTTP(s) POST、HTTP(s) GET、HTTP BASIC AUTH** *感谢@0dayctf、Rondons、Enigma、001 的测试和贡献*

**安装**

**cd /opt
git 克隆 https://github . com/cerbrutus-brutus/cerbrutus**

**用途**

**python 3/opt/cerbrutus/cerbrutus . py–help
用法:cerbrutus.py [-h] -U USERS -P 密码[-p 端口] [-t 线程] [-q [QUIET [QUIET …]]]主机服务
基于 Python 的网络暴力破解工具！
位置参数:
Host 要连接的主机-以 IP 或 VHOST/域名的形式
Service The Service to brute force(目前实现了‘SSH’)
可选参数:
-h，–help 显示此帮助消息并退出
-U USERS，–USERS USERS
要么是单个用户，要么是您希望使用的用户的文件路径
-P password，–PASSWORDS
要么是单个密码， 或者您希望使用的密码列表的路径
-p PORT，–PORT PORT 您希望指向的端口(仅在非标准端口上运行时需要)
-t THREADS，–THREADS THREADS
要使用的线程数
-q [QUIET [QUIET …]，–QUIET[QUIET[QUIET…]]
不打印横幅**

**/opt/cerbrutus/cerbrutus . py 10 . 10 . 10 . 10 SSH-U " username "-P/opt/word lists/fast track . txt-t 10
= = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = =
***_ */]/*| \\ | | | | | | |/*//
///[*| D)| O)| D)| | | |(_
//| |*]|/| |/| |*| | | | | |*| | | | |
/_[_ | ^ | ^ | ^ |:| | |:|/\ |
\ | |
|。 | || .\ | | | | |
_ _ _ _ _ _ _ | |*| | _ |*| | _ | ^ _ _ ^ _ ^， *| || _* ，_| _|
网络暴力工具
，_ | _ |
= = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = = =
[*–初始化密码列表…从/中读入 224 个单词*******

**试运行**

**#密码在 rockyou 中行号 12600
64 个线程- > 1400 秒~ 7 分钟(九头蛇用了 30 分钟)
1000 个线程- > 464 秒- >每秒 27 个请求
100 个线程用了 1000 秒- >每秒 12 个请求
# 密码在第 460 行
100 个线程用了 32 秒- >每秒 14 个请求
1000 个线程用了 16 秒- >每秒 28 个请求
64 个线程用了 51 秒- >每秒 9 个请求(hydra 用了同样的时间)
# word number 20k in rock you
1100 个线程用了 637 秒这意味着 31 个 rps
110 个线程用了 1457 秒所以**

使用 paramiko 的自定义实现来克服为 ssh 强制实现它的一些小问题。https://github.com/paramiko/paramiko/

[**Download**](https://github.com/Cerbrutus-BruteForcer/cerbrutus)