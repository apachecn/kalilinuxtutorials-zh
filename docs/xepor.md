# Xepor:面向逆向工程师和安全研究人员的 Web 路由框架

> 原文：<https://kalilinuxtutorials.com/xepor/>

[![](img/9b3111717e6ef45924f4897ae833b634.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj6SVXDv2VB_BMFZ4RDOeTVtmpQgLgh1xUsTSnVIUCY09Yhpgq8l11DXeRk_rHXrpbjf5b7svrp8oJSbDfFom5UK3tNzXrIiPAeXQQWe1zVYwnjwmEHSYiaLWZ5XeLXPqaAWwFp0yEYQTDJjQDXQfudFiNQT0QGhBiNuwWawVmOAkKETU2p_VO77-Gt/s728/h41%20(1).png)

Xepor (读作 */ˈzɛfə/* ，zephyr)，一个面向逆向工程师和安全研究人员的网络路由框架。它为黑客提供了一个类似 Flask 的 API，以一种人类友好的编码方式拦截和修改 HTTP 请求和/或 HTTP 响应。

该项目旨在与 mitmproxy 一起使用。用户用`**xepor**`编写脚本，用`**mitmproxy -s your-script.py**`运行 mitmproxy 内的脚本*。*

如果您想从概念验证阶段进入生产阶段，从演示阶段(例如 http-reply-from-proxy.py、http-trailers.py、http-stream-modify.py)进入可以用 WiFi 菠萝解决问题的阶段，Xepor 就是您的理想之选！

## 特性

*   一切用`**@api.route()**`编码，就像 Flask 一样！用*的一个*剧本写所有东西，不再用`i**f..else**`了。
*   在一个`**InterceptedAPI**`实例中处理多个 URL 路由，甚至多个主机。
*   对于每条路由，您可以选择在连接到服务器之前修改请求*(甚至返回一个没有连接到上游的假响应)，或者在*转发给用户之前修改响应*。*
*   黑名单模式或白名单模式。仅允许脚本中定义的 URL 端点连接到上游，使用 HTTP 404 阻止其他所有内容(在特定域中)。适用于透明代理。
*   人类可读的 URL 路径定义和由 parse 支持的匹配
*   主机重新映射。定义规则，从您的假冒主机重定向到真正的上游。支持正则表达式匹配。**最适合 SSL 剥离和服务器端许可破解**！
*   加上所有来自 mitmproxy 的最好的！**完全支持所有**操作模式(**`mitmproxy`/`mitmweb`+`regular`/`transparent`/`socks5`/`reverse:SPEC`/`upstream:SPEC`**)。

## 使用案例

*   邪恶的美联社和网络钓鱼通过 MITM。
*   通过 iptables +透明代理嗅探来自特定设备的流量，使用 xepor 动态修改有效负载。
*   破解基于云的软件许可。请参见 examples/krisp/作为示例。
*   用 **~100 行代码**写复杂的网络爬虫。参见 examples/polyv_scrapper/作为示例。
*   …以及更多。

本项目不提供 SSL 剥离。

# 安装

**pip 安装 xepor**

# 快速启动

以 examples/httpbin 中的脚本为例。

在这个例子中，我们在`**127.0.0.1**`上设置了 mitmproxy 服务器。您可以将其更改为您机器上的任何 IP，或者更改为您的 VPS 的 IP。在反向、上游和透明模式下运行的 mitmproxy 服务器需要设置`**--set connection_strategy=lazy**`选项，以便 Xepor 可以正常工作。我建议这个选项总是打开，以获得最佳稳定性。

将您的浏览器 HTTP 代理设置为`**http://127.0.0.1:8080**`，访问 web 界面 http://127.0.0.1:8081/。

从 http://httpbin.org/#/HTTP_Methods/get_get 发送一个 GET 请求，然后你可以看到 Xepor 在 mitmweb 界面、浏览器 devtools 或 Wireshark 中所做的修改。

`**httpbin.py**`做两件事。

*   当用户访问 http://httpbin.org/get,时，在 HTTP 请求中注入一个查询字符串参数`**payload=evil_param**`。
*   当用户访问 http://httpbin.org/basic-auth/xx/xx/时(我们只是假装不知道密码)，从 HTTP 请求中嗅探`**Authorization**`报头，并将密码打印给攻击者。

就像 mitmproxy 经常做的那样，但是用 xepor 方式编写代码。

# https://github.com/xepor/xepor-examples/tree/main/httpbin/httpbin.py

**from mitm proxy . http import http flow
from xe por import intercepted API，route type
HOST _ http bin = " http bin . org "
API = intercepted API(HOST _ http bin)
@ API . route("/get ")
def change _ your _ request(flow:http flow):
" "
修改 URL 查询参数。
测试地点:
http://httpbin.org/#/HTTP_Methods/get_get
" " "
flow . request . query[" payload "]= " evil _ param "
@ API . route("/basic-auth/{ usr }/{ pwd } "，rtype=RouteType。RESPONSE)
def capture _ auth(flow:http flow，usr=None，pwd=None):
"""
嗅探密码。
测试于:
http://httpbin.org/#/Auth/get_basic_auth__user___passwd_
" " "
print(
f " auth @ { usr }+{ pwd }:"，
f " Captured { ' successful ' if flow . response . status _ code<300 else ' unsuccessed ' } log in:"，
flow . request . headers . get(" Authorization "，"")，
)
addons = [api]**

[**Download**](https://github.com/xepor/xepor)