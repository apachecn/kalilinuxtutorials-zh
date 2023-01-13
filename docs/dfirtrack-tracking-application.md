# Dfirtrack:事件响应跟踪应用程序

> 原文：<https://kalilinuxtutorials.com/dfirtrack-tracking-application/>

DFIRTrack(数字取证和事件响应跟踪应用程序)是一个开源 web 应用程序，主要基于使用 [PostgreSQL](https://www.postgresql.org/) 数据库后端的 [Django](https://www.djangoproject.com/) 。

与主要基于案例并支持 CERTs、SOC 等工作的其他优秀事件响应工具形成对比。在他们的日常业务中，DFIRTrack 专注于处理一个有许多受影响系统的重大事件，这在 APT 案例中是常见的。

它旨在用作大型案件中专门事件响应团队的工具。因此，当然，CERTs 和 SOC 也可以使用 DFIRTrack，但他们可能会觉得在特殊情况下使用它更合适，而不是在日常工作中使用。

与基于案例的应用程序不同，DFIRTrack 以基于系统的方式工作。

它跟踪各种系统的状态以及与它们相关联的任务，使分析师在事故响应流程的调查阶段到补救阶段的任何时候都能够充分了解受影响系统的状态和数量。

**也可阅读:** [BeeBug:检查可利用性的工具](https://kalilinuxtutorials.com/beebug-checking-exploitability/)

**特性**

一个焦点是系统和相关信息的快速和可靠的导入和导出。导入系统的目标是提供一个快速无误的程序。

此外，导出系统及其状态的目标是拥有多个文档实例:例如，为技术人员提供详细的降价报告，为非技术人员提供电子表格，在数据集中没有冗余和偏差。

数字匹配的经理是快乐的经理！😉

目前实现了以下功能:

*   **进口商**
    *   系统和任务的创建者(通过 web 界面快速创建多个相关实例)，
    *   CSV(简单和通用的基于 CSV 的导入(主机名和 IP 或者主机名和标签与 web 表单相结合)，应该适合许多工具的导出功能)，
    *   条目降价(每个系统(报告)一个条目)。
*   **出口商**
    *   所谓系统报告的降价(在 [MkDocs](https://www.mkdocs.org/) 结构中使用)，
    *   电子表格(CSV 和 XLS)，
    *   乳胶(计划中)。

**安装和依赖**

DFIRTrack 是为部署在 **Debian Stretch** 或 **Ubuntu 16.04** 上开发的。其他基于 T4 Debian T5 的发行版或版本可能可以工作，但是还没有测试过。目前，该项目将集中于 Ubuntu LTS 和 Debian 版本。

为了在专用服务器上快速而简单地安装，包括所有依赖项，编写了[可回答的](https://docs.ansible.com/ansible/latest/)剧本和角色(此处[可用](https://github.com/stuhli/dfirtrack_ansible))。为了测试，准备了一个 docker 环境(见下文)。

对于最小设置，需要以下依赖关系:

*   `django` (2.0)，
*   `django_q`，
*   `djangorestframework`，
*   `gunicorn`，
*   `postgresql`，
*   `psycopg2-binary`，
*   `python3-pip`，
*   `PyYAML`，
*   `requests`，
*   `virtualenv`，
*   `xlwt`。

**注意，这个存储库中没有`settings.py`。** [该文件](https://github.com/stuhli/dfirtrack_ansible/blob/master/roles/dfirtrack/templates/settings.py.j2)通过 Ansible 提交或者需要手动复制配置。这在将来会有所改变(更多信息请参见问题)。

**Docker 环境**

这个项目提供了一个只在本地使用的实验性 Docker 组合环境。在项目根目录中运行以下命令来启动环境:

**坞站-合成**

已经创建了用户管理员。可以通过以下方式设置密码:

**坞站/setup_admin.sh**

该应用程序位于 localhost:8000。

**免责声明**

这个软件处于早期的阿尔法阶段，所以有很多工作要做。即使实现了一些基本的错误检查，到目前为止，DFIRTrack 的使用主要取决于正确的处理。

DFIRTrack 过去没有，将来也很可能永远不会用于公开的服务器。

尽管如此，还是实施了一些基本的安全功能(特别是与相应的责任角色相关的功能)。务必在安全的环境中安装 DFIRTrack(例如，专用虚拟机或独立网络中)！

[**Download**](https://github.com/stuhli/dfirtrack)