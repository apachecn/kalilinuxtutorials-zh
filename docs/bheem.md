# Bheem:用于执行各种工具和侦察过程的工具

> 原文：<https://kalilinuxtutorials.com/bheem/>

[![Bheem : Tool To Carry Out Various Tools And Recon Process](img/aaf29351c9b58eafbcf3d614081fa3b9.png "Bheem : Tool To Carry Out Various Tools And Recon Process")](https://1.bp.blogspot.com/-hNPKWB1VE6U/X-J9JuA5b-I/AAAAAAAAIMY/bzrGQ64y8j80VJX2tIsOTqv3K6r84Nr_gCLcBGAsYHQ/s728/h%25281%2529.png)

Project **Bheem** 是一个简单的小型 bash 脚本集合，它反复运行以实现各种工具和 recon process &以一种有组织的方式存储输出。

这个项目最初是为个人使用的 Recon 自动化而创建的，从来没有打算公开，因为它没有什么奇特之处，但由于社区的要求，项目 Bheem 现在是公开的。

请尽可能地改进它。这里面没有什么秘方，只是用 bash 脚本编写的一组命令和现有工具，用于简单的侦察自动化。

Bheem 项目支持@harshbothra_ 的基于范围的侦察方法中的一种侦察方法。目前，该工具支持执行以下侦察:

*   小范围(范围内的单个 URL):执行有限的重新搜索&当范围内只有几个 URL 时很有用
*   中等范围(范围内为*.target.com):执行侦察以枚举更多资产，给你更多攻击选项。
*   大范围(范围内的一切) :执行几乎所有可能的侦察向量，从子域枚举到模糊化。

像端口扫描这样的一些特性在当前版本中可能无法工作，一些新发布的工具也可能会被遗漏。我们正在升级该工具，但请随意分叉、升级并提出拉取请求(确保工具不会损坏)。

**先决条件**

*   确保安装了“Go”的最新版本，并且正确设置了路径。

**安装**

*   克隆存储库
*   运行以下脚本来安装必要的工具:`**sh install.sh**`
*   `**arsenal**`目录包含一组用于自动化 Bheem 的小脚本。授予此目录中脚本的可执行权限。
*   导航到 **`~/arsenal`** 目录，只需运行以下命令即可查看 Bheem 中提供的所有支持选项:

`**./Bheem.sh -h**`

*   要在 vps 上使用它对更大的目标集执行侦察，请执行以下命令:

**T0`~/arsenal/Bheem.sh -h`**

*   这将保持`Bheem`运行，即使 SSH 连接被终止或者您关闭了本地机器。

**样品用途**

*   小范围侦察:`**Bheem -t targetfile -S**`
*   中型侦察:`**Bheem -t targetfile -M**`
*   大范围侦察:`**Bheem -t targetfile -L**`

包含执行侦察的域列表。比如:`**targettest.com**`

**旁注**

*   如果你不想使用特定的模块，只需将其注释掉，就不会再使用它了。
*   将以下文件`**/Bheem/arsenal/autoxss.sh**`中的盲 XSS 有效载荷更改为您的。访问[XSS·亨特](https://xsshunter.com/)获得你的盲人 XSS 有效载荷

**使用的工具**

1.  核心
2.  HTTPX
3.  GF 和 GF 模式
4.  秘密发现者
5.  心脏出血单行
6.  积累
7.  子 finder
8.  资产查找器
9.  JSScan
10.  FavFreak
11.  Waybackurls
12.  高斯
13.  平行的
14.  阿斯尼普
15.  目录搜索
16.  身材高挑
17.  subjack
18.  CORS 扫描仪
19.  git-hound
20.  洗牌机
21.  Massdns

~要添加的其他在线工具。

**PR 注释**

*   如果有任何 GO 版本/路径相关的问题，请不要为此创建 PR。
*   请为功能请求创建一个 PR。
*   如果`install.sh`中有任何缺失的部分，请为其创建一个 PR。
*   对于与特定工具相关的问题，如 Bheem 使用的`X`工具安装不成功，请不要为其创建 PR。因为这个问题需要向特定的工具所有者提出。

**未来计划/开发中**

*   添加目录枚举
*   添加子域强制
*   添加 HTTP 同步扫描器
*   添加易受攻击的软件和漏洞利用建议者
*   为 CORS、CRLF 和其他矢量添加单线扫描仪
*   添加视觉侦察

**特别感谢**

每一个应用安全社区成员和工具开发者。特别感谢:

*   项目发现(Httpx，Subfinder，chaos，nuclei)
*   OWASP (Amass)
*   Tomnomnom (Assetfinder，Waybackurls，GF)
*   Devansh (FavFreak)
*   心脏放血单排机
*   M4ll0k(秘密探测器)
*   lc (gau)
*   蒂尔逊
*   ffuf (ffuf)
*   sensepost (gowitness)
*   走私者
*   haccer(次杰克)
*   crt.sh(夜叉)

[**Download**](https://github.com/harsh-bothra/Bheem)