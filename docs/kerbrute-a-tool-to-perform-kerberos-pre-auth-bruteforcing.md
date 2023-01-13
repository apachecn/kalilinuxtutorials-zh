# Kerberos:一个执行 Kerberos 预授权强制的工具

> 原文：<https://kalilinuxtutorials.com/kerbrute-a-tool-to-perform-kerberos-pre-auth-bruteforcing/>

Kerberos 是一种通过 Kerberos 预认证快速强制和枚举有效活动目录帐户的工具。从发布版[页面](https://github.com/ropnop/kerbrute/releases/tag/v1.0.1)找到最新的二进制文件开始。

这个工具源于几年前我编写的一些 bash 脚本，使用 Linux 中的 Heimdal Kerberos 客户端执行暴力破解。

他们想要一些不需要特权就能安装 Kerberos 客户端的东西，当我发现 Kerberos [gokrb5](https://github.com/jcmturner/gokrb5) 惊人的纯 Go 实现时，他们决定最终学习 Go 并编写这个。

用 Kerberos 强制 Windows 密码比我所知道的任何其他方法都要快，而且可能更隐蔽，因为预认证失败不会触发“传统的”`**An account failed to log on**`事件 4625。

使用 Kerberos，只需向 KDC(域控制器)发送一个 UDP 帧，就可以验证用户名或测试登录。

**又读-[Twint:Twitter 智能工具](https://kalilinuxtutorials.com/twint-twitter-osint-intelligence/)**

**用途**

Kerbrute 有三个主要命令:

*   **bruteuser**–从单词列表中强制单个用户的密码
*   **passwordspray**–根据用户列表测试单个密码
*   **usernenum**–通过 Kerberos 枚举有效的域用户名

必须指定域(`-d`)或域控制器(`--dc`)。如果没有给定域控制器，将通过 DNS 查找 KDC。

默认情况下，Kerberos 是多线程的，使用 10 个线程。这可以通过`-t`选项改变。

输出被记录到 stdout，但是可以用`-o`指定日志文件。

默认情况下，不会记录故障，但可以用`-v`来更改。

最后，Kerbrute 有一个`--safe`选项。启用此选项后，如果某个帐户重新锁定，它将中止所有线程以停止锁定任何其他帐户。

`help`命令可用于获取更多信息

$ ./kerbrute
版本:v 1 . 0 . 0(43 f9ca 1)–03/06/19–Ronnie Flathers @ ROP nop

该工具旨在通过 Kerberos 预认证帮助快速破解有效的 Active Directory 帐户。
它被设计用于能够访问其中一个域控制器的内部 Windows 域。
警告:失败的 Kerberos 预授权算作失败的登录，并将锁定帐户

用法:
kerbrut[command]

可用命令:
bruteuser brute 从单词列表中获取单个用户的密码
帮助关于任何命令的帮助
passwords 请根据用户列表测试单个密码
userenum 通过 Kerberos 枚举有效的域用户名
版本显示版本信息并退出

标志:)如果为空，将通过 DNS
-d，–domain string 查找要使用的完整域(例如 contoso.com)
-h，–help kerbrute
-o，–输出字符串文件以写入日志。可选。
–安全模式。如果任何用户因被锁定而返回，将会中止。Default: FALSE
-t，–Threads int Threads to Use(缺省值 10)
-v，–详细日志失败和错误

使用“kerbrute[command]–help”了解有关命令的更多信息。

**用户枚举**

为了枚举用户名，Kerbrute 发送没有预认证的 TGT 请求。如果 KDC 响应一个`PRINCIPAL UNKNOWN`错误，则用户名不存在。

但是，如果 KDC 提示进行预认证，我们知道用户名存在，然后继续。这不会导致任何登录失败，因此不会锁定任何帐户。如果启用了 Kerberos 日志记录，则会生成 Windows 事件 ID 4768。

**root@kali:~#。/kerbrute _ Linux _ amd64 userenum-d lab.ropnop.com 用户名. txt

版本:dev(43 f9ca 1)–03/06/19–罗尼·弗拉瑟斯@罗普诺

2019/03/06 21:28:04 >使用 KDC(s):
2019/03/06 21:28:04>pdc01.lab.ropnop.com:88

2019/03/06 21 在 0.425 秒内测试了 1001 个用户名(2 个有效)**

**密码喷**

使用 passwordwpray，Kerbrute 将对域用户列表执行水平暴力攻击。当您有大量用户时，这对于测试一个或两个常用密码很有用。

**警告:**这将增加失败登录次数并锁定账户。这将生成两个事件 IDs 4768 请求了 Kerberos 身份验证票证(TGT ),以及 4771—Kerberos 预身份验证失败

root@kali:~#。/kerbrute _ Linux _ amd64 passwordspray-d lab.ropnop.com 域 _users.txt Password123

版本:dev(43 f9ca 1)–03/06/19–罗尼·弗拉瑟斯@罗普诺

2019/03/06 21:37:29 >使用 KDC(s):
2019/03/06 21:37:29>pdc01.lab.ropnop.com:88

2019 在 7.674 秒内测试了 2755 次登录(2 次成功)

原始用户

这是一个针对用户名的传统暴力帐户。只有在您确定没有锁定策略的情况下才运行此命令！

这将生成两个事件 IDs 4768 请求了 Kerberos 身份验证票证(TGT ),以及 4771—Kerberos 预身份验证失败

root@kali:~#。/kerbrute _ Linux _ amd64 bruteuser-d lab.ropnop.com 密码. lst thoffman

版本:dev(43 f9ca 1)–03/06/19–罗尼·弗拉瑟斯@罗普诺

2019/03/06 21:38:24 >使用 KDC(s):
2019/03/06 21:38:24>pdc01.lab.ropnop.com:88

2019/03/019 在 2.711 秒内测试了 1001 次登录(1 次成功)

**安装**

您可以从 releases 页面下载 Linux、Windows 和 Mac 的预编译二进制文件。如果你想生活在边缘，你也可以安装 Go:

**$ go 获取 github.com/ropnop/kerbrute
随着库的克隆，你也可以使用 Make 文件来编译通用架构:

$ make help
help:显示这个帮助。
windows:制作 windows x86 和 x64 二进制文件
linux:制作 linux x86 和 x64 二进制文件
mac:制作 Darwin (Mac) x86 和 x64 二进制文件
clean:删除任何二进制文件
all:制作 Windows、Linux 和 Mac x86/x64 二进制文件

$ make all
Done。
建筑为 windows amd64..
windows 386 的构建..
搞定。
构建 linux amd64…
构建 linux 386…
完成。
为 mac 建造 amd64…
为 mac 建造 386…
完成。

$ ls dist/
kerbrute _ Darwin _ 386 kerbrute _ Linux _ 386 kerbrute _ windows _ 386 . exe
kerbrute _ Darwin _ amd64 kerbrute _ Linux _ amd64 kerbrute _ windows _ amd64 . exe**

**信用:** jcmturner

[**Download**](https://github.com/ropnop/kerbrute)