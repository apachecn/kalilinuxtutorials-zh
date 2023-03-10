# Quarantyne 现代网络防火墙

> 原文：<https://kalilinuxtutorials.com/quarantyne-modern-web-firewall/>

[![Quarantyne · Modern Web Firewall](img/86414197745ef3d0f550dd6fc19fa81c.png "Quarantyne · Modern Web Firewall")](https://1.bp.blogspot.com/-1I_7GwzDVKU/XQg7CluUwaI/AAAAAAAAA4Q/rDGDGu5MojkAAmBf0TbJ2q9kxnxJzPqYgCLcBGAs/s1600/Modern%2BWeb%2BFirewall.png%20)

Quarantyne 是一个反向代理，实时保护 web 应用和 API 免受欺诈行为、误用、僵尸程序和网络攻击。

**要求**

*   Java 8

**演讲**

这是一个用 java 写的反向代理。它保护 web 应用程序或 API，防止欺诈行为、误用、僵尸程序和网络攻击。它不能阻止所有这些，但它肯定会使执行起来更加困难和昂贵。

它类似于防火墙，但更智能，因为它不只是因为用户代理不在白名单中而阻止流量。它还执行深度请求检查，以检测所使用的密码之前是否被泄露过，或者电子邮件是否是一次性的，只需最少的配置，无需更改您的应用程序。我们的 [coverage](https://github.com/quarantyne/quarantyne#coverage) 部分精确地列出了它可以识别的内容。

**亦读-[Salsa 工具:ShellReverse TCP/UDP/ICMP/DNS/SSL/bind TCP&AV Bypass，AMSI 打补丁](https://kalilinuxtutorials.com/salsa-tools-shellreverse/)**

**特色**

**常见 HTTP 威胁和误用的广泛覆盖**

参见 [coverage](https://github.com/quarantyne/quarantyne#coverage) 了解它可以识别和阻止的威胁和滥用的完整列表。

**深度流量分析**

它对进入您的应用程序的 web 流量进行深度检查，以验证正在发送的数据没有被破坏或成为垃圾。

**通用集成**

它将额外的 HTTP 头添加到代理服务的请求中。例如，来自 AWS 的 HTTP 请求将带有以下标头:

*   `**X-Quarantyne-Labels: PCX**`
*   `**X-Quarantyne-RequestId: 08a0e31a-f1a5-4660-9316-0fdf5d2a959d**`

**主动保护**

它可以配置为阻止恶意请求到达您的服务器，避免浪费计算/数据库/缓存资源、指标偏差、垃圾数据…请参见(被动与主动)[#passivevsactive]。

**指标&健康报告**

它绑定到一个内部的`adminPort`，其中报告了指标(延迟、成功率……)以及代理的健康状况。

**隐私友好/ GDPR 合规**

是离线软件。它运行在您的私有网络中，不会通过互联网与任何人共享有关您的流量、业务或用户的数据。

**Ops 友谊赛**

具有 0 个依赖项的单个 jar。指标在`**[proxyHost]:[adminPort]/metrics**`可用。服务健康可在`**[proxyHost]:[adminPort]/health**`获得

**覆盖范围**

它能够检测以下威胁和误用。

| 标签 | 定义 | 行为 | 执行 |
| --- | --- | --- | --- |
| **发光二极管** | 大型主体数据 | 用正文大于 1MB 的 POST/PUT 请求重载目标的表单处理器 | 是 |
| **阶段** | 快速浏览 | 请求速率比常规的人工浏览更快 | 是 |
| **CPW** | 泄露的密码 | 使用的密码是从以前的数据泄露中得知的。可能的帐户接管 | 是 |
| **DMX** | 一次性电子邮件 | 使用的电子邮件是一次性电子邮件服务 | 是 |
| **IPR** | IP 地址轮换 | 同一个访问者正在轮换其 IP 地址 | 不 |
| **SHD** | 可疑的请求标头 | 异常的 HTTP 请求标头 | 是 |
| **SUA** | 可疑用户代理 | 不是来自常规 web 浏览器的用户代理 | 是 |
| **PCX** 的缩写形式 | 公共云执行 | IP 地址属于 AWS 或 GCP 等公共云服务 | 不 |
| **IPD** | IP/国家差异 | 从访问者 IP 推断的国家与提交的请求中的国家字段不同 | 不 |
| **SGE** | 可疑地理位置 | 该请求通常不是从该地理位置接收的。可能的帐户接管。 | 不 |

**被动 vs 主动**

**被动模式**

它让您决定如何处理它标记的请求。Quarantyne 的默认配置是**而不是**阻止受污染的流量。该流量将到达您的服务器，并通过 HTTP 报头进行标记。

被动模式是熟悉它并了解你的网络流量内部情况的推荐方式。在您的应用中，记录或绘制传入的 Quarantyne 标签，您可能会对您的发现感到惊讶(或不惊讶)!

**主动模式**

在主动模式下，Quarantyne 会阻止受污染的流量到达您的应用程序。只有明确配置 Quarantyne，才会发生阻塞。[配置](https://github.com/quarantyne/quarantyne#configuration)部分解释了如何启用流量阻塞。

**配置**

使用了两个互补的配置系统:命令行参数和外部(本地或远程)JSON 配置文件。

**命令行参数**

运行以下命令以显示帮助和可用的参数

**$ java -jar quarantyne -h
用法:[选项]
选项:
–admin
内部 ip:访问管理、UI 和指标的端口。可选
–配置文件
Quarantyne JSON 配置文件的可选 URL 或本地路径
–出口
Quarantyne 转发带注释的 web 流量的 HTTP 目的地。
默认:http://httpbin.org
–帮助，-帮助，–h，-h
显示关于可用配置参数的帮助
默认:假
–入口
ip:入站 web 流量的端口。
默认值:0.0.0.0:8080**

`**--config-file**`是一个可选的 JSON 配置文件，它告诉 Quarantyne 对服务的请求是如何构造的。它支持深度流量分析并增加覆盖范围。

**流量配置 JSON 文件**

流量配置文件是可选的，可以是绝对本地路径，也可以是 JSON 文件的[远程 HTTP(S) URL](https://s3-us-west-2.amazonaws.com/releases.quarantyne.com/quarantyne.json) ，其中包含一个具有以下结构的 JSON 对象。描述 HTTP 请求的结构有助于 Quarantyne 对密码、电子邮件或国家/地区等关键数据进行深度检查。

**{
"登录 _ 动作":{
"路径": "/任何东西"，
"标识符 _ 参数": "电子邮件"，
"秘密 _ 参数":"密码"
}，
"注册 _ 动作":{
"路径":"/任何东西"，
"标识符 _ 参数":"电子邮件"，
"秘密 _ 参数":"密码"
}，
"电子邮件 _ 参数 _ 密钥"::"**

Quarantyne 能够解析通过`POST` / `PUT`、带有`application/json`或`application/x-www-form-urlencoded`的`Content-Type`提交的有效载荷。

根属性是可选的。

| 财产 | 定义 | 笔记 |
| --- | --- | --- |
| `*_action` | 一个`POST` / `PUT`数据有效载荷 | `login_action`描述登录时发送的数据结构。`register_action`定义注册/创建账户时发送的数据结构。 |
| `*_action.path` | 提交数据的路径 | 必须从`/`开始 |
| `*_action.identifier_param` | 发送用户标识符的表单/JSON 键名 |  |
| `*_action.secret_param` | 发送用户密码的表单/JSON 密钥 |  |
| `email_param_keys` | 发送电子邮件地址的表单/JSON 密钥 |  |
| `country_iso_code_param_keys` | 发送国家 iso 代码的表单/JSON 密钥 |  |
| `blocked_request_page` | 阻塞请求时返回的 HTTP 响应 | 当这看起来像一个合法的页面/错误时，最好不要泄露攻击。如果能注入假数据就更好了🙂 |
| `blocked_classes` | 要阻止的攻击类的数组。 | `[]`相当于被动模式。阻止 Quarantyne 可以检测到的每一类攻击。见[报道](https://github.com/quarantyne/quarantyne#coverage) |

**快速奔跑**

**主持演示**

可在[https://demo.quarantyne.com/](https://demo.quarantyne.com/)买到。在这种情况下，Quarantyne 以被动方式面对 httpbin.org。发送的威胁和滥用将通过 HTTP 头进行标记，因此查询 https://demo.quarantyne.com/headers 或 https://demo.quarantyne.com/anything 的[是了解发生了什么的良好开端。提示:从简单开始，从卷曲开始。](https://demo.quarantyne.com/headers)

**跑罐子**

Quarantyne 作为一个独立的可执行 jar 提供。下载一个版本并运行:

**$ java -jar quarantyne.jar**

**从源代码构建**

克隆此 repo 或，并运行以下命令

**$。/gradlew run**

您应该看到以下内容:

*   **" 2018-11-28t 22:25:17.152-0800 "[main]INFO com . quarantyne . proxy . main–0 . 0 . 0:8080<= quarantyne =>http://httpbin.org:80**
*   **" 2018-11-28t 22:25:17.223-0800 "[main]INFO com . quarantyne . proxy . main–使用–help 查看可用选项**
*   **" 2018-11-28t 22:25:17.234-0800 "[main]DEBUG com . quarantyne . proxy . main-= =>事件循环大小为 8**
*   **" 2018-11-28t 22:25:17.234-0800 "[main]DEBUG com . quarantyne . proxy . main-= =>检测到 4 个 CPU 核心**
*   **" 2018-11-28t 22:25:17.496-0800 "[main]INFO com . quarantyne . config . configretrieveroptionssupplier–远程配置文件位于 https://S3-us-west-2 . amazonaws . com/releases . quarantyne . com/quarantyne . test . JSON**

你都准备好了！默认情况下，Quarantyne 从 127.0.0.1:8080 开始，代理流量到[http://httpbin.org](http://httpbin.org/)。

通过各种方式向[http://127 . 0 . 0 . 1:8080/headers](http://127.0.0.1:8080/headers)发送几个请求。如果检测到欺诈行为，您应该会在应用程序接收的请求中看到`X-Quarantyne-Label` HTTP 报头。提示:用 curl 试试。

[**Download**](https://github.com/quarantyne/quarantyne)