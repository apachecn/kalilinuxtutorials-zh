# 能够抓取单页应用程序的网络应用程序扫描器

> 原文：<https://kalilinuxtutorials.com/htcap-crawl-single-page-application/>

Htcap 是一个 web 应用程序扫描器，能够通过拦截 ajax 调用和 DOM 更改，以递归方式爬行单页面应用程序(SPA)。

Htcap 不仅仅是另一个漏洞扫描器，因为它专注于爬行过程，旨在检测和拦截 ajax/fetch 调用、websockets、jsonp ecc。

它使用自己的 fuzzers 加上一组外部工具来发现漏洞，并且它被设计成一个用于现代 web 应用程序的手动和自动渗透测试的工具。

它还有一个小而强大的框架，可以用不到 60 行 python 快速开发定制的 fuzzers。

fuzzers 可以处理 GET/POST 数据、XML 和 JSON 有效载荷，并在 POST 和 GET 之间切换。当然，fuzzers 在多线程环境中并行运行。

这是第一个使用 headless chrome 代替 phantomjs 的版本。

Htcap 的 Javascript 爬行引擎已经重写，以利用 ecmascript 的新 async/await 特性，并已转换为 Puppetteer 之上的 nodjes 模块。

**也可阅读:**[Hatch——暴力破解工具，用于暴力破解大多数网站](https://kalilinuxtutorials.com/hatch-brute-force-tool/)

#### **要求**

*   Python 2.7
*   Nodejs 和 npm
*   Sqlmap(用于 sqlmap 扫描仪模块)
*   Arachni(用于 arachni 扫描仪模块)

### Htcap 下载并运行

git 克隆 https://github . com/fcavalani/htcap . git
htcap $ htcap/htcap . py

#### **执照**

这个程序是自由软件；您可以根据自由软件基金会发布的 [GNU 通用公共许可证](https://www.gnu.org/licenses/gpl-2.0.html)的条款重新发布和/或修改它；许可证的第 2 版，或(由您选择)任何更高版本。

[**Download**](https://github.com/fcavallarin/htcap)