# 自动外壳查找

> 原文：<https://kalilinuxtutorials.com/af-shellhunter/>

[![](img/0bddc36630ae72bb256c843fa706dced.png)](https://blogger.googleusercontent.com/img/a/AVvXsEjkPADJ3igffTz4RSFxOc-G_p61qtwrKCkm-5Vtnc_0aWDeJNeIUMlWw_m6b2q3_0E6m8_BB2L8m1ZnMAN68cOnkHkbg6VEfSw3RQ57yVjK226krXSm4AtpuNunfvwsmX5VhGO2LGsSns22GOqslnaM4IfLJUP_rA0dnJd9uh_DJag4UP0TGbNiSaKa=s728)

AF-ShellHunter 这是一个在 AF 团队中自动搜索 WebShell 的脚本

**如何**

pip 3 install-r requirements . txt
python 3 shell hunter . py–help

**基本用法**

您可以在两种模式下运行 shellhunter

*   **–url-u**扫描单个 URL 时
*   **–file-f**同时扫描多个网址

示例使用 burpsuite 代理搜索 webshell，隐藏大小在 100 到 1000 个字符之间的字符串“404”

**┌──(blueudp㉿xxxxxxxx)-[~/af-shellhunter】
└─$ python 3 shell hunter . py-u https://xxxxxxxxxx-hs " 404 "-p burp–大于 100–小于 1000
运行 af-team shell hunt 1 . 1 . 0
URL:https://xxxxxxxxxxx x
仅显示:200，302
线程:20
不显示与:404
代理一致:burp
大于:100**

**多个站点的文件配置**

网络钓鱼 _ 列表

# **如何？**
# s**et country block with[country]，please read user _ files/config . txt
# ' Show-response-code " option 1 " " option 2 "->显示带有这些状态代码的响应，as -sc
#'show-string' - >显示与该字符串匹配，as -ss
#'show-regex' - >显示与 regex 匹配，as-Sr
#使用' not '表示不显示上述选项中的 X，as -ss302，200 状态代码，不显示大小在 100 到 1000 个字符之间的结果(w/' página en mantenimiento)
[burp]
https://Banco . phishing->显示响应代码“302”“200”，不显示字符串“página en mantenimiento”，大于 100，小于 1000
【no proxy】
Banco . es->#**

**设置您的代理和自定义标题**

配置文件

**[HEADERS] #请求自定义标题，添加' OPTION: VALUE'
用户代理？Mozilla/5.0(Linux；安卓 8 . 0 . 0；SM-G960F Build/R16NW)apple WebKit/537.36(KHTML，像壁虎一样)Chrome/62 . 0 . 3202 . 84 Mobile Safari/537.36
Referer？bit.ly/THIS_is_PHISHING #绕过引用者保护
【代理】
打嗝？https://127.0.0.1:8080，http://127.0.0.1:8080**

**其他特征**

*   按正则表达式筛选
*   按字符串过滤
*   按 HTTP 状态代码筛选
*   按长度过滤
*   自定义标题
*   URL 文件的自定义代理或代理块
*   多线程(自定义工人号)

[**Download**](https://github.com/blueudp/AF-ShellHunter)