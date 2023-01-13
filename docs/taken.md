# 采取:接管 AWS IPS &有一个子域接管的工作概念证明

> 原文：<https://kalilinuxtutorials.com/taken/>

[![Taken : Takeover AWS IPS & Have A Working POC For Subdomain Takeover](img/20a7644a9d1c56753e780bbec4ca124b.png "Taken : Takeover AWS IPS & Have A Working POC For Subdomain Takeover")](https://1.bp.blogspot.com/-QxyNMyZVMCI/X5a6zDVluzI/AAAAAAAAH2M/AefRtKI7TJIuN0amQWgAjRrfX7POlowVwCLcBGAsYHQ/s728/Taken.png)

**Taken** 是一个接管 AWS ips 的工具，并有一个用于子域接管的工作 POC。想法很简单

*   获取子域。
*   进行反向查找以仅保存 AWS ips。
*   每分钟重新启动一次 EC2 实例。公共 ip 在每次重启时都会轮换。匹配它与您现有的子域 IP 列表，你有一个工作子域接管概念。
*   一旦你接管了一个子域，就通过电子邮件通知

**先决条件**

*   AWS 帐户
*   Linux 和 Bash 脚本知识

**使用的技术/框架**

**用**建造

*   `Bash`

**特性**

*   收集子域名并进行反向查找，只针对 AWS ips。
*   通过重新启动 ec2 实例来轮换 IP，直到它与列表中的 IP 之一匹配。
*   在匹配时，IP/主机被添加到白名单文件中，因此它不会再次轮换并发送电子邮件通知。

**使用**的详细步骤

*   创建一个实例 t2.medium(攻击机器)，免费 24*365。
*   使用实例类型 t3a.nano 创建 5-10 个实例，可能在一个或多个地区成本最低(数量越多机会越多，但 10 台机器每月的费用约为 60 美元),需要 5 分钟，让 SG 组仅向您的公共 ip 开放。
*   创建 AWS API 密钥来停止/启动实例。
*   SSH 到您的攻击机器。
*   安装电子邮件通知实用程序 SSMTP。[https://www . digital ocean . com/community/questions/how-to-send-emails-from-a-bash-script-using-ssmtp](https://www.digitalocean.com/community/questions/how-to-send-emails-from-a-bash-script-using-ssmtp)
*   安装 subfinder 和 sublist3r.py 工具，用于收集子域。(或者任何其他你想要的工具，但这需要你将它添加到子域收集脚本中)按照步骤设置这些工具[https://github.com/aboul3la/Sublist3r](https://github.com/aboul3la/Sublist3r)https://github.com/projectdiscovery/subfinder[](https://github.com/projectdiscovery/subfinder)
*   克隆已执行的回购并打开一个屏幕会话来运行子域收集脚本。如果您不知道如何使用屏幕会话-[https://linuxize.com/post/how-to-use-linux-screen/](https://linuxize.com/post/how-to-use-linux-screen/)
*   创建一个包含所有域的文本文件，将它作为“all domains”保存在同一个目录中，然后运行子域收集脚本。该脚本使用 subfinder 和 sublist3r.py。这将在每行中以“subdomain:IP”的格式生成一个或多个域的所有子域的列表。这将在以后用于匹配和通知。
*   打开另一个屏幕会话，并在该会话中导出 AWS 凭据。正在导出 AWS 密钥。`export AWS_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE The access key for your AWS account.`
    `export AWS_SECRET_ACCESS_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY The secret access key for your AWS account.`
    在不同的屏幕会话中运行接管脚本。您还可以在不同的屏幕会话中为每个区域运行(查看下面的屏幕截图)。
    `Reasoning`–AWS 中的每个区域都关联了不同的 IP 子网。为了锁定位于美国的公司，它们很有可能在美国的任何地区经营，但也可能在其他地区拥有资产，如爱尔兰、法兰克福等。因此，不要在一个地区运行 10 项资产，而是尝试在公司总部所在的地区运行 5 项资产，在不同的地区运行另外 5 项资产。

**屏幕会话示例**:

![](img/659d7178ebb1218907c039dcf10ef92b.png)

**电子邮件通知:**

![](img/0fe4907ff9d7baaf782d55ce0b8a48fd.png)

`Took over a subdomain what next`–SSH 进入该主机，创建一个简单的 HTML 文件并启动一个 python 服务器，您就有了一个正在运行的 POC。(我计划在下一个版本中自动完成这项工作)

**批量运行**

我浏览了 HackerOne 和 Bugcrowd 以及 SaaS 福布斯/SaaS 500 强公司的所有公共项目，收集了它们的子域名，然后开始点击。在 24 小时内，我能够接管 3 个子域名。在 3 个不同的地区总共运行 10 个实例。成功率在很大程度上取决于运行的实例数量。由于使用该脚本，您在 24 小时内更改了大约 1440 个 IP，因此在 24 小时内有 10 个实例的情况下，它将变成大约 14400 个 IP。

[**Download**](https://github.com/In3tinct/Taken)