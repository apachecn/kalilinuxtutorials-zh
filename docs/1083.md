# 多扫描器:模块化文件扫描/分析框架

> 原文：<https://kalilinuxtutorials.com/multiscanner-modular-file-scanning-analysis/>

[![Multiscanner : Modular File Scanning/Analysis Framework](img/938c50ed559a92669bfbb493588e8c24.png "Multiscanner : Modular File Scanning/Analysis Framework")](https://1.bp.blogspot.com/-9YsvqGtOaY0/XhOqKSN-CfI/AAAAAAAAESU/b0CUD274U64437bGSnzDKKYSyVM708K5gCLcBGAsYHQ/s1600/MultiScanner%25281%2529.png)

**MultiScanner** 是一个文件分析框架，通过为用户自动运行一套工具并汇总输出来帮助用户评估一组文件。工具可以是定制的 Python 脚本、web APIs、在另一台机器上运行的软件等。通过创建在框架中运行的模块来合并工具。

模块被设计成可以快速编写并容易地集成到框架中。当前编写和维护的模块与恶意软件分析相关，但框架不限于该范围。有关模块列表，您可以在[模块/](https://github.com/mitre/multiscanner/blob/master/modules) 中查找。描述和配置选项可在[分析模块](http://multiscanner.readthedocs.io/en/latest/use/use-analysis-mods.html)页面找到。

它还支持用于样品存储、分析和报告查看的分布式工作流程。这个功能包括一个 web 界面、一个 REST API、一个分布式文件系统(GlusterFS)、分布式报告存储/搜索(Elasticsearch)和分布式任务管理(Celery / RabbitMQ)。更多详情请见[架构](http://multiscanner.readthedocs.io/en/latest/arch.html)。

**用途**

它可以用作命令行界面、Python API 或具有 web 界面的分布式系统。关于[安装](http://multiscanner.readthedocs.io/en/latest/install.html)和[使用](http://multiscanner.readthedocs.io/en/latest/use/index.html)的更多详细信息，请参见文档。

**也可阅读-[Pown:一个安全测试开发工具包](https://kalilinuxtutorials.com/pown-security-testing-toolkit/)建成**

**命令行**

如果你还没有安装 Python (2.7 或 3.4+)。

然后运行以下命令(用您想要扫描的实际文件替换`**<file>**`):

克隆 https://github.com/mitre/multiscanner.git
$ CD 多功能扫描仪
$ sudo -HE。/install.sh
$多扫描器初始化

这将为您生成一个默认配置。检查`**config.ini**`查看启用了哪些模块。更多信息见[配置](http://multiscanner.readthedocs.io/en/latest/install.html#configuration)。

现在您可以扫描文件(用您想要扫描的实际文件替换`**<file>**`):

**$多扫描仪<文件>**

您可以运行以下命令来获取所有 MultiScanner 命令行选项的列表:

**$ multi scanner–帮助**

**注意**:如果你不在基于 RedHat 或 Debian 的 Linux 发行版上，不要运行`**install.sh**`脚本，安装 pip(如果你还没有安装的话)并运行以下代码:

**$ pip install-r requirements . txt**

**Python API**

**导入 multi scanner
multi scanner . config _ init(file path)
output = multi scanner . multi scan(file _ list)
results = multi scanner . parse _ reports(output，python=True)**

**网页界面**

如果你还没有安装最新版本的 [Docker](https://docs.docker.com/engine/installation/) 和 [Docker Compose](https://docs.docker.com/compose/install/) 。

**$ git 克隆 https://github.com/mitre/multiscanner.git
$ CD 多扫描仪
$ docker-compose up**

您可能需要等待一段时间，直到所有服务都已启动并运行，但之后您就可以通过在网络浏览器中转至`**http://localhost:8000**`来使用网络界面。

*注意*:这不应该在生产中使用；这只是对完整安装的介绍。更多详情见[此处](http://multiscanner.readthedocs.io/en/latest/install.html#standalone-docker-installation)。

[**Download**](https://github.com/mitre/multiscanner)