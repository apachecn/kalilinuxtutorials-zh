# Networkit:一个不断发展的用于大规模网络分析的开源工具包

> 原文：<https://kalilinuxtutorials.com/networkit/>

[![](img/d89fab1b6265f4b8ffd6ed2235161315.png)](https://blogger.googleusercontent.com/img/a/AVvXsEjER7ac6p5knKD58GQXhbYAP8qWEJf06Lz2FNLwa1grnNU88OqIoY4elDp46m_nwmBzU9aJa4fF8BXJuDA6K6aED4BPc7XbhhjI5pp_9nBxyi1avKXCXLbmClJ2Ob_JNbMdsK25DWETnuEWZE3ye6qzBQHQIZKJPyp05-JVEqvV3sg87eNIVy8tp1vB=s1347)

**NetworKit** 是一个用于高性能网络分析的开源工具套件。它的目标是为分析从数千到数十亿条边的大型网络提供工具。为此，它实现了高效的图形算法，其中许多算法是并行的，以利用多核架构。这意味着计算网络分析的标准措施。网络 it 注重可扩展性和全面性。NetworKit 也是算法工程的试验台，包含最近发表的研究中的新算法(见下面的出版物列表)。

它是一个 Python 模块。高性能算法用 C++编写，并通过 Cython 工具链向 Python 公开。Python 反过来给了我们交互工作的能力和丰富的数据分析和科学计算工具环境。此外，如果需要，可以构建 NetworKit 的核心并将其用作本地库。

**要求**

您将需要以下软件来将 NetworKit 作为 python 包安装:

*   现代 C++编译器，例如:g++ (>= 6.1)，clang++ (>= 3.9)或 MSVC (>= 14.13)
*   OpenMP for parallelism(通常随编译器一起提供)
*   Python3(支持 3.6 或更高版本)
    *   Python3 的开发库。包名取决于您的发行版。示例:
        *   Debian/Ubuntu: `**apt-get install python3-dev**`
        *   RHEL/CentOS: `**dnf install python3-devel**`
        *   Windows:使用 www.python.org 官方发布的安装程序
*   点
*   CMake 版本 3.6 或更高版本(如果可用，建议使用系统包。备选:`**pip3 install cmake**`)
*   建造系统:制造还是忍者
*   Cython 版本 0.29 或更高版本(如`**pip3 install cython**`)

**安装**

为了使用 NetworKit，您可以通过包管理器安装它，或者从源代码构建 Python 模块。

**通过软件包管理器安装**

虽然最新版本通常适用于所有的软件包管理器，但是旧的可下载版本的数量有所不同。

匹普

**pip3 安装[–用户]网络 it**

康达(康达-福吉频道)

**conda 配置–添加 conda-forge 频道
conda 安装网络 it [-c conda-forge]**

啤酒

**brew 安装网络 it**

一巴掌

**打包安装 py-networkit**

**从源代码构建 Python 模块**

**git 克隆 https://github.com/networkit/networkit 网络 it
cd 网络 it
python 3 setup . py build _ ext[-jX]
pip 3 install-e .**

脚本将调用`**cmake**`和**T1(`make`作为后备)将 NetworKit 编译为库，构建扩展并复制到顶层文件夹。默认情况下，NetworKit 将使用优化模式下的可用内核数量构建。有可能添加选项`**-jN**`用于编译的线程数量。**

**用法举例**

要了解网络 it 的不同功能/类别，请查看我们的交互式笔记本部分，尤其是网络 it 用户指南。注意:要查看和编辑笔记本的计算输出，建议使用 Jupyter 笔记本。这需要预先安装 NetworKit。在开始进行网络分析之前，您真应该检查一下。

我们还提供了我们笔记本的一个活页夹实例。要访问此服务，您可以点击顶部的徽章或点击此链接。免责声明:由于基础映像的重建，您的 Binder 实例需要一段时间才能使用。

如果你只想简单地看看网络是如何使用的——下面的例子提供了一个例子。这里，我们生成一个具有 100k 个节点的随机双曲图，并使用 PLM 方法计算其社区:

**导入 networkit 为 nk
g = nk.generators .双曲线生成器(1e5)。generate()
communities = NK . community . detect communities(g，inspect=True)
PLM(balanced，pc，turbo)在 0.14577102661132812【s】
解决方案属性:
communities 4536
最小社区大小 1
最大社区大小 2790
平均。社区规模 22.0459
模块化 0.987243
——————————**

**仅安装 C++内核**

如果您只想使用 NetworKit 的 C++核心，您可以通过包管理器安装它或者从源代码构建它。

**通过包管理器**安装 C++内核

康达(康达-福吉频道)

**conda 配置–添加通道 conda-forge
conda 安装 libnetworkit [-c conda-forge]**

啤酒

**brew 安装 libnetworkit**

一巴掌

**spack 安装 libnetworkit**

**从源代码构建 C++内核**

我们推荐 CMake 和您首选的构建系统来构建 NetworKit 的 C++部分。

以下描述仅显示了如何使用 CMake 来构建 C++核心:

首先，您必须创建并更改一个构建目录:(在本例中命名为`**build**`)

**mkdir 构建
cd 构建**

然后调用 CMake 为`**make**`构建系统生成文件，指定根`**CMakeLists.txt**`文件的目录(例如`**..**`)。在此之后，调用`**make**`开始构建过程:

**cmake..
make -jX**

为了加快编译速度，在多核机器上，你可以添加`**-jX**`，其中 X 表示要编译的线程数。

**把 NetworKit 当库用**

本段解释了如何使用 NetworKit core C++库，如果它是从源代码构建的。通过包管理器安装时如何使用，最好参考官方文档( [brew](https://brew.sh/) 、 [conda](https://docs.conda.io/) 、 [spack](https://spack.readthedocs.io/en/latest) )。

为了使用以前编译的 networkit 库，您需要安装它，并在编译项目时链接它。使用这些说明在`/usr/local`中编译和安装 NetworKit:

**cmake..
make -jX 安装**

一旦安装了 NetworKit，就可以在 C++应用程序中使用 include 指令，如下所示:

**#包括****<network it/graph/graph . HPP**>

您可以编译您的源代码，如下所示:

**g++ my _ file . CPP-lnetworkit**

**单元测试**

构建和运行 NetworKit 单元测试不是强制性的。但是，作为一名开发人员，您可能希望为您的代码编写并运行单元测试，或者如果您遇到任何有关 NetworKit 的问题，您可能希望检查 NetworKit 是否正常运行。单元测试只能从存储库的克隆或副本中运行，而不能从 pip 安装中运行。为了运行单元测试，您需要首先编译它们。这是通过将 CMake `**NETWORKI_BUILD_TESTS**`标志设置为`**ON**`来实现的:

**cmake-DNETWORKIT _ BUILD _ TESTS = ON**..

单元测试是使用 GTest 宏实现的，比如`**TEST_F(CentralityGTest, testBetweennessCentrality)**`。单一测试可通过以下方式执行:

**。/network it _ tests–gt test _ filter = centrality gt test . test between ness centrality**

此外，可以通过添加`**--loglevel <log_level>**`来指定日志输出的级别；支持的日志级别有:`**TRACE**`、`**DEBUG**`、**、`INFO`、**、`**WARN**`、`**ERROR**`和`**FATAL**`。

**用地址/泄漏杀毒程序编译**

清理程序是调试代码的好工具。NetworKit 提供了额外的 Cmake 标志来启用地址、泄漏和未定义行为清理程序。要用杀毒程序编译代码，将 CMake `**NETWORKIT_WITH_SANITIZERS**`设置为`**address**`或`**leak**`:

**cmake-DNETWORKIT _ WITH _ sanitiners = leak..**

通过将此标志设置为`**address**`，您的代码将使用`**address**`和`**undefined**`杀毒程序进行编译。将其设置为`**leak**`还会添加`**leak**`消毒剂。

[**Download**](https://github.com/networkit/networkit)