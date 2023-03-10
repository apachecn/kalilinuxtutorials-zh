# Orbitaldump:一个用 Python 编写的简单多线程分布式 SSH 强力工具

> 原文：<https://kalilinuxtutorials.com/orbitaldump/>

[![Orbitaldump : A Simple Multi-Threaded Distributed SSH Brute-Forcing Tool Written In Python](img/5e69efef5a09b43bc3ec92e6b6f81c35.png "Orbitaldump : A Simple Multi-Threaded Distributed SSH Brute-Forcing Tool Written In Python")](https://1.bp.blogspot.com/-Gaob94MYSpI/YPbDHjK35_I/AAAAAAAAKJM/JKJhQaRClyg4pjU5gkXA22ceKDHshrT_gCLcBGAsYHQ/s571/images.png)

**Orbitaldump** 是一个简单的多线程分布式 SSH 强力工具，用 Python 编写。

当在没有`**--proxies**`开关的情况下执行脚本时，它的行为就像任何其他多线程 SSH 强制脚本一样。当添加了`**--proxies**`开关时，脚本从 ProxyScrape 中提取一个 SOCKS4 代理列表(通常是数千个),并通过 SOCKS4 代理发起所有暴力攻击，因此暴力攻击尝试不太可能受到目标主机的速率限制。

**安装**

可以通过 pip 安装 OrbitalDump。

用户轨道转储
轨道转储

或者，您可以克隆这个存储库并直接运行源代码。

**git 克隆 https://github.com/k4yt3x/orbitaldump.git
CD 轨道转储
python -m 轨道转储**

用途

下面显示了一个简单的用法。下面这个命令:

*   `**-t 10**`:启动 10 个强力线程
*   `**-u usernames.txt**`:从 usernames.txt 中读取用户名(每行一个用户名)
*   `**-p passwords.txt**`:从 passwords.txt 中读取密码(每行一个密码)
*   `**-h example.com**`:将强力目标设置为`example.com`
*   从 ProxyScrape 发起对代理的攻击

**python-m orbital dump-t 10-u usernames . txt-p passwords . txt-h example.com-代理**

**完整用法**

您可以通过使用`--help`开关执行 OrbitalDump 来获得完整的用法。以下部分可能已过期。

**用法:orbitaldump[–help][-t THREADS][-u USERNAME][-p PASSWORD]-h HOSTNAME[–PORT PORT][–time out time out][–proxy]
可选参数:
–help 显示此帮助消息并退出
-t THREADS，–THREADS
要使用的线程数(默认值:5)
-u USERNAME，–USERNAME 用户名
用户名文件路径(默认值:无)
-p PASSWORD，–PASSWORD
密码文件路径(默认值:无)**

[**Download**](https://github.com/k4yt3x/orbitaldump#installation)