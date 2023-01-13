# Cdb:自动执行常见的 Chrome 调试协议任务，帮助调试 Web 应用程序

> 原文：<https://kalilinuxtutorials.com/cdb/>

[![](img/004befb3eaf19091d62baca581782961.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjwmF0c0s2nEGe8qJJyfCSoluuMu0Qgeh_OOJeqvx3Zz6oooh8FLVtCUNw-8t4ZdzJ18qK3RD3oE3ZC7OFxHYjXpzguiIHnLfQ2Jid7FdeoPE4UjSorGwZZgT6qbufP--qS1fs1nU91xDiO-3azIYgA36p4K1TPxEgA8St1RMPaQG-OquavTSyqG29T/s728/1_b_KiuAIq03Bp7Hq58sASPw%20(1).png)

CDB 是一个 Chrome 调试协议工具。该工具的主要目标是自动化常见任务，以帮助从命令行调试 web 应用程序，并主动监控和拦截 HTTP 请求和响应。这在渗透测试和其他类型的安全评估和调查中特别有用。

## 快速启动

该工具旨在作为 Pown.js 的一部分使用，但也可以作为一个独立的工具单独调用。

照常首先安装 Pown:

**$ npm install -g pown@latest**

直接从 Pown 调用:

**$ pown cdb**

### 图书馆使用

从项目的根目录本地安装此模块:

**$ NPM install @ pown/CDB–保存**

完成后，调用 pown cli:

**$ POWN_ROOT=。。/node_modules/。bin/pown-cli cdb**

## 使用

**pown cdb
chrome 调试协议工具
命令:
pown cdb launch 启动 Chrome、firefox、opera、edge 等服务器应用【别名:start】
pown CDB 导航到指定 url【别名:Go to、Go】
pown CDB 网络 Chrome 调试协议网络监视器【别名:net、sniff、proxy、mon、Monitor】
pown CDB cookie 转储当前页面 cookie【别名:cookie】
pown CDB 截图当前页面【别名:capture、shot**

`**pown cdb navigate**`

**pown cdb 导航
转到指定 url
选项:
–版本显示版本号【布尔】
–帮助显示帮助【布尔】
–主机，-H 远程调试主机[字符串][默认:“localhost”]
–端口，-p 远程调试端口[数字][默认:9222]
–安全，-s HTTPS/WSS 前端[布尔][默认:假]**

`**pown cdb network**`

**pown cdb 网络
Chrome 调试协议网络监视器
选项:
–版本显示版本号【布尔】
–帮助显示帮助【布尔】
–主机，-H 远程调试主机[字符串][默认:“localhost”]
–端口，-p 远程调试端口[数字][默认:9222]
–安全，-s HTTPS/WSS 前端[布尔][默认:假]
–输出，-o 输出目录/文件[数组][默认:[]]
-有福了**

[**Download**](https://github.com/pownjs/cdb)