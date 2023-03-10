# BruteLoops:协议不可知的在线密码猜测 API

> 原文：<https://kalilinuxtutorials.com/bruteloops/>

[![](img/133eaf302593c1b53d53c2103ca7b860.png)](https://blogger.googleusercontent.com/img/a/AVvXsEhu0jiAyEAJ-Vqx78OTIxrv1wuGxDNPp7YQNEs-uWTQfF3Y4SVPB8tqpp5Fxzp5Vf6QB4hdspae5nmSSu372wvGZmJ90Ga8UQZievjGevXebOyu0Lik5PogcCMQOxhoc4VQ5SaxaKoM8T2F6k03z1fvJEpYdEXer2zyJJ7cqgAHyxT2sL1NnQxkwrkZ=s755)

是一个非常简单的库，为针对认证接口的高效密码暴力攻击提供了基础逻辑。

有关更多信息，请参见各个 Wiki 部分。

该库包含一个“模块化”示例，演示如何使用这个包。它的功能齐全，并提供多个暴力模块。以下是其功能的示例:

**HTTP . Accel lion _ FTP Accel lion FTP 接口登录模块
HTTP . basic _ digest Generic HTTP basic digest auth
HTTP . basic _ NTLM Generic HTTP basic NTLM 认证
HTTP . Global _ Protect
Global Protect web 接口
http.mattermost Mattermost 登录 web 接口
http.netwrix Netwrix web 登录
HTTP . Okta Okta JSON API
HTTP . OWA 2010 OWA 2010**

**主要特征**

*   **协议不可知**–如果可以用 Python 编写回调函数，就可以用暴力工具攻击它
*   **SQLite 支持**–所有用户名、密码和凭证都保存在 SQLite 数据库中。
    *   一个创建和管理输入数据库的配套工具(`**dbmanager.py**`)伴随着 BruteLoops
*   **在一个工具中进行喷射和填充攻击**–BruteLoops 在相同的攻击逻辑和数据库中支持喷射和填充攻击，这意味着您可以配置单个数据库并运行攻击，而无需进行大量的重新配置和混淆。
*   **Guess scheduling**–SQLite 数据库中的每个用户名都配置了一个时间戳，该时间戳会在每次身份验证事件后更新。这意味着，我们可以通过精确安排每个身份认证事件，显著降低锁定帐户的可能性。
*   **避免锁定事件的精细可配置性**–微软的锁定策略可以使用 BruteLoop 的参数进行一对一匹配:
    *   `**auth_threshold**` =锁定阈值
    *   `**max_auth_jitter**` =锁定观察窗口
    *   在 BruteLoops 的 SQLite 数据库中跟踪与每个认证事件相关的时间戳。每个用户名都会收到一个不同的时间戳，以确保身份验证事件得到高度控制。
*   **攻击恢复**–停止和恢复攻击是可能的，不用担心在攻击中失去自己的位置或锁定帐户。
*   **多重处理**–使用多重处理加速攻击！通过配置“并行猜测计数”，您可以有效地告诉 BruteLoops 有多少用户名可以并行猜测。
*   **记录**–每个认证事件可以有选择地记录到磁盘。这些信息在 red 团队中非常有用，可以为客户提供详细的攻击时间表，这些时间表可以映射回记录的事件。

**依赖关系**

BruteLoops 需要 **Python3.7 或更新的**和 SQLAlchemy 1.3.0，后者可以通过 pip 和这个资源库中的 requirements.txt 文件获得:`**python3.7 -m pip install -r requirements.txt**`

**安装**

**git 克隆 https://github.com/arch4ngel/bruteloops
CD bruteloops
python 3-m pip install-r requirements . txt**

我如何使用这该死的东西？

呀，已经好了…我们可以把攻击分成几个步骤:

*   找到可攻击的服务
*   如果在 **`example.py` [** 1]目录中还没有可用的回调函数，就构建一个回调函数
*   找到一些用户名、密码和凭证
*   通过将认证数据传递给`**dbmanager.py**` [2]来构建数据库
*   如果相关，列举或请求 AD 锁定策略以智能配置攻击
*   根据目标锁定策略执行攻击[1][3][4]

[**Download**](https://github.com/arch4ngel/BruteLoops)