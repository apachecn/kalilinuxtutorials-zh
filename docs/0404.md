# Pwndb:搜索泄漏的凭据

> 原文：<https://kalilinuxtutorials.com/pwndb-search-leaked-credentials/>

Pwndb 是一个 python 命令行工具，用于使用同名的洋葱服务搜索泄漏的凭证。

**用途**

用法:pwn db . py[-h][–TARGET TARGET][–LIST LIST LIST][–OUTPUT OUTPUT]
可选参数:
-h，–help 显示此帮助消息并退出
–TARGET TARGET email/domain 以搜索漏洞。
–LIST 列出文件中的电子邮件列表，以查找漏洞。
–输出输出返回结果为 json/txt

注意:tor 服务必须启动并运行，才能在端口 9050 上与其连接

**也可理解为:** [Windows 95:在 macOS、Linux 和 Windows 上运行的电子版 Windows 95](https://kalilinuxtutorials.com/windows-95/)

**安装**

只需创建一个 virtualenv，安装需求并确保 Tor 正在运行。

$ git 克隆 https://github.com/davidtavarez/pwndb
克隆到‘pwn db’…
远程:枚举对象:10，完成。
远程:清点对象:100% (10/10)，完成。
远程:压缩对象:100% (9/9)，完成。
远程:总计 10(增量 2)，复用 4(增量 0)，打包复用 0
拆包对象:100% (10/10)，完成。
$ CD pwn db
$ virtualenv venv
在/Users/davidtavarez/pwn db/venv/bin/python
中新建 python 可执行文件安装 setuptools、pip、wheel…完成。
$ source venv/bin/activate
(venv)$ pip install-r requirements . txt
收集 py socks = = 1 . 6 . 8(from-r requirements . txt(line 1))
…
(venv)$ python pwn db . py-h
用法:pwn db . py[-h][–TARGET TARGET][–LIST][–OUTPUT]
可选参数:
-h，–help 显示此帮助
–LIST 列出文件中的电子邮件列表，以查找漏洞。
–以 json/txt 格式输出输出返回结果

**免责声明**

未经双方事先同意，使用 pwndb.py 攻击目标是非法的。最终用户有责任遵守所有适用的地方、州和联邦法律。开发人员不承担任何责任，也不对任何误用或造成的损坏负责。

[**Download**](https://github.com/davidtavarez/pwndb)