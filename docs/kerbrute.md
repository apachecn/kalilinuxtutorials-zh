# Kerbrute:使用 Impacket 执行 Kerberos 强制的脚本

> 原文：<https://kalilinuxtutorials.com/kerbrute/>

[![](img/6d54f43e368f37797f56ca8f1426fec2.png)](https://blogger.googleusercontent.com/img/a/AVvXsEjlXLa-3ZyCoEjHyNLSCu939G5Sd-y2iYNNkFX2ltjHPjNMSjH3LrSZVDDxrUi0cQMxlmrMhPUSbSYgev6Zr8LLc1kLIhdGRBEZgKtmxL8stJNqeKBwft8YuqSGxZQWCu489ui2VSVhSKRrMbKijbur1kxqOXgY8FKBXywTFzSUBXnvPzeZNyZv0Kal=s728)

是一个通过使用 Impacket 库执行 kerberos 强制的脚本。

当执行时，作为输入，它接收用户或用户列表以及密码或密码列表。然后 is 执行暴力攻击来列举:

*   有效的用户名/密码对
*   有效用户名
*   无需预认证的用户名

因此，该脚本会生成一个发现的有效凭据列表，并根据这些有效凭据生成 TGT。

## 安装

来自 pypi:

**pip3 安装 kerbrute**

来自回购:

**git 克隆 https://github.com/TarlogicSecurity/kerbrute
CD kerbrute
pip install-r requirements . txt**

## 使用

没有参数的帮助:

**root @ kali:~ # kerbrute
Impacket v 0 . 9 . 18-Copyright 2018 secure auth Corporation
用法:kerbrute . py[-h][-debug](-USER USER |-USERS)
[-PASSWORD PASSWORD |-PASSWORDS]-DOMAIN 域域
[-DC-IP][-THREADS THREADS]
[-output file output file][-no-save-ticket]
可选参数:
-h， –帮助显示此帮助消息并退出
-调试打开调试输出
-用户用户用户执行暴力
-用户用户文件每行包含用户
-密码密码执行暴力
-密码每行包含密码的密码文件
-域域域执行暴力
-域控制器的 dc-ip IP 地址
-线程线程数执行暴力的线程数。 default = 1
-output File output File
保存发现的用户的文件:密码
-no-save-ticket 不保存检索到的具有正确凭证的 TGTs
示例:
。/kerbrute . py-users users _ file . txt-passwords _ file . txt-domain contoso.com**

执行示例:

**root @ kali:~ # kerbrute-domain Jurassic . park-users users . txt-passwords . txt-output file Jurassic _ passwords . txt
Impacket v 0 . 9 . 18–版权所有 2018 secure auth Corporation
【*】stampirance =>triceratops:sh 4 rph 0 rns[*]在 triceratops . ccache
[*]Valid user =>velociraptor【非预认证】[***

[**Download**](https://github.com/TarlogicSecurity/kerbrute)