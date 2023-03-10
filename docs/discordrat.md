# DiscordRAT:完全用 Python 编写的 Discord 远程管理工具

> 原文：<https://kalilinuxtutorials.com/discordrat/>

[![DiscordRAT : Discord Remote Administration Tool Fully Written In Python](img/d685523b3aa0f973204714f65b4b3b51.png "DiscordRAT : Discord Remote Administration Tool Fully Written In Python")](https://1.bp.blogspot.com/-MdlLTFEEtak/XsTFpbwQnFI/AAAAAAAAGXU/qRghGqqnaWoCsNdS0lkfzujzCAPj4vy8wCLcBGAsYHQ/s1600/Discord.png)

**DiscordRAT** 是一个完全用 Python3 编写的 Discord 远程管理工具。这是一只被超过 20 个后开发模块控制的老鼠。

**设置指南**

您首先需要向 Discord developper 门户注册一个 bot，然后将 bot 添加到您想要的服务器。一旦创建了 bot，复制 bot 的令牌并粘贴到第 18 行(如果使用 WithCV ),或者粘贴到第 17 行(如果选择 WithCV)。

现在继续 discord，转到设置，转到外观，滚动到底部，并激活“开发者模式”，现在转到您的 bot 添加的服务器，右键单击您希望 bot 发布的频道，单击复制 ID，最后，如果您使用 NoCV，请将频道 ID(而不是服务器 ID)粘贴到第 97 行的括号中，如果您使用 WithCV，请粘贴到第 67 行的括号中。

安装要求(" pip 3 install-r requirements . txt ")
然后，如果在启动 python 文件或可执行文件后上述步骤成功，它将在服务器上发布一条消息，并生成 uuid，剩下要做的就是发布"！与给定的 uuid 进行“交互”。现在你的机器人应该可以使用了！

**要求**

*   Python3
*   Windows 操作系统

**编译成 exe(可选)**

*   如果你想把机器人编译成 exe，你可以使用 PyInstaller。
    *   在 bot 的目录中执行"**py installer–one file–noconsole DiscordRAT . py "或" python 3-m py installer–one file–noconsole DiscordRAT(NoCV)。py(或 DiscordRAT.py)**
*   如果编译期间出现错误，请尝试导入 discord 模块"**py installer–one file–no console–hidden-import = discord discord rat . py**"

**建议**

如果您在安装 win32api 或其他模块时遇到问题，请尝试将其安装在 python 虚拟环境中。有两个 python 文件，一个有 opencv 和网络摄像头相关模块，另一个没有，这是因为 open-cv 在编译时增加了几十兆字节。exe 文件。

也可阅读-[exe gol:一个卡利轻基地，几乎没有有用的附加工具](https://kalilinuxtutorials.com/exegol/)

**免责声明**

该工具仅用于教育用途，作者不对该工具的任何误用负责。这是我在 github 上的第一个项目，因为这个项目远非完美，我会听取任何批评，只要它是建设性的。

[**Download**](https://github.com/Sp00p64/DiscordRAT)