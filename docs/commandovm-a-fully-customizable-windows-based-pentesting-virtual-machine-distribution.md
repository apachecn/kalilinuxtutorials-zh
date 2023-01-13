# CommandoVM:一个完全可定制的基于 Windows 的 Pentesting 虚拟机发行版

> 原文：<https://kalilinuxtutorials.com/commandovm-a-fully-customizable-windows-based-pentesting-virtual-machine-distribution/>

[![CommandoVM : A Fully Customizable Windows-Based Pentesting Virtual Machine Distribution](img/01bbd17d4e0a77724b5f4e369dd172ed.png "CommandoVM : A Fully Customizable Windows-Based Pentesting Virtual Machine Distribution")](https://1.bp.blogspot.com/-PJRFGkR34Kk/XUyYdhLlxII/AAAAAAAABzo/SdX0ANMpoX4YqSDAcjTJbrckZgagqk5SwCLcBGAs/s1600/Commando%25281%2529.png)

欢迎使用 CommandoVM，这是一个完全可定制的基于 Windows 的安全发行版，用于渗透测试和 red teaming。

**安装**

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
    *   需要 KALI 或 DOCKER

**指令**

**标准安装**

1.  创建并配置新的 Windows 虚拟机

*   确保虚拟机完全更新。您可能需要检查更新，重新启动，并再次检查，直到没有任何剩余
*   给你的机器拍个快照！
*   在新配置的机器上下载并复制`install.ps1`。
*   以管理员身份打开 PowerShell
*   通过运行以下命令启用脚本执行:
    *   `Set-ExecutionPolicy Unrestricted`
*   最后，执行安装程序脚本，如下所示:
    *   `.\install.ps1`
    *   您也可以将您的密码作为参数传递:`.\install.ps1 -password <password>`

该脚本将设置 Boxstarter 环境，并继续下载和安装 Commando VM 环境。为了在安装过程中自动重启主机，系统会提示您输入管理员密码。如果没有设置密码，出现提示时按 enter 也可以。

**也可以理解为-[SET:trusted sec](https://kalilinuxtutorials.com/set-social-engineer-toolkit-trustedsec/)T3 的社会工程师工具包储存库**

**自定义安装**

*   从[https://github.com/fireeye/commando-vm](https://github.com/fireeye/commando-vm)下载压缩文件到你的下载文件夹。
*   解压缩 zip 文件，并通过删除工具或在“包”部分添加工具来编辑`**${Env:UserProfile}\Downloads\commando-vm-master\commando-vm-master\profile.json**`文件。工具可以从我们的[包列表](https://github.com/fireeye/commando-vm/blob/master/packages.csv)或 chocolatey 库获得。
*   打开管理 PowerShell 窗口并启用脚本执行。`**Set-ExecutionPolicy Unrestricted -f**`
*   切换到解压缩后的项目目录。`**cd ${Env:UserProfile}\Downloads\commando-vm-master\commando-vm-master\**`
*   使用-profile_file 参数执行安装。`**.\install.ps1 -profile_file .\profile.json**`

关于定制安装的更多详细说明，请参见我们的[博客](https://www.fireeye.com/blog/threat-research/2019/08/commando-vm-customization-containers-kali.html)

**安装新的软件包**

突击队虚拟机使用 Chocolatey Windows 包管理器。安装新的软件包很容易。例如，以管理员身份输入以下命令，在您的系统上部署 Github Desktop:

**cinst github**

**保持最新**

键入以下命令，将所有软件包更新到最新版本:

**杯尽**

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

**码头工人**

*   积累
*   蜘蛛脚

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

**信息收集**

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
*   去拿
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

**卡利 Linux**

*   kali-Linux-默认
*   kali-linux-xfce
*   VcXsrv

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

[**Download**](https://github.com/fireeye/commando-vm#installation-install-script)