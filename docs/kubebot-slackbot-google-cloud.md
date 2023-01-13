# kube bot:Google 云平台上的安全测试 Slackbot

> 原文：<https://kalilinuxtutorials.com/kubebot-slackbot-google-cloud/>

Kubebot 是一个安全测试 Slackbot，在 Google 云平台上用 Kubernetes 后端构建。

**数据流**

*   1–API 请求(工具、目标、选项)从 Slackbot 发起，发送到 API 服务器，该服务器在 Kubernetes (K8s)集群上作为 Docker 容器运行，并且可以扩展。
*   2–API 服务器将接收到的请求作为消息发送到发布订阅工具主题。
*   3–消息发布到工具订阅。
*   4–在 K8s 集群上作为 Docker 容器运行的订阅工作器使用来自订阅的消息。这些工人的数量也可以扩大。
*   5–根据从最终用户收到的工具、目标和选项，在与 Docker 容器相同的 K8s 集群中启动适当的工具工人。结果临时存储在该容器的本地目录中。该工具的 Github 目录被克隆。
*   6–检查生成的结果文件是否存在。如果它不存在，它会被添加，更改会被推送到 Github。如果存在，就比较文件，新文件被推送到 Github，只有更改被推送到下一步。
*   7–来自工具工人的 webhook 将更改发送回 Slack。工具工人被删除，因为不再需要他们。

PS–在部署到 K8s 集群之前，API 服务器、订阅工作器和工具工作器的所有 Docker 映像都是从该 GCP 帐户的 Google 容器注册中心下载的。

**也可以理解为-[Find domain-使用证书透明性日志来查找子域的工具](https://kalilinuxtutorials.com/findomain-certificate-transparency-subdomains/)**

到目前为止集成的工具列表(随着更多工具的加入，该列表将不断更新。“工具”文件夹中有一些附加工具，但它们仍在开发中。)

*   [自定义菜单](https://github.com/anshumanbh/kubebot/blob/master/tools/enumall/enumall-ab.py)
*   [git-all-secrets](https://github.com/anshumanbh/git-all-secrets)
*   [gitrob](https://github.com/michenriksen/gitrob) 。还要检查 [gitrob-server](https://github.com/anshumanbh/kubebot/blob/master/docs/gitrob-server.md) ，以便在运行 gitrob 客户机的 Slash 命令之前先启动 Gitrob 服务器。
*   [git-secrets](https://github.com/awslabs/git-secrets)
*   [捉鬼敢死队](https://github.com/OJ/gobuster)
*   [nmap](https://nmap.org/)
*   [子类](https://github.com/TheRook/subbrute)
*   [子列表 3r](https://github.com/aboul3la/Sublist3r)
*   [松露猪](https://github.com/dxa4481/truffleHog)

**迄今为止集成的自动化工作流列表(随着更多工作流的添加，该列表将不断更新)**

*   [wfuzz 基本认证强制实施](https://github.com/anshumanbh/kubebot/blob/master/docs/automation-workflow.md)

**文件夹布局**

*   [API](https://github.com/anshumanbh/kubebot/blob/master/api)–包含 Kubebot API 服务器的所有代码。
*   [config](https://github.com/anshumanbh/kubebot/blob/master/config)–包含部署 Kubebot 组件的配置文件。
*   [cron jobs](https://github.com/anshumanbh/kubebot/blob/master/cronjobs)–包含一个示例部署(。yaml)文件来设置在特定时间间隔运行特定工具的 cronjobs，并通过 Webhook 将结果发送回 Slack。
*   [文档](https://github.com/anshumanbh/kubebot/blob/master/docs)–文档
*   [img](https://github.com/anshumanbh/kubebot/blob/master/imgs)–图像
*   [设置脚本](https://github.com/anshumanbh/kubebot/blob/master/setup-scripts)–一些用于设置 Kubebot 的脚本。
*   [订阅工作器](https://github.com/anshumanbh/kubebot/blob/master/subscriptionworker)–包含订阅工作器的代码。
*   [工具](https://github.com/anshumanbh/kubebot/blob/master/tools)–kube bot 可以运行的所有工具。有些仍在研究中。
*   [实用程序](https://github.com/anshumanbh/kubebot/blob/master/utils)–实用程序文件夹。
    *   一个名为`checkfile`的工具容器用于对 github 文件执行 diff 操作，以识别工具上次运行和最近一次运行之间的任何变化。该容器在每个工具容器之后运行。
    *   名为`converttobq`的实用程序用于将工具中的数据转换成 BigQuery 可接收的格式。该工具在自动化工作流中运行，每个工具的结果都存储在 BQ 中，以便其他工具使用。
    *   一个名为`wfuzzbasicauthbrute`的实用程序用于使用存储在另一个 BQ 表中的所有秘密来强制执行存储在一个 BQ 表中的端点的基本认证机制
*   . env . sample——将该文件重命名为`.env`,并确保在本地部署 Kubebot 时其中的值是准确的。
*   Makefile——用于构建 Kubebot 环境的 makefile。

**入门**

*   [先决条件](https://github.com/anshumanbh/kubebot/blob/master/docs/pre-requisites.md)–请确保满足所有这些先决条件。
*   [在本地运行 Kubebot](https://github.com/anshumanbh/kubebot/blob/master/docs/local-kubebot.md)–这是在远程运行 kube bot 之前开始习惯它的好地方。
*   [集成自己的工具](https://github.com/anshumanbh/kubebot/blob/master/docs/integration.md)–如果你想将自己的工具集成到 Kubebot 中，这很容易做到！
*   请帮助我让 Kubebot 变得更好！
*   一旦你确信 Kubebot 在本地工作正常(使用 Minikube ),并且现在想要释放它并在云上充分发挥它的潜力，它可以部署在谷歌容器引擎(GKE)集群上。然而，我现在还不能提供远程部署的说明。话虽如此，如果有兴趣，我将非常乐意协助。此外，如果你希望只是将 Kubebot 用作一个松散的应用程序，而不担心后端基础设施，也可以安排一个小的每月订阅计划，因为我将在我的个人 GCP 帐户中托管后端，而你只需负责在云提供商上托管 VPS 的正常成本。请随时联系我们讨论这些选项。

**Slack 中的样本斜线命令**

注意如何使用工具名称、选项和目标运行斜杠命令。我说目标是因为您可以运行一个斜杠命令来运行一个带有一组选项的工具来对付多个目标。例如，下面的 gitrob 命令正在针对`test`和`abc`运行。

*   /runtool nmap |-Pn-p 1-1000 | Google . com
*   /runtool sublist 3r |-t 50 | test . com
*   /runtool gobuster|-m dns -w 凶 _ 主机列表. txt -t 10 -fw|google.com

PS–单词列表可供选择:

bitquark _ 2016 02 27 _ subdomains _ popular _ 1000000 . txt
deep magic . com _ top 500 prefixes . txt
凶 _ hostlist . txt
namelist . txt
names . txt
sorted _ knock _ DNS recon _ 凶 _ recon-ng . txt
subdomains-top 1 mil-110000 . txt

*   /runtool enu mall |-s shod an-API-key | test . com
*   /runtool subbrute|-s 子文件/names.txt -v|kubebot.io(这需要很长时间)
*   /runtool git rob | analyze–no-banner–no-server | test，abc
*   /run tool trufflehg |[https://github . com/kingasius/iaquest . git](https://github.com/KingAsius/iaquest.git)
*   /runtool git secrets | |[https://github.com/pmyagkov/slack-emoji-bots.git](https://github.com/pmyagkov/slack-emoji-bots.git)
*   /run tool gitall secrets |-user | secret 1，secret 2
*   /runtool gitall secrets |-tool name repo-supervisor-org | secretor g123
*   /run tool gitall secrets |-repourl |[https://github . com/anshuman BH/docker-lair . git](https://github.com/anshumanbh/docker-lair.git)
*   /run tool gitall secrets |-gisal |[https://gist . github . com/anshuman BH/f48 dc1 d9 D8 b 2158252 f 716 a 3719 BF 8 e 6](https://gist.github.com/anshumanbh/f48dc1d9d8b2158252f716a3719bf8e6)
*   /run automation wfuzzbasicauthrubert |<[www.target.com](http://www.target.com)>。

**演示视频**

[https://www.youtube.com/embed/RKvtyU3CcZk?feature=oembed&enablejsapi=1](https://www.youtube.com/embed/RKvtyU3CcZk?feature=oembed&enablejsapi=1)

[https://www.youtube.com/embed/-ApGLGOV0vc?feature=oembed&enablejsapi=1](https://www.youtube.com/embed/-ApGLGOV0vc?feature=oembed&enablejsapi=1)

**Installing Kubebot Locally**

[https://www.youtube.com/embed/R2aMWGyldlI?feature=oembed&enablejsapi=1](https://www.youtube.com/embed/R2aMWGyldlI?feature=oembed&enablejsapi=1)

**Running nmap**

[https://www.youtube.com/embed/6SdkjrRGFhI?feature=oembed&enablejsapi=1](https://www.youtube.com/embed/6SdkjrRGFhI?feature=oembed&enablejsapi=1)

**Running sub-domain bruteforcing tools**

[https://www.youtube.com/embed/aip1Q0aCBhQ?feature=oembed&enablejsapi=1](https://www.youtube.com/embed/aip1Q0aCBhQ?feature=oembed&enablejsapi=1)

**Running git searching tools**

[**Download**](https://github.com/anshumanbh/kubebot)