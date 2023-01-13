# swego:Golang 的瑞士军刀网络服务器

> 原文：<https://kalilinuxtutorials.com/swego/>

[![Swego : Swiss Army Knife Webserver In Golang](img/8ca8c7048be5d0ffb92e00690a99c173.png "Swego : Swiss Army Knife Webserver In Golang")](https://1.bp.blogspot.com/-G-nw0xNT1aA/X-pKlaN3T4I/AAAAAAAAIOU/S4k4CwbdClg-BUPWXC6533bqTQFdc5vLwCLcBGAsYHQ/s728/Swego%25281%2529.png)

Swego 是一个位于 Golang 的瑞士军刀网络服务器。像 python SimpleHTTPServer 一样保持简单，但具有许多特性。

**用途**

**运行二进制程序**

如果你不想构建它，可以在 https://github.com/nodauf/Swego/releases 上找到二进制文件

否则，应该安装 build-essential 并配置 GOPATH:

**git 克隆 https://github.com/nodauf/Swego.git
CD Swego/src
make compile Linux #或 make compileWindows**

**帮助**

**$。/webserver -help
web 子命令
-绑定字符串
绑定端口(默认为“8080”)
-证书字符串
HTTPS 证书:OpenSSL req-new-x509-sha 256-Key server . Key-out server . CRT-days 365
-gzip
启用 gzip/zlib 压缩(默认为真)
-help
打印用法
-密钥字符串
HTTPS 密钥:openssl genrsa -out default/tmp/simple http server-golang/src/bin/private(默认“private”)
-根字符串
根文件夹(默认“/tmp/simple http server-golang/src/bin”)
-TLS
启用 HTTPS
-用户名字符串
基本 auth 的用户名，默认:admin(默认“admin”)

run 子命令
用法:
。 /webserver-linux-amd64 运行

打包的二进制文件:**

**通过 HTTP 的网络服务器**

**$。8080 上的/webserver
共享/tmp/…
8080 上的共享/tmp/private…**

**HTTPS 的网络服务器**

**$ OpenSSL gen rsa-out server . key 2048
生成 RSA 私钥，2048 位长模数(2 个素数)
…………………………………………………………………++++
..++++++
e 是 65537(0x 010001)

$ OpenSSL req-new-x509-sha 256-key server . key-out server . CRT-days 365
您将被要求输入将被纳入
到您的证书请求中的信息。
你即将进入的是所谓的识别名或 DN。
有很多字段，但您可以保留一些空白
对于某些字段，如果您输入“.”，将会有一个默认值
，该字段将留空。
————
国家名称(2 个字母代码)【AU】:
州或省名称(全名)【Some-State】:
地点名称(例如，城市)】:
组织名称(例如，公司)【Internet wid gits Pty Ltd】:
组织单位名称(例如，部门)】:
常用名称(例如，服务器 FQDN 或您的姓名)[]:
电子邮件地址[]:

$。/web server we b-TLS-key server . key-cert server . CRT
共享/tmp/ on 8080 …
共享/tmp/private on 8080 …**

**使用私有目录和根目录的 Web 服务器**

*   **同一目录下的私人文件夹**

**$。/web server-Linux-amd64 web-private the private folder-用户名 no dauf-密码 nodauf
共享/tmp/ on 8080 …
共享/tmp/the private folder on 8080…**

*   **根目录和私人目录的不同路径**

**$。/web server-Linux-amd64 we b-private/tmp/private-root/home/no dauf-username no dauf-password no dauf
8080 上的共享/home/no dauf…
8080 上的共享/tmp/private…**

**嵌入式二进制(仅在 Windows 上)**

*   **列出嵌入的二进制文件:**

C:\Users\Nodauf >。\webserver.exe 运行
你必须指定一个二进制来运行
-args string
args 二进制
-binary string
Binary 来执行
-help
Print usage
-List
列出嵌入文件

打包的二进制:
Invoke-powershelltcp . PS1
mimikatz.exe
php-reverse-shell.php
plink.exe

*   **使用参数运行二进制:**

**C:\Users\Nodauf >。\ web server . exe run-binary mimikatz.exe-args " privilege::debug sekurlsa::logon passwords "
…。**

以这种方式运行二进制文件有助于绕过反病毒保护。有时发送到二进制文件的参数可能会被 AV 捕获，如果可能的话，使用二进制文件的交互式 CLI(如 mimikatz)或重新编译二进制文件来更改参数名称。

**特性**

*   HTTPS
*   目录列表
*   使用基本身份验证定义私人文件夹
*   上传多个文件
*   以加密 zip 格式下载文件(密码:已感染)
*   带 zip 的下载文件夹
*   嵌入文件
*   运行用 C#编写的嵌入式二进制文件(仅在 Windows 上可用)
*   从浏览器创建文件夹
*   执行嵌入式二进制文件的能力
*   搜索和替换功能(例如在反向外壳中填充 IP 地址)
*   生成一行程序来下载和执行文件

**待办事项**

*   JS/CSS 菜单在 powershell 中给出命令行，一些 lolbins，curl，wget 下载并执行
*   用于搜索和替换的配置文件(对默认配置有用)和其他功能
*   使用正则表达式进行搜索和替换
*   使用虚拟文件系统管理嵌入式文件

[**Download**](https://github.com/nodauf/Swego)