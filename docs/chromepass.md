# Chromepass:黑掉 Chrome 保存的密码

> 原文：<https://kalilinuxtutorials.com/chromepass/>

[![Chromepass : Hacking Chrome Saved Passwords](img/72be1d794c1e479a067f6f06cf2e92da.png "Chromepass : Hacking Chrome Saved Passwords")](https://1.bp.blogspot.com/-F56sBhRADYU/XpM2xuIfOdI/AAAAAAAAF4w/jxTNReUwKbI_SkAC8lAwynMjH32XbjaagCLcBGAsYHQ/s1600/Hacking%2BChrome.png)

**Chromepass** 是一个基于 python 的控制台应用程序，可生成具有以下特性的 windows 可执行文件:

*   解密 chrome 保存的密码
*   远程发送包含登录/密码组合的文件(电子邮件或反向 http)
*   自定义图标
*   完全无法被反病毒引擎检测到

**AV 检测**

由于这种编码方式，它目前完全没有被发现。以下是使用各种网站执行扫描的一些链接

*   [病毒全面扫描](https://www.virustotal.com/gui/file/b4780b4712f494dc9856ff23ce29415445ad5eea3776663da28c556645f0e202/detection)(0/68)2019 年 9 月 30 日
    *   这是一个教育项目，所以分发(或缺少分发)不是问题，因此使用 VirusTotal
*   [反扫描](https://antiscan.me/scan/new/result?id=kmpsMNccfuRJ) (0/26) 24-09-2019
*   [杂交分析](https://www.hybrid-analysis.com/sample/9ca69d2c60f0db6c09e9959b6f9c8bfdf66ddbe2e28f9f7539fd2856b62315c0)全部清除(CrowdStrike Falcon、MetaDefender 和 virus total)2019 年 9 月 24 日

**入门**

**依赖关系&需求**

这是一个非常简单的应用程序，只使用了:

*   [Python](https://www.python.org/downloads/)–仅在 3.7.4 上测试，但应该可以在 3.6+上运行

**安装**

*   Chromepass 需要 [Python](https://www.python.org/downloads/) 3.6+才能运行。
*   安装依赖项:

**>CD chromepass
>pip install-r requirements . txt**

如果出现任何错误，请确保您运行在正确的环境中(如果适用)，并且您拥有 python 3.6+(最好是 3.7.4)。如果错误仍然存在，请尝试:

**> python -m pip 安装–升级 pip
> python -m pip 安装–r 需求. txt**

**用途**

Chromepass 非常简单。从跑步开始:

**>python create _ server . py**

它会要求您在两个选项中进行选择:

*   **(1)通过电子邮件** *【待定】*
    *   这将要求您输入一个 ***电子邮件*** 地址和一个 ***密码***
    *   然后它会问你是否希望发送到另一个地址或你自己
    *   接下来，询问您是否想要显示错误消息。这是一条假消息，如果启用，受害者在密码被转移后打开可执行文件时会出现这条消息。
    *   然后你可以写下你自己的信息或者留空
    *   你完了！等待可执行文件生成，然后它就准备好了。
*   **(2)途经 client.exe***【目前推荐】*
    *   首先要求你输入一个 ***IP 地址*** 进行反向连接。这是属于攻击者的地址。可以是 ***本地 IP 地址*** 或 ***远程 IP 地址*** 。如果选择远程地址，[端口转发](https://www.noip.com/support/knowledgebase/general-port-forwarding-guide/)需要到位。
    *   然后询问您是否想要显示错误消息。这是一条假消息，如果启用，受害者在密码被转移后打开可执行文件时会出现这条消息。
    *   然后你可以写下你自己的信息或者留空
    *   你完了！等待生成可执行文件，然后它就准备好了。
    *   **client.exe**必须在 **server_ip.exe** 之前启动。 **server_ip.exe** 是受害者收到的文件。

**注意:**要设置自定义图标，请将 ***icon.ico*** 替换为相同名称和格式的所需图标。

**也读作-[Frida-Fuzzer:用于 API 内存模糊化的实验性模糊化器](https://kalilinuxtutorials.com/frida-fuzzer/)**

**待办事项**

*   发送受害者的实时精确位置(**完成，发布下一次更新**
*   还偷火狐密码(**完成，发布下一次更新**)
*   安装允许远程控制受害者计算机的后门的选项(**完成，发布下一个更新**
*   支持更多的电子邮件提供商(**进行中**)
*   也从其他程序中窃取密码，比如钥匙链(**进行中**)
*   添加夜间模式(**进行中**)

**错误、bug&功能请求**

如果您发现错误或缺陷，请将其作为问题报告。如果您希望对某项功能或改进提出建议，请在问题页面中报告。

创建问题时，请遵循显示的模板。

**了解更多信息**

想要进入一个充满有抱负的计算机安全专家的社区，从完全的初学者到经验丰富的老手，请加入我们的 Discord 服务器: [WhiteHat Hacking](https://discord.gg/beczNYP)

如果你想联系我，你可以通过: [marionascimento@itsec.us](mailto:marionascimento@itsec.us)

**免责声明**

我不负责你用提供的信息和代码做什么。这仅用于专业或教育目的。