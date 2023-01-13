# pyrdp:MITM & Python 3 的库，能够实时或事后观察连接

> 原文：<https://kalilinuxtutorials.com/pyrdp-mitm-library-for-python-3-with-the-ability-to-watch-connections-live-or-after-the-fact/>

[![Pyrdp : MITM & Library For Python 3 With The Ability To Watch Connections Live Or After The Fact](img/aa8602a405541540198c321fd118c2b3.png "Pyrdp : MITM & Library For Python 3 With The Ability To Watch Connections Live Or After The Fact")](https://1.bp.blogspot.com/-1x_DUnP8yc8/XYGvOfkeFfI/AAAAAAAACf4/1MPSuR8IMU0aYQUbcGGDj0lsToNTF_b5ACLcBGAsYHQ/s1600/New%2BProject.png)

PyRDP 是一个 Python 3 远程桌面协议(RDP)的中间人(MITM)和库。它有几个工具:

*   **RDP 中间人**
    *   记录连接时使用的凭据
    *   窃取复制到剪贴板的数据
    *   保存通过网络传输的文件的副本
    *   在后台对共享驱动器进行爬网并将其保存在本地
    *   保存连接的重播，以便以后查看
    *   在新连接上自动运行控制台命令或 PowerShell 有效负载
*   **RDP 玩家:**
    *   观看来自 MITM 的现场 RDP 连线
    *   查看 RDP 连接的重播
    *   控制活跃的 RDP 会议，同时隐藏您的行动
    *   列出客户端映射的驱动器，并在活动会话期间从这些驱动器下载文件
*   **RDP 证书克隆者:**
    *   使用与 RDP 服务器证书相同的字段创建自签名 X509 证书

我们使用这个工具作为 RDP 蜜罐的一部分，记录会话并保存恶意软件在我们目标机器上的副本。

PyRDP 最初是在一篇博客文章中介绍的，在这篇文章中，我们[展示了我们可以在行动中抓住一个真正的威胁角色。2019 年 5 月，其作者](https://www.youtube.com/watch?v=eB7RC9FmL6Q)在 NorthSec 做了一个[演示，并进行了两次演示。](https://docs.google.com/presentation/d/1avcn8Sh2b3IE7AA0G9l7Cj5F1pxqizUm98IbXUo2cvY/edit#slide=id.g404b70030f_0_581)[第一个涵盖了](https://youtu.be/5JztJzi-m48)凭证记录、剪贴板窃取、客户端文件浏览和会话接管。[第二部分讲述了](https://youtu.be/bU67tj1RkMA)当客户端成功通过身份验证时，cmd 或 powershell 有效负载的执行。2019 年 8 月，PyRDP 在黑帽兵工厂演示([幻灯片](https://docs.google.com/presentation/d/17P_l2n-hgCehQ5eTWilru4IXXHnGIRTj4ftoW4BiX5A/edit?usp=sharing))。

**也可阅读——主动统治:网络枚举&攻击工具集**

**支持的系统**

PyRDP 应该在 Python 3.6 和更高版本上工作。

该工具已经过测试，可以在 Linux (Ubuntu 18.04)和 Windows 上的 Python 3.6 上工作(参见第[节在 Windows 上安装](https://github.com/gosecure/pyrdp#installing-on-windows))。它还没有在 OSX 身上测试过。

**安装**

我们建议在[虚拟环境](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)中安装 PyRDP，以避免依赖性问题。

首先，确保安装必备包(在 Ubuntu 上):

sudo apt 安装 libd bus-1-dev libd bus-gli b-1-dev

在某些系统上，您可能需要安装`python3-venv`包:

sudo apt install python3-venv

然后，在 PyRDP 的目录中创建您的虚拟环境:

pydp CD
python 3-m venv venv

*不要*使用虚拟环境文件夹的根 PyRDP 目录(`**python3 -m venv .**`)。你会搞得一塌糊涂，反正用`venv`这样的目录名更规范。

在安装依赖项之前，您需要激活虚拟环境:

源 venv/bin/激活

最后，您可以使用 Pip 安装项目:

pip3 安装-U pip 设置工具轮
pip3 安装-U -e。

这应该会安装运行 PyRDP 所需的所有依赖项。

如果您想离开您的虚拟环境，只需将其停用即可:

复员

请注意，每当您希望 PyRDP 脚本作为 shell 命令可用时，您都必须激活您的环境。

**在 Windows 上安装**

步骤都差不多。还有两个额外的先决条件。

1.  任何 C 编译器
2.  [OpenSSL](https://wiki.openssl.org/index.php/Binaries) 。确保从您的`$PATH`可以到达。

然后，在 PyRDP 的目录中创建您的虚拟环境:

pydp CD
python 3-m venv venv

*不要*使用虚拟环境文件夹的根 PyRDP 目录(`**python3 -m venv .**`)。你会搞得一塌糊涂，反正用`venv`这样的目录名更规范。

在安装依赖项之前，您需要激活虚拟环境:

venv \脚本\激活

最后，您可以使用 Pip 安装项目:

pip3 安装-U pip 设置工具轮
pip3 安装-U -e。

这应该会安装运行 PyRDP 所需的所有依赖项。

如果您想离开您的虚拟环境，只需将其停用即可:

复员

请注意，每当您希望 PyRDP 脚本作为 shell 命令可用时，您都必须激活您的环境。

**用 Docker** 安装

首先，通过在 PyRDP 的根目录(Dockerfile 所在的位置)执行这个命令来构建映像:

坞站 build-t pydp。

之后，您可以执行以下命令来运行容器:

坞站运行-it pydp-mitm . py 192 . 168 . 1 . 10

有关各种命令和参数的更多信息，请参考以下章节:

*   [使用 PyRDP MITM](https://github.com/gosecure/pyrdp#using-the-pyrdp-man-in-the-middle)
*   [使用 PyRDP 播放器](https://github.com/gosecure/pyrdp#using-the-pyrdp-player)
*   [使用 PyRDP 证书克隆程序](https://github.com/gosecure/pyrdp#using-the-pyrdp-certificate-cloner)

永久存储 PyRDP 输出(日志、文件等)。)，将-v 选项添加到前面的命令中。例如:

docker run-v/home/my name/pyrdp _ output:/home/pyrdp/pyrdp _ output pyrdp
pyrdp-mitm . py 192 . 168 . 1 . 10

确保您的目标目录由 UID 为 1000 的用户拥有，否则您将得到一个权限被拒绝的错误。如果您是系统中唯一的用户，您应该不需要担心这个问题。

**使用 Docker 中的播放器**

使用播放器需要将 DISPLAY 环境变量从主机导出到 docker。这将播放器的 GUI 重定向到主机屏幕。您还需要暴露主机的网络，并阻止 Qt 使用 MIT-SHM X11 共享内存扩展。为此，请在 run 命令中添加-e 和–net 选项:

docker run-e DISPLAY = $ DISPLAY-e QT _ X11 _ NO _ MITSHM = 1–net = host pyrdp pyrdp-player . py

请记住，将主机的网络暴露给 docker 会损害容器和主机之间的隔离。如果您计划使用播放器，使用 SSH 连接的 X11 转发将是一种更安全的方式。

**从 pycrypto 迁移出去**

由于不再维护 pycrypto，我们选择迁移到 pycryptodome。如果出现此错误，这意味着您使用的是 pycrypto 模块，而不是 pycryptodome 模块。

[…]
文件“[…]/pyrdp/pyrdp/PDU/RDP/connection . py”，第 10 行，在来自 Crypto 的
中。public key . RSA import RsaKey
import error:无法导入名称“RSA key”

您需要删除模块 pycrypto 并重新安装 PyRDP。

pip3 卸载 pycrypto
pip3 install -U -e。

**使用 PyRDP 中间人**

使用`**pyrdp-mitm.py <ServerIP>**` **或** `**pyrdp-mitm.py <ServerIP>:<ServerPort**>`运行 MITM。

假设您有一个运行在`**192.168.1.10**`上并监听端口 3389 的 RDP 服务器，您将运行:

pyrdp-mitm.py 192.168.1.10

当第一次在 Linux 上运行 MITM 时，应该在`~/.config/pyrdp`中为您生成一个私钥和证书。当在连接上使用 TLS 安全时，会用到这些。例如，您可以使用它们来解密 Wireshark 中的 PyRDP 流量。

**指定私钥和证书**

如果密钥生成不起作用或者您想要使用自定义密钥和证书，您可以使用`-c`和`-k`参数来指定它们:

pyrdp-mitm . py 192 . 168 . 1 . 10-k private _ key . PEM-c certificate . PEM

**连接 PyRDP 播放器**

如果您想通过 PyRDP 播放器查看实时 RDP 连接，您需要使用`-i`和`-d`参数指定播放器正在监听的 ip 和端口。注意:port 参数是可选的，默认端口是 3000。

pydp-mitm . py 192 . 168 . 1 . 10-I 127 . 0 . 0 . 1-d 3000

**当 MITM 在服务器上运行时连接到 PyRDP 播放器**

如果你在服务器上运行 MITM，并且仍然想看到实时的 RDP 连接，你应该使用 [SSH 远程端口转发](https://www.booleanworld.com/guide-ssh-port-forwarding-tunnelling/)将你服务器上的一个端口转发到你机器上玩家的端口。一旦完成，就将`127.0.0.1`和转发的端口作为参数传递给 MITM。例如，如果服务器上的端口 4000 被转发到您机器上的播放器端口，则可以使用以下命令:

pydp-mitm . py 192 . 168 . 1 . 10-I 127 . 0 . 0 . 1-d 4000

**在新连接上运行有效载荷**

PyRDP 支持在建立新连接时自动运行控制台命令或 PowerShell 有效负载。由于 RDP 的性质，这个过程有点粗糙，并不总是 100%可靠。它是这样工作的:

*   等待用户通过身份验证。
*   阻止客户端的输入/输出，以隐藏有效负载并防止干扰。
*   发送一个假的 Windows+R 序列，运行`cmd.exe`。
*   将有效负载作为控制台命令运行，并退出控制台。如果配置了 PowerShell 有效负载，它将使用`powershell -enc <PAYLOAD>`运行。
*   稍等片刻，让有效负载完成。
*   恢复客户端的输入/输出。

为此，您需要设置 3 个参数:

*   有效载荷
*   有效负载开始前的延迟
*   有效负载的持续时间

**设定有效载荷**

您可以使用下列参数之一来设置要运行的有效负载:

*   `**--payload**`，包含控制台命令的字符串
*   `**--payload-powershell**`，包含 PowerShell 命令的字符串
*   `**--payload-powershell-file**`，PowerShell 脚本的路径

**选择何时启动有效载荷**

目前，PyRDP 不检测用户何时登录。在运行有效负载之前，您必须给它一段等待时间。经过这段时间后，它将发送假的密钥序列，并期望有效载荷正常运行。为此，您可以使用`--payload-delay`参数。延迟以毫秒为单位。例如，如果您希望用户在前 5 秒内登录，您可以使用以下参数:

–有效负载-延迟 5000

通过利用 RDPDR 初始化期间交换的一些消息，这可以变得更加准确。如果你有兴趣让这项工作做得更好，请看本期。

**选择何时恢复正常活动**

因为没有直接的方法知道控制台何时停止运行，所以您必须告诉 PyRDP 您希望客户端的输入/输出被阻塞多长时间。我们建议您将此设置为运行有效负载的控制台可见的最长时间。换句话说，你期望你的有效载荷完成的时间。要设置有效负载持续时间，您可以使用带有以毫秒为单位的时间量的`**--payload-duration**`参数。例如，如果您预计您的有效负载最多需要 5 秒钟才能完成，您可以使用以下参数:

–有效负载持续时间 5000

这将阻止客户端的输入/输出 5 秒钟，以隐藏控制台并防止干扰。5 秒钟后，输入/输出恢复正常。

**其他 MITM 论点**

运行`**pyrdp-mitm.py --help**`获得参数的完整列表。

**使用 PyRDP 播放器**

使用`**pyrdp-player.py**`运行播放器。

**播放回放文件**

您可以使用菜单打开一个新的重放文件:文件>打开。

您也可以在启动播放器时打开重播文件:

pyrdp-player . py<file1><file2>……</file2></file1>

**监听实时连接**

播放器总是监听实时连接。默认情况下，监听端口为 3000，但可以更改:

pyrdp-player.py -p

**改变监听地址**

默认情况下，播放机只侦听来自本地计算机的连接。我们不建议向其他机器开放播放器。如果你还想改变监听地址，可以用`-b`来做:

pyrdp-player.py -b

**其他玩家争论**

运行`**pyrdp-player.py --help**`获得参数的完整列表。

**使用 PyRDP 证书克隆程序**

PyRDP 证书克隆程序使用现有 RDP 服务器证书的值创建一个全新的 X509 证书。它连接到 RDP 服务器，下载其证书，生成新的私钥，并使用新的私钥替换公钥和证书签名。这可以在 pentest 中使用，例如，如果你试图欺骗一个合法用户通过你的 MITM。使用看起来像合法证书的证书可以提高成功率。

**克隆证书**

您可以使用`pyrdp-clonecert.py`克隆证书:

pyrdp-clone cert . py 192 . 168 . 1 . 10 cert . PEM-o key . PEM

`-o`参数定义用于生成的私钥的路径名。

**使用自定义私钥**

如果您想使用自己的私钥，而不是生成新的私钥:

pyrdp-clone cert . py 192 . 168 . 1 . 10 cert . PEM-I input _ key . PEM

**其他克隆人论据**

运行`**pyrdp-clonecert.py --help**`获得参数的完整列表。

[**Download**](https://github.com/gosecure/pyrdp)