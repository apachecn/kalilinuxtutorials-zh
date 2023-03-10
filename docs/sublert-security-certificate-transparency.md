# 子许可:利用证书透明性的安全和侦察工具

> 原文：<https://kalilinuxtutorials.com/sublert-security-certificate-transparency/>

[![Sublert : Security & Reconnaissance Tool Which Leverages Certificate Transparency](img/9e0f91822d905a17bce35cc55f2e533f.png "Sublert : Security & Reconnaissance Tool Which Leverages Certificate Transparency")](https://1.bp.blogspot.com/-5E307wacsok/XWNxxOF4mYI/AAAAAAAACLc/zg063g8oR4EnLPUn3EqdMnOuA0VLHwjHACLcBGAs/s1600/5%2B%25281%2529.png)

**Sublert** 是一个安全和侦察工具，它利用证书透明性来自动监控由特定组织部署的新子域名和颁发的 TLS/SSL 证书。

该工具应该在固定的时间、日期或间隔(理想情况下是每天)定期运行。新标识的子域将通过通知推送发送到松弛工作区。此外，该工具执行 DNS 解析以确定工作子域。

**要求**

*   运行在 Unix 上的虚拟专用服务器(VPS)。(我个人用 digitalOcean)
*   Python 2.x 或 3.x。
*   空闲工作空间。

**亦读-[AutoRDPwn:影子攻击框架](https://kalilinuxtutorials.com/autordpwn-shadow-attack-framework/)**

**如何设置？**

*要求*:

*   运行在 Unix 上的虚拟专用服务器(VPS)。(我用的是[数字海洋](https://digitalocean.com/)
*   Python 2.x 或 3.x。
*   自由松弛的工作场所。

首先，您必须将这个工具从 Github 克隆到您的 web 服务器上:

$ git clone[https://github . com/yasinaboukor/sublert . git](https://github.com/yassineaboukir/sublert.git)&&CD sufferet

现在，我们可以安装所需的模块，如下所示:

forPython *2:*

**$ sudo pip 安装要求. txt**

或者，Python 3:

**$ sudo pip 3 install-r requirements . txt**

下一步是创建一个宽松的工作场所，新的子域将被发送到那里。只需浏览到[https://slack.com/](https://slack.com/)并创建一个免费账户。

然后，创建两个通道:一个用于子域，另一个用于错误记录，如下所示:

![](img/209bb2469e788e462248efaa905fd9dd.png)

接下来，我们需要为每个通道生成 Webhook URLs，这样我们就可以利用 Slack API。

浏览到[https://api.slack.com/apps](https://api.slack.com/apps)并创建一个新的应用程序。

浏览到 ***传入的 Webhooks*** ，创建两个 Webhooks，并将每个 Webhooks 链接到之前形成的两个通道。

![](img/5979378c7a985c9f452965db2e426e99.png)

并将每个网钩与相应的松弛通道相链接。

![](img/f93495699f563c84a8975955e0b038c0.png)

您将获得以下格式的链接:

[**https://hooks . slack . com/services/XXXXXXX/bf0x xxxx me/XXXXXXXXXXXXX**](https://hooks.slack.com/services/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)

复制两个 webhook 链接并编辑 **config.py**

![](img/a37a4e2a943d6bf0a37dac504af33893.png)

你差不多准备好了！现在有趣的部分是增加域名，以监测新的子域。现在，最好分别添加每个域。让我们以 PayPal 为例:

**$ python sub lert . py-u paypal.com**

![](img/f910730e8c35d4aff55c766bd4351724.png)

您可以用同样的方式处理您想要监控的所有其他域名。一旦完成了目标的添加，下一步就是配置 **Cron** 以便在固定的时间定期调度 Sublert 的执行。

让我们使 Sublert.py 可执行:

**$ chmod u+x sublert.py**

现在，我们需要添加一个新的 Cron 作业来调度它在给定时间的执行。为此，请键入:

**$ Crontab -e**

在 Cron 文件的末尾添加以下行:

**0 */12 * * * CD/root/sub lert/&&/usr/bin/python sub lert . py-r-l>>/root/sub lert/sub lert . log 2>&1**

您需要将 **/root/sublert/** 更改为您拥有该工具的确切目录。

如果你使用 python3，确保将 **/usr/bin/python** 改为 **/usr/bin/python3**

*   **0 */12 * * *** →指示 Cron 每隔 12 小时运行一次工具。如果你想把它改成你想要的任何固定时间，可以随意使用 https://crontab.guru/的[来定制你的时间。](https://crontab.guru/)
*   **-r** →指示子权限执行 DNS 解析。这是可选的，但建议使用。
*   **–l→**指示 Sublert 记录错误并将其推送到 Slack 通道。这是可选的，但建议使用。
*   **/var/log/sublert . log 2>&1**→指示 Cron 将 sub lert 输出保存到/var/log/sublert.log，如果您对工具运行是否顺畅有任何疑问，可以随时查看。

**用法**

| 简易格式 | 长格式 | 描述 |
| --- | --- | --- |
| -你 | –网址 | 添加要监控的域。例如:yahoo.com。 |
| -d | –删除 | 要从监控列表中删除的域。例如:yahoo.com。 |
| ［构成动植物的古名或拉丁化的现代名］ | –列表 | 列出所有受监控的域。 |
| 相当于-ED | –螺纹 | 要使用的并发线程数(默认值:20)。 |
| -r | –解决 | 执行 DNS 解析。 |
| -我 | –记录 | 启用基于时差的错误日志记录。 |
| -m | –重置 | 重置一切。 |

[**Download**](https://github.com/yassineaboukir/sublert)