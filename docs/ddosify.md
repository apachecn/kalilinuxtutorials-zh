# Ddosify:高性能负载测试工具

> 原文：<https://kalilinuxtutorials.com/ddosify/>

[![](img/86bfabed8df0a8ddacc549d32a6a32be.png)](https://blogger.googleusercontent.com/img/a/AVvXsEhYXPvIryryDvcLQbIhuzhT_NBZBveWtJsmZftAPXXfdXMmIqkNlwgi3tTLC5YlC9pzKI6yFmzWAl4nvN-fldUwTOzP43EMO0gMVa2o2n5p-5V-ub31N99_lpVN6pHRdAZ99To2jdKs7oHgA7pngNCXS0use9nPEBEhHzj7OtP4wKjnYCuRIVJRwTPV=s728)

Ddosify 是一个高性能的负载测试工具

**特性**

*   与协议无关–目前支持 *HTTP、HTTPS、HTTP/2* 。其他协议正在制定中。

*   基于场景——在 JSON 文件中创建您的流程。没有一行代码！

*   不同的负载类型–测试您的系统在不同负载类型下的极限。

**安装**

`**ddosify**`可通过 Docker、Homebrew Tap 获得，也可从 macOS、Linux 和 Windows 的发布页面下载预编译的二进制文件。

**码头工人**

**docker run-it–RM ddosify/ddosify**

**家酿 Tap (macOS 和 Linux)**

**brew 安装 ddosify/tap/ddosify**

**apk，deb，rpm，Arch Linux 包**

*   对于 arm 架构，将`**ddosify_amd64**`更改为`**ddosify_arm64**`或`**ddosify_armv6**`。
*   需要超级用户权限。

**基于 red hat(Fedora、CentOS、RHEL 等。)
rpm-I https://github . com/ddosify/ddosify/releases/latest/download/ddosify _ amd64 . rpm
针对基于 Debian(Ubuntu、Linux Mint 等。)
wget https://github . com/ddosify/ddosify/releases/latest/download/ddosify _ amd64 . deb
dpkg-I ddosify _ amd64 . deb
For Alpine
wget https://github . com/ddosify/ddosify/releases/latest/download/ddosify _ amd64 . apk
apk add–allow-untrusted ddosify _ amd64 . apk
For Arch Lin**

**使用便利脚本(macOS 和 Linux)**

*   该脚本需要 root 或 sudo 权限才能将 ddosify 二进制文件移动到 **`/usr/local/bin`。**
*   该脚本试图检测您的操作系统(macOS 或 Linux)和体系结构(arm64、x86、amd64 ),以便从 releases 页面下载适当的二进制文件。
*   默认情况下，脚本会安装最新版本的`**ddosify**`。
*   如果有问题，请查看常见问题
*   必需的包:`**curl**`和`**sudo**`

**curl-sSfL https://raw.githubusercontent.com/ddosify/d**dosi fy/master/scripts/install . sh | sh

**从源代码安装(macOS、Linux、Windows)**

**去安装-v go.ddosify.com/ddosify@latest**

**轻松启动**

本节旨在向您展示如何使用 Ddosify，而无需深入了解它的细节。

*   **简单负载测试**

**ddosify -t target_site.com**

上面的命令运行一个负载测试，默认值是 10 秒钟 100 个请求。

**使用某些功能**

**ddosify-T target _ site . com-n 1000-d 20-P HTTPS-m PUT-T 7-P http://**proxy _ server . com:80

Ddosify 在 *20* 秒内通过代理*http://proxy _ server . com:80*向 *https://target_site.com* 发送总计 *1000* *PUT* 请求，每个请求的超时为 *7* 秒。

**基于场景的负载测试**

**ddosify-config config _ examples/config . JSON**

1.  Ddosify 首先使用基本认证凭证 *test_user:12345* 通过代理*HTTP://proxy _ host . com:proxy _ port*向*https://test _ site 1 . com/endpoint _ 1*发送 *HTTP/2 POST* 请求，超时 *3* 秒。一旦收到响应，HTTPS 获取请求将连同包含在*config _ examples/payload . txt*文件中的有效载荷一起发送到*https://test _ site 1 . com/endpoint _ 2*，超时 2 秒。该流程将在 *5* 秒内重复 *20* 次，响应将被写入 *stdout* 。

**详情**

您可以通过 CLI 选项或配置文件来配置负载测试。Config 文件支持比 CLI 更多的功能。例如，您不能使用 CLI 选项创建基于场景的负载测试。

**CLI 标志**

**ddosify [FLAG]**

| 旗 | 描述 | 类型 | 默认 | 必需的？ |
| --- | --- | --- | --- | --- |
| `**-t**` | 目标网站 URL。例如:https://ddosify.com | `**string**` | – | 是 |
| `**-n**` | 请求总数 | `**int**` | `**100**` | 不 |
| `**-d**` | 以秒为单位的测试持续时间。 | `**int**` | `**10**` | 不 |
| `**-p**` | 请求的协议。支持的协议有 *HTTP，HTTPS* 。HTTP/2 支持只能通过使用如上所述的配置文件来实现。将添加更多的协议。 | `**string**` | `**HTTPS**` | 不 |
| `**-m**` | 请求方法。HTTP 的可用方法有*获取、发布、上传、删除、更新、修补* | `**string**` | `**GET**` | 不 |
| `**-b**` | 网络数据包的有效负载。也就是 HTTP 的主体。 | `**string**` | – | 不 |
| `**-a**` | 基本身份验证。用法:`**-a username:password**` | `**string**` | – | 不 |
| `**-h**` | 请求的标头。您可以提供带有多个`-h`标志的多个标题。 | `**string**` | – | 不 |
| `**-T**` | 请求的超时时间(秒)。 | `**int**` | `**5**` | 不 |
| `**-P**` | 代理地址作为主机:端口。`**-P http://user:pass@proxy_host.com:port'**` | `**string**` | – | 不 |
| `**-o**` | 测试结果输出目标。将添加其他输出类型。 | `**string**` | `**stdout**` | 不 |
| `**-l**` | 负载测试的类型。Ddosify 支持 3 种负载类型。 | `**string**` | `**linear**` | 不 |
| `**-config**` | 负载测试的配置文件。 | `**string**` | – | 不 |
| `**-version**` | 打印版本、git 提交、构建日期(utc)、go 信息并退出 | – | – | 不 |

**负载类型**

**线性**

**ddosify-t target _ site . com-l linear**

结果:

![](img/ce9eb8f80d0f27dc8ac6a6368769762c.png)

**挥挥手**

**ddosify**–**t target _ site . com-l 挥挥手**

结果:

![](img/2d41e458402d5b9d4333fc3e9187e3c2.png)

**配置文件**

配置文件允许您使用 Ddosify 的所有功能。

配置文件可以使用的功能；

*   场景创建
*   自定义装载类型创建
*   来自文件的有效负载
*   额外的连接配置，如*保持活动状态*启用/禁用逻辑
*   HTTP2 支持

用法；

**ddosify -config**

config_examples/config.json 中有一个示例配置文件。每个参数的详细信息；

*   `**request_count**` *可选*这相当于`**-n**`旗。不同之处在于，如果您的场景中有多个步骤，则该值表示这些步骤的迭代次数。
*   `**load_type**` *可选*这相当于`**-l**`旗。
*   `**duration**` *可选*这相当于 **`-d`** 旗。
*   `**manual_load**` *可选*如果您正在寻找创建您自己的定制装载类型，您可以使用此功能。下面的示例说明 Ddosify 将按照提供的持续时间分别运行场景 5 次、10 次和 20 次。`**request_count**`和`**duration**`将由 Ddosify 根据`**manual_load**`配置自动填充。在这个例子中，`**request_count**`将是 35 秒，而`**duration**`将是 18 秒。此外，如果您同时提供了 **`manual_load`** 和`**load_type**`两者，则它们会被覆盖。因此，在使用 **`manual_load`时，不需要提供这 3 个参数。**

**“手动 _ 加载”:[
{“持续时间”:5，“计数”:5}、
{“持续时间”:6，“计数”:10}、
{“持续时间”:7，“计数”:20}、
]**

*   `**proxy**` *可选*这相当于`**-P**`旗。
*   `**output**` *可选*这相当于`**-o**`旗。
*   `**steps**` *强制*这个参数让你创建你的场景。Ddosify 分别运行提供的步骤。对于给定的示例文件，步骤 id: 2 将在收到步骤 id: 1 的响应后立即执行。执行顺序与配置文件中的步骤顺序相同。**一个步骤的每个参数的详细信息；**
    *   `**id**` *强制*每个步骤必须有一个唯一的整数 id。
    *   `**url**` *强制*这相当于`**-t**`旗。
    *   `**protocol**` *可选*这相当于`**-p**`旗。
    *   `**method**` *可选*这相当于`**-m**`旗。
    *   `**headers**` *可选*带关键字的表头列表:数值格式。
    *   `**payload**` *可选*这相当于`**-b**`旗。
    *   `**payload_file**` *可选*如果你需要长的有效载荷，我们建议用这个参数代替`**payload**`。
    *   `**auth**` *可选*基本认证。

**“auth”:{
“username”:“test _ user”，
“password”:“12345”
}**

`**others**`   *optional*

该参数接受动态的*键:值*对，以配置正在使用的协议的连接细节。

**" others ":{
" keep-alive ":true，//默认 false
" disable-compression ":false，//默认 true
"h2": true，//启用 HTTP/2。默认为假。
“禁用-重定向”:真//默认假
}**

**常见问题**

**macOS 安全问题**

**“ddosify”打不开，因为 Apple 无法检查它是否有恶意软件。**

*   打开`**/usr/local/bin**`
*   右击`**ddosify**`并选择打开
*   选择打开
*   关闭打开的终端

[**Download**](https://github.com/ddosify/ddosify)