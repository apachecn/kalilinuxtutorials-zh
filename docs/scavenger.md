# 清道夫:爬虫(Bot)在不同的粘贴站点上搜索凭证泄漏

> 原文：<https://kalilinuxtutorials.com/scavenger/>

[![Scavenger : Crawler (Bot) Searching For Credential Leaks On Different Paste Sites](img/fa11c387219b66c952fdffb85461a073.png "Scavenger : Crawler (Bot) Searching For Credential Leaks On Different Paste Sites")](https://1.bp.blogspot.com/-GP05JhgBC38/XOWygRXRoVI/AAAAAAAAAbA/lfwsr4MhZcg1waqNMCZblQIptQSigVNBgCLcBGAs/s1600/Scavenger%25281%2529.png)

清道夫爬虫(Bot)搜索不同粘贴站点上的凭据泄漏。只是我的 OSINT 机器人在不同的粘贴网站上搜索敏感数据泄漏的代码。

**搜索词:**

*   资格证书
*   私有 RSA 密钥
*   WordPress 配置文件
*   MySQL 连接字符串
*   洋葱链接
*   链接到洋葱网络内部托管的文件(PDF，DOC，DOCX，XLS，XLSX)

请记住:

*   这个机器人不漂亮。我写得又快又脏，不关心代码约定或其他狗屎…我永远不会关心这些事情。
*   代码目前还不完整。这个在线存储库中缺少一些部分，如将凭据集成到数据库中。
*   如果你想使用这段代码，请随意。请记住，你必须定制的东西，让它在你的系统上运行。
*   我知道我有一些假阳性，我知道我错过了一些凭证。所以如果你认为这是废话…好吧。现在就离开。如果你有更好的检测方法，请告诉我！
*   再来一次:又快又脏！不要期待好的代码。

**也可阅读—[Secure tea 项目:旨在帮助保护未授权访问的 OWASP 应用](https://kalilinuxtutorials.com/securetea/)**

**重要**

该机器人可以在两种主要模式下运行:

*   apic 模式
*   刮擦模式(使用 TOR)

我强烈推荐使用 API 模式。这是从 Pastebin.com 刮浆糊的方法，这样做是公平的。你唯一需要的是一个 Pastebin.com 专业帐户，并在他们的网站上把你的公共 IP 列入白名单。

要在 API 模式下启动 bot，只需按以下方式运行程序:

**python run.py -0**

但是，这种方法并不总是可行的，因为您可能处于 NAT 模式，因此您没有专用的 IP 地址(在这里将您的 IP 地址列入白名单是不合理的)。这就是为什么我还实施了一种抓取模式，在这种模式下，快速 TOR 周期与合理的用户代理结合使用，以避免 IP 阻塞和 Cloudflare 验证码。

要以抓取模式启动 bot，请按以下方式运行它:

**python run.py -1**

重要注意事项:您需要在系统上安装 TOR 服务来监听端口 9050。此外，您需要在/etc/tor/torrc 文件中添加以下行。

**maxcircuitdirty 30**

这将 TOR 的最大周期时间设置为 30 秒。

**用法**

要了解如何使用该软件，您只需调用带有-h/–help 参数的 run.py 脚本。

**python run.py -h**

**输出:**

**用法:run . py[-h][-0][-1][-2][-PS]

针对本次粘贴爬虫不同模块的控制软件。

可选参数:
-h，–help 显示此帮助信息并退出
-0，–pastebinCOMapi 激活 Pastebin.com 模块(使用 API)
-1，–pastebinCOMtor 激活 Pastebin.com 模块(使用
TOR 的标准刮擦以避免 IP 阻塞)
-2，–pasteORG 激活 pasteORG 模块
-ps，–pStatistic 显示一个简单的统计数据。**

到目前为止，我只实现了 Pastebin.com 模块，我在 Paste.org 工作。我将添加更多的模块，并随着时间的推移更新这个脚本。

只需单独启动 Pastebin.com 模块(我实现的第一个模块)…

**python P_bot.py**

粘贴存储在数据/raw_pastes 中，直到它们超过 48000。当它们超过 48000 时，它们会被过滤、压缩并移动到存档文件夹中。所有包含凭证的粘贴都存储在带有密码的数据/文件中

请记住，目前只能检测到用户名:密码和其他简单组合。但是，有一个工具可以搜索包含凭据的代理日志。

您可以使用 getProxyLogs.py 文件搜索代理日志(包含用户名和密码组合的 URL)

**python getproxylogs . py data/raw _ pastes**

如果你想在原始数据中搜索特定的字符串，你可以使用 searchRaw.py(非常慢)。

**python search raw . py search string**

要查看机器人的统计数据，只需调用

**python status.py**

文件 findSensitiveData.py 搜索文件夹(带有粘贴内容)以查找敏感数据，如信用卡、RSA 密钥或 mysqli_connect 字符串。请记住，这个脚本使用 grep，因此对于大量的粘贴文件来说非常慢。如果你想分析大量的糊状物，我推荐 ELK-Stack。

**python findsensitive data . py data/raw _ pastes**

有两个脚本可以用来监控特定的 twitter 用户。这意味着他发布的每条推文都会被保存，每个包含的 URL 都会被下载。要启动跟踪者，只需执行包装器。

**python stall _ user _ wrapper . py**

**待办事项**

我发现了其他网站，比如 Pastebin，它们允许阅读最新的粘贴并抓取它们。我需要把它们集成到我的机器人里。如果你知道其他值得一看的网站，请告诉我。

**举例:
https://slexy.org/recent
http://pastebin . fr
http://pastebin.es/lists
http://pastebin.it/archive.php**

[**Download**](https://github.com/rndinfosecguy/Scavenger)