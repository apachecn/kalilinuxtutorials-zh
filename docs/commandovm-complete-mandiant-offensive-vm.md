# CommandoVM:完整的 Mandiant 进攻虚拟机(突击虚拟机)，第一个完整的基于 Windows 的渗透测试虚拟机分发

> 原文：<https://kalilinuxtutorials.com/commandovm-complete-mandiant-offensive-vm/>

[![CommandoVM : Complete Mandiant Offensive VM (Commando VM), The First Full Windows-Based Penetration Testing Virtual Machine Distribution](img/382a718d3cf09f2944ce04aed25a42c6.png "CommandoVM : Complete Mandiant Offensive VM (Commando VM), The First Full Windows-Based Penetration Testing Virtual Machine Distribution")](https://1.bp.blogspot.com/-0rNbLNa0dW0/XSjFsDrLBqI/AAAAAAAABUk/MKAZyNC1QtQ3_pgGXXYfuacIgcApYZQfgCLcBGAs/s1600/Commando%25281%2529.png)

欢迎使用 commando VM——一个完全定制的、基于 Windows 的安全发行版，用于渗透测试和 red teaming。

**【安装脚本】**

**要求**

*   Windows 7 服务包 1 或 Windows 10
*   60 GB 硬盘
*   2 GB 内存

**推荐**

*   Windows 10
*   80+ GB 硬盘
*   4+ GB 内存
*   2 个网络适配器
*   为虚拟机启用虚拟化支持

**指令**

1.  创建并配置新的 Windows 虚拟机

*   确保虚拟机完全更新。您可能需要检查更新，重新启动，并再次检查，直到没有任何剩余
*   给你的机器拍个快照！
*   在新配置的机器上下载并复制`**install.ps1**`。
*   以管理员身份打开 PowerShell
*   通过运行以下命令启用脚本执行:
    *   `**Set-ExecutionPolicy Unrestricted**`
*   最后，执行安装程序脚本，如下所示:
    *   `**.\install.ps1**`
    *   您也可以将您的密码作为参数传递:`**.\install.ps1 -password <password>**`

该脚本将设置 Boxstarter 环境，并继续下载和安装 Commando VM 环境。为了在安装过程中自动重启主机，系统会提示您输入管理员密码。如果没有设置密码，出现提示时按 enter 也可以。

**安装新的软件包**

突击队虚拟机使用 Chocolatey Windows 包管理器。安装新的软件包很容易。例如，以管理员身份输入以下命令，在您的系统上部署 Github Desktop:

**cinst github**

**保持最新**

键入以下命令，将所有软件包更新到最新版本:

**杯尽**

**也可阅读-[who nix:隐私保护、在线匿名、匿名操作系统](https://kalilinuxtutorials.com/whonix-privacy-protection/)**

**安装工具**

**活动目录工具**

*   远程服务器管理工具(RSAT)
*   SQL Server 命令行实用工具
*   系统内部

**命令&控制**

*   契约
*   PoshC2
*   WM 植入物
*   WMIOps

**开发者工具**

*   Dep
*   饭桶
*   去
*   Java 语言(一种计算机语言，尤用于创建网站)
*   Python 2
*   Python 3(默认)
*   红宝石
*   Ruby 开发包
*   Visual Studio 2017 构建工具(Windows 10)
*   Visual Studio 代码

**闪避**

*   请结账
*   半伪装
*   防守队员检查
*   DotNetToJScript
*   调用-摇篮工匠
*   Invoke-DOSfuscation
*   调用混淆
*   Invoke-Phant0m
*   不是 PowerShell (nps)
*   PS >攻击
*   圣歌
*   Pafishmacro
*   无电源外壳
*   powershell
*   星际战斗机

**剥削**

*   改编剧本
*   API 监视器
*   CrackMapExec
*   CrackMapExecWin
*   潮湿
*   EvilClippy
*   Exchange-AD-Privesc
*   FuzzySec 的 PowerShell 套件
*   模糊证券的夏普套件
*   生成宏
*   幽灵背包
    *   Rubeus
    *   安全 Katz
    *   安全带
    *   SharpDPAPI
    *   夏普 Dump
    *   夏普烤肉
    *   急剧上升
    *   夏普米
*   GoFetch
*   冲击
*   Invoke-ACLPwn
*   调用-DCOM
*   Invoke-PSImage
*   Invoke-PowerThIEf
*   多汁的土豆
*   用于 Windows 的 Kali 二进制文件
*   好彩
*   大温
*   Metasploit
*   Unikod3r 先生的 RedTeamPowershellScripts 脚本
*   NetshHelperBeacon
*   霓裳
*   奥尔卡
*   PSReflect
*   powerturk
*   powergrip
*   PowerSploit
*   PowerUpSQL
*   专用交换机
*   罗特滕波塔通
*   尺子
*   SharpClipHistory
*   夏普 ExchangePriv
*   夏普赛克
*   SpoolSample
*   夏普斯洛特
*   UACME
*   impact et-示例-windows
*   vssown
*   伏尔甘

**信息收集**

*   ADACLScanner
*   sdexplorer
*   ADOffline
*   奥雷孔
*   大猎犬
*   dnsrecon
*   FOCA
*   Get-ReconInfo
*   GoBuster
*   身材高挑
*   网络掠夺者
*   Nmap
*   权力观
    *   包括开发部门
*   分享猎犬
*   夏普维尤
*   假脱机扫描仪
*   沃森

**网络工具**

*   Citrix 接收器
*   OpenVPN
*   Proxycap
*   油灰
*   用于远程联接服务的标准协议或者实现此协议的软件(可为动词)
*   VMWare Horizon 客户端
*   VMWare vSphere 客户端
*   VNC 观察报
*   WinSCP
*   风泵
*   Wireshark

**密码攻击**

*   ASREPRoast
*   信用忍者
*   DomainPasswordSpray
*   DSInternals
*   get-laps 密码
*   哈希卡特
*   内心独白
*   猛烈抨击
*   调用-TheHash
*   凯睿
*   小偷
*   LAPSToolkit
*   邮件狙击手
*   米米卡茨
*   米米基滕斯
*   RiskySPN
*   会话 Gopher

**逆向工程**

*   DNSpy(间谍)
*   闪光牙线
*   伊尔斯皮
*   试映
*   Windbg
*   x64dbg

**公用事业**

*   7zip
*   Adobe Reader
*   你帮了我
*   Cmder
*   网络咖啡馆
*   资源管理器套件
*   花边
*   绿色快照
*   Hashcheck
*   Hexchat
*   HxD
*   Keepass
*   mobaxterm(mobaxterm)
*   Mozilla 雷鸟
*   Neo4j 社区版
*   记事本++
*   洋泾浜
*   流程黑客 2
*   SQLite 数据库浏览器
*   Screentogif
*   外壳代码启动器
*   崇高文本 3
*   乌龟
*   VLC 媒体播放器
*   我赢了
*   yEd 图形工具

**漏洞分析**

*   广告控制路径
*   出口评估
*   群组 2
*   NtdsAudit
*   PwndPasswordsNTLM
*   他破产了

**网络应用**

*   打嗝组曲
*   游手好闲的人
*   火狐浏览器
*   OWASP Zap
*   子域-暴力
*   Wfuzz

**词表**

*   模糊数据库
*   有效载荷所有事物
*   秘书
*   可能单词表
*   机器人被丢弃

**变更日志:**

1.3–2019 年 6 月 28 日

*   https://github.com/breenmachine/RottenPotatoNG# 63
*   补充多汁的土豆[https://github.com/ohpe/juicy-potato](https://github.com/ohpe/juicy-potato)# 63、#64
*   补充沃森[https://github.com/rasta-mouse/Watson](https://github.com/rasta-mouse/Watson)# 64
*   增加了 PwndPasswordsNTLM[https://github.com/JacksonVD/PwnedPasswordsNTLM](https://github.com/JacksonVD/PwnedPasswordsNTLM)# 67
*   https://github.com/JacksonVD/PwnedPasswordsNTLM# 71 补充 FOCA
*   补充火神[https://github.com/praetorian-code/vulcan](https://github.com/praetorian-code/vulcan)
*   增加了夏普利历史[https://github.com/mwrlabs/SharpClipHistory](https://github.com/mwrlabs/SharpClipHistory)
*   增加了网虫[https://github.com/NytroRST/NetRipper](https://github.com/NytroRST/NetRipper)
*   新增机器人消失[https://github.com/danielmiessler/RobotsDisallowed](https://github.com/danielmiessler/RobotsDisallowed)
*   增加了可能的词汇列表[https://github.com/berzerk0/Probable-Wordlists](https://github.com/berzerk0/Probable-Wordlists)
*   增加了夏普斯洛特[https://github.com/cobbr/SharpSploit](https://github.com/cobbr/SharpSploit)
*   已更改 WinRM 配置#65
*   未加固的 UNC 文件路径#68
*   修正了圣约#61、#76 的安装问题

1.2–2019 年 5 月 31 日

*   添加了建议的硬件设置#20、#17
*   添加了域名密码祈祷[https://github.com/dafthack/DomainPasswordSpray](https://github.com/dafthack/DomainPasswordSpray)# 2
*   增加了捉鬼敢死队[https://github.com/OJ/gobuster](https://github.com/OJ/gobuster)# 39
*   增加了 Wfuzz[https://github.com/xmendez/wfuzz](https://github.com/xmendez/wfuzz)# 40
*   添加了记事本++ 30
*   为 Notepad++添加了 TextFX 插件
*   增加了浏览器套件(CFF 浏览器)

1.1–2019 年 4 月 30 日

*   增加了广告控制路径[https://github.com/ANSSI-FR/AD-control-paths/releases](https://github.com/ANSSI-FR/AD-control-paths/releases)
*   增加了防守检查[https://github.com/matterpreter/DefenderCheck](https://github.com/matterpreter/DefenderCheck)
*   增加了 DNS recon[https://github.com/darkoperator/dnsrecon](https://github.com/darkoperator/dnsrecon)
*   https://github.com/outflanknl/EvilClippy
*   增加了 NTDs audit[https://github.com/Dionach/NtdsAudit](https://github.com/Dionach/NtdsAudit)
*   增加了夏普赛克[https://github.com/anthemtotheego/SharpExec](https://github.com/anthemtotheego/SharpExec)
*   增加了子域-暴力[https://github.com/visualbasic6/subdomain-bruteforce](https://github.com/visualbasic6/subdomain-bruteforce)
*   修复了路径问题#18
*   在$Home\Pictures 中添加了透明背景的突击队标志
*   将 Firefox 固定到任务栏
*   修复了 Readme #42/#43 中的拼写错误
*   添加了 Ruby 和 Ruby Devkit #1
*   将 Rubeus 包更新到当前版本(1.4.2) #31

2019 年 4 月 10 日

*   将缺少的“seclists.fireeye”包添加到 packages.json #38

2019 年 3 月 31 日

*   使用 https 而不是 http 安装 boxstarter #10

[Download](https://github.com/fireeye/commando-vm)