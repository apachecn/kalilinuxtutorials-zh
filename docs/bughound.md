# Bughound:基于弹性搜索的静态代码分析工具

> 原文：<https://kalilinuxtutorials.com/bughound/>

[![Bughound : Static Code Analysis Tool Based On Elastic search](img/9cf6109a58807c7aa6446844ec0bea29.png "Bughound : Static Code Analysis Tool Based On Elastic search")](https://1.bp.blogspot.com/-bA9y5CUGF_Q/YPOohdS4dAI/AAAAAAAAKE8/Q-jflAw9B08g0MyHH3gOZeoTBXDQNclMgCLcBGAsYHQ/s517/1%2B%25281%2529.png)

**Bughound** 是一个开源的静态代码分析工具，它分析你的代码，并将结果发送给 Elasticsearch 和 Kibana，以获得关于你代码中潜在漏洞的有用见解。

Bughound 拥有自己的 Elasticsearch 和 Kibana Docker 图像，并预先配置了仪表盘，为您提供强大的可视化结果。

您可以检测各种类型的漏洞，例如:

*   命令注入。
*   XXE。
*   不安全的反序列化。
*   还有更多！

Bughound 目前可以分析`PHP`和`JAVA`代码，它包含了一组针对这些语言的不安全函数。

我会确保随着时间的推移添加越来越多的功能/语言，但现在主要的焦点是项目稳定性本身。

***请注意，Bughound 的结果并非 100%准确，它旨在帮助您在分析调查过程中识别潜在的弱点。***

它是如何工作的？

首先，Bughound 将基于您想要审计的文件的扩展名构建您的项目内所有文件的列表，然后它将读取每个文件，并尝试找到您的项目语言的任何预定义的不安全函数。

分析阶段依赖于预先配置的正则表达式和一些自定义的文本匹配来检测潜在的漏洞，所以同样，您需要进行手动分析，以便检查这些发现是否可被利用。

最后，它会将结果发送到 Bughound docker 映像，该映像有一个预配置的 Elasticsearch 和 Kibana，其中包含为您的发现定制的仪表板。

仪表盘将为您提供有关调查结果的详细信息，例如:

*   函数名。
*   漏洞的类别。
*   行号。
*   还有更多！

此外，使用 Kibana，您将能够查看潜在易受攻击的代码片段，以开始进行分析和跟踪，检查它是否可被利用。

当然，如果您愿意，您可以使用自己的 ELK 堆栈，Bughound 将为您进行初始配置，但是在这种情况下，您将没有预配置的仪表板。

**要求**

您可以使用以下命令安装运行 Bughound 代码的所有要求:

`**pip3 install -r requirements.txt**`

这将确保为代码安装了所有的需求。

此外，您需要安装 Docker 来运行 Bughound 映像，下一节将详细介绍！

**如果你想使用你自己的 Elasticsearch 和 Kibana 实例，跳过 docker 安装步骤**

**安装**

确保使用以下命令获得最新版本的 Bughound:

`git clone https://github.com/mhaskar/Bughound`

在安装了上一步中的要求后，您可以使用以下命令运行 Bughound:

`./bughound.py`

你会看到 Bughound 的主屏幕。

**┌─[askar@hackbook]─[/opt/bughound】
└──╼美元。/bughound . py
*_ _ _ _ _ _**_*_。_* 。*_*
|*\ | | | |/*| | | |/\ | | |
| | | |
| |*| || ||
|
||||*|
|
|
|
|
|
|*|
|
|
|
|
|*|
|*|
|–.| | _<| | | | | | _ | | | | | | | | |。`| | | | | | |_) | |`–' | | | | | | |`--' | |`–' | | | \ | | '–' | |/_ _ _ _ _ _/_ _ _ _ _ _ | | | | _ _ _ _ _ _/_ _ _ _ _ _/| ^ _ _ |*/
\/
oVo
_ _ _ XXX*/
XXXXX
/XXXXX \
/XXX \
V 1.0 Beta
[+]举例:。/bughound 3 . py–路径 vulnerable _ code/–语言 PHP–扩展。PHP–name test project
用法:bughound . py[-h][–path path][–git git]–language language
–extension extension–name[–verbose[verbose]]
bughound . py:error:argument–language 必选
┌─[✗]─[askar@hackbook]─[/opt/bughound】
└──╼$**

**Docker 镜像安装**

要安装 Bughound docker 映像，您只需执行以下操作:

`**docker pull bughound/bughound**`

这将获取图像的最新版本，并将其保存到您的机器上。

提取映像后，我们可以使用以下命令运行它:

`**docker run --name bughound -p5601:5601 -p 9200:9200 bughound/bughound**`

这将在一个名为`bughound`的新容器下运行映像，并暴露 Bughound 将 Elasticsearch 和 Kibana 与您的主机通信所需的端口。

您可能需要增加最大虚拟内存来使用映像，因此请确保运行以下命令:

`**sysctl -w vm.max_map_count=262144**`

完成两件事之后，现在就可以使用 Bughound 了！

**用途**

要开始代码的分析过程，您应该使用有一些选项的`Bughound.py`文件，要通过帮助横幅查看这些选项，您可以使用以下命令:

**┌─[✗]─[askar@hackbook]─[/opt/bughound】
└──╼美元。/bughound.py -h
。**_*_。_* 。*_*
|*\ | | | |/*| | | |/\ | | |
| | | |
| |*| || ||
|
||||*|
|
|
|
|
|
|*|
|*|
|
|
|
|
|*|
|–.| | _<| | | | | | _ | | | | | | | | |。`| | | | | | |_) | |`–' | | | | | | |`--' | |`–' | | | \ | | '–' | |/_ _ _ _ _ _/_ _ _ _ _ _ | | | | _ _ _ _ _ _/_ _ _ _ _ _/| ^ _ _ |*/
\/
oVo
_ _ _ XXX*/
XXXXX
/XXXXX \
/XXX \
V 1.0 Beta
[+]举例:。/bughound 3 . py–路径 vulnerable _ code/–语言 PHP–扩展。PHP–name test project
用法:bughound . py[-h][–path path][–git git]–language language
–extension extension–name name[–verbose[verbose]]
可选参数:
-h，–help 显示此帮助消息并退出
–path path 源代码的本地路径
–git git 库 URL
–language 所使用的编程语言
–extension extension
要搜索的扩展
–name***

 ***扫描本地项目**

例如，要扫描本地 php 项目，可以使用以下命令:

`**./bughound.py --path /opt/dummyproject --language php --extension .php --name dummyproject**`

该命令将在 Elasticsearch 索引中创建一个名为“dummyproject”的新项目，并抓取所有扩展名为“”的本地文件。php“在本地路径”/opt/dummyproject”并将结果发送到 Elasticsearch。

**扫描远程 Git 库**

此外，您可以使用如下的`--git`开关从 git 存储库中提取远程项目:

`**./bughound.py --git https://github.com/DummyCode/DummyProject --language php --extension .php --name dummyproject**`

Bughound 会为你克隆代码并保存在`projects`目录下，然后会扫描它。

**预配置仪表板**

如果您决定使用正式的 Bughound docker 映像，您将获得几个现成的仪表板，它们将帮助您进行分析。

到目前为止，以下仪表板可用:

*   Bughound 主仪表板
*   命令注入仪表板
*   反序列化仪表板
*   二十.仪表板

这些仪表板将为您提供关于代码中发现的函数和代码片段的统计数据，以便您可以开始您的分析过程。

[**Download**](https://github.com/mhaskar/Bughound)*