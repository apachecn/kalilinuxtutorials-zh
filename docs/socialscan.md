# social scan–在在线平台上以 100%的准确率检查电子邮件地址和用户名的可用性

> 原文：<https://kalilinuxtutorials.com/socialscan/>

[![Socialscan – Check Email Address And Username Availability On Online Platforms With 100% Accuracy](img/eaf32f09318eec9c4c05e54779fbcf29.png "Socialscan – Check Email Address And Username Availability On Online Platforms With 100% Accuracy")](https://1.bp.blogspot.com/-EsqypStlVmI/XjALzSpudiI/AAAAAAAAEpk/_9noa2HQJOk6yeHDxuwy-alADOc0sc3BACLcBGAsYHQ/s1600/SoialScan%25281%2529.png)

**Socialscan** 为**提供准确的**和**快速的**检查在线平台上的电子邮件地址和用户名使用情况。给定一个电子邮件地址或用户名，socialscan 会返回它在在线平台上是否可用、被占用或无效。

将 socialscan 与类似工具区分开来的功能(例如 knowem.com、Namechk 和夏洛克):

*   **100%准确率** : socialscan 的查询方式消除了类似工具中经常出现的误报和漏报，保证了结果始终准确。
*   **速度** : socialscan 使用 asyncio 和 aiohttp 同时执行所有查询，即使是涉及数百个用户名和电子邮件地址的批量查询也能提供快速搜索。在一台具有一般规格和网速的测试计算机上，100 个查询在大约 4 秒内被执行。
*   **库/ CLI** : socialscan 可以通过 CLI 执行，也可以作为 Python 库导入，与现有代码一起使用。
*   **电子邮件支持** : socialscan 支持对电子邮件地址和用户名的查询。

**也读作-[赫谢尔:多平台反向外壳生成器](https://kalilinuxtutorials.com/hershell-multiplatform-reverse-shell-generator/)**

目前支持以下平台:

|  | 用户名 | 电子邮件 |
| --- | --- | --- |
| 照片墙 | **支持的** | **支持的** |
| 推特 | **支持的** | **支持的** |
| 开源代码库 | **支持的** | **支持的** |
| Tumblr | **支持的** | **支持的** |
| 上次调频 | **支持的** | **支持的** |
| Snapchat | **支持的** | **否** t **支持** |
| GitLab | **支持的** | **否** t **支持** |
| Reddit | **支持的** | **否** t **支持** |
| 美国 Yahoo 公司(提供互联网的信息检索服务) | **支持的** | **否** t **支持** |
| 拼趣 | **否** t **支持** | **支持的** |
| Spotify | **否** t **支持** | **支持的** |

![](img/2337e0bbb6476b66b2851db63020a960.png)![](img/967d7cfdbb88520fcd275833ae064dc4.png)

**背景**

其他类似的工具通过请求有问题的用户名的配置文件页面来检查用户名的可用性，并根据诸如 HTTP 状态代码或所请求页面上的错误文本之类的信息来确定用户名是否已被占用。

这是一种幼稚的方法，在以下情况下会失败:

*   保留关键字:大多数平台都有一组不允许在用户名中使用的关键字
    (一个简单的测试:尝试检查保留字，如“admin”、“home”或“root”，并查看其他服务是否将它们标记为可用)

*   删除/禁止的帐户:删除/禁止的帐户用户名往往是不可用的，即使个人资料页面可能不存在

因此，这些工具往往会出现误报和漏报。

这种检查方法还依赖于具有基于网络的个人资料页面的平台，并且不能扩展到电子邮件地址。

Socialscan 旨在通过直接查询平台的注册服务器，检索适当的 CSRF 令牌、报头和 cookies 来填补这些空白。

**安装**

**皮普**

> **pip 安装社会扫描**

**从源安装**

**> git 克隆 https://github . com/iojw/socialscan . git
>CD
>pip 安装。**

**用途**

```
usage: socialscan [list of usernames/email addresses to check]

optional arguments:
  -h, --help            show this help message and exit
  --platforms [platform [platform ...]], -p [platform [platform ...]]
                        list of platforms to query (default: all platforms)
  --view-by {platform,query}
                        view results sorted by platform or by query (default:
                        query)
  --available-only, -a  only print usernames/email addresses that are
                        available and not in use
  --cache-tokens, -c    cache tokens for platforms requiring more than one
                        HTTP request (Snapchat, GitHub, Instagram. Lastfm &
                        Tumblr), reducing total number of requests sent
  --input input.txt, -i input.txt
                        file containg list of queries to execute
  --proxy-list proxy_list.txt
                        file containing list of HTTP proxy servers to execute
                        queries with
  --verbose, -v         show query responses as they are received
  --version             show program's version number and exit 
```

**作为图书馆**

Socialscan 也可以导入到现有代码中，用作库。

v1.0.0 引入了异步方法`**execute_queries**`和相应的同步包装器`**sync_execute_queries**`，该包装器接受查询列表和可选的平台和代理列表，并发执行所有查询。然后，该方法以相同的顺序返回结果列表。

**从 socialscan.util 导入平台，sync_execute_queries

查询= ["用户名 1 "，" email2@gmail.com "，" mail42@me.com"]
平台=[平台。GITHUB，平台。LASTFM]
results = sync _ execute _ queries(查询，平台)

for result in results:
print(f " { result . query } on { result . platform }:{ result . message }(成功:{result.success}，有效:{result.valid}，可用:{ result . Available })"**

**输出**:

**GitHub 上的 username1:用户名已被占用(成功:真，有效:真，可用:假)
last FM 上的 username1:抱歉，此用户名不可用。(Success: True，Valid: True，Available:False)【GitHub 上的 email2@gmail.com:Available(Success:True，Valid: True，Available:True)
last FM 上的 email2@gmail.com:抱歉，那个邮箱已经注册了另一个账号。(成功:真，有效:真，可用:假)【GitHub 上的 mail42@me.com:可用(成功:真，有效:真，可用:真)
Lastfm 上的 mail42@me.com:好看！(成功:真，有效:真，可用:真)**

**文本文件输入**

对于使用**–输入选项**的批量查询，在。txt 文件:

**用户名 1
email2@mail.com
用户名 3**

[**Download**](https://github.com/iojw/socialscan)