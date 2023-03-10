# Qvm-Create-Windows-Qube:快速、轻松、安全地运行新的 Windows Qubes

> 原文：<https://kalilinuxtutorials.com/qvm-create-windows-qube-spin-up-new-windows-qubes-quickly-effortlessly-and-securely/>

[![Qvm-Create-Windows-Qube : Spin Up New Windows Qubes Quickly, Effortlessly And Securely](img/b5e682a73302034fa092f21eb0090800.png "Qvm-Create-Windows-Qube : Spin Up New Windows Qubes Quickly, Effortlessly And Securely")](https://1.bp.blogspot.com/-aeS2mRI6rmg/YLsi0lfJG-I/AAAAAAAAJUg/iwqYkVkZ3uMvHy6Fr1P84UeZ-3RceJe5ACLcBGAsYHQ/s728/logo%2B%25281%2529.png)

qvm-create-windows-qube 是一款使用 [Qubes Windows Tools (QWT)](https://www.qubes-os.org/doc/windows-tools/) 驱动程序快速方便地安装全新 Windows [qubes](https://www.qubes-os.org/) 的工具。它正式支持 Windows 7，8.1 和 10 以及 Windows Server 2008 R2，2012 R2，2016 和 2019。

该项目强调正确性、安全性，并在整个过程中将 Windows 视为不可信的客户操作系统。它还具有其他功能，例如使用 [Chocolatey](https://chocolatey.org/) 自动安装包括 Firefox、Office 365、Notepad++和 Visual Studio 等软件包。

**安装**

*   通过打开链接，右键单击并选择“将[页面]另存为…”来下载[安装脚本](https://raw.githubusercontent.com/elliotkillick/qvm-create-windows-qube/master/install.sh)
*   在 Dom0 中运行以下命令，将 **`install.sh`** 复制到 Dom0 中:
    *   `**qvm-run -p --filter-escape-chars --no-color-output <qube_script_is_located_on> "cat '/home/user/Downloads/install.sh'" > install.sh**`
*   检查`**install.sh**`的代码以确保其完整性
    *   启用以上转义字符过滤更安全；当输出是文件时，qvm-run 默认禁用它
*   运行`**chmod +x install.sh && ./install.sh**`
    *   注意，这将在全局默认 **`TemplateVM`，**中安装软件包，默认为`**fedora-XX**`
*   查看产生的代码`**qvm-create-windows-qube.sh**`

Qubes R4.1 将提供更加简化和安全的打包安装流程。

**用途**

**用法:。/qvm-create-windows-qube . sh[options]-I-a
-h，–help
-c，–计算具有所需给定基本名称的 Windows qubes 的数量
-t，–template 使此 qube 成为模板 vm 而不是独立的 VM
-n，–NetVM NetVM for Windows 使用
-s，–无缝启用无缝模式在重新启动后持续运行
-o，–优化通过禁用 qube 的不必要功能来优化 Windows
-y，–spyless 配置 Windows 遥测 –软件包以逗号分隔的要预安装的软件包列表(请参见 https://chocolatey.org/packages 的可用软件包)
-i，–iso Windows media 自动安装和设置
-a，–Windows 安装的答案文件设置**

**下载 Windows ISO**

`**windows-media/isos/download-windows.sh**`脚本(`windows-mgmt` 中的**)安全下载官方 Windows ISO 供 **`qvm-create-windows-qube`使用。****

**创建 Windows 虚拟机**

#### Windows 10

`**./qvm-create-windows-qube.sh -n sys-firewall -oyp firefox,notepadplusplus,office365proplus -i win10x64.iso -a win10x64-pro.xml work-win10**`

`**./qvm-create-windows-qube.sh -n sys-firewall -oyp steam -i win10x64.iso -a win10x64-pro.xml game-console**`

#### Windows Server 2019

`**./qvm-create-windows-qube.sh -n sys-firewall -oy -i win2019-eval.iso -a win2019-datacenter-eval.xml fs-win2019**`

#### Windows 10 LTSC

*   微软官方提供的更稳定、更精简、更安全、更私密的 Windows 10 版本

`**./qvm-create-windows-qube.sh -n sys-firewall -oyp firefox,notepadplusplus,office365proplus -i win10x64-ltsc-eval.iso -a win10x64-ltsc-eval.xml work-win10**`

`**./qvm-create-windows-qube.sh -n sys-whonix -oyw -i win10x64-ltsc-eval.iso -a win10x64-ltsc-eval.xml anon-win10**`

#### Windows 7

*   不推荐，因为微软不再支持 Windows 7，但是，如果需要无缝窗口集成或动态调整大小，这是 Qubes GUI 驱动程序(在 Qubes Windows 工具中)支持的唯一桌面操作系统
*   有关详细信息，请参阅下面的安全>窗口>咨询部分

`**./qvm-create-windows-qube.sh -n sys-firewall -soyp firefox,notepadplusplus,office365proplus -i win7x64-ultimate.iso -a win7x64-ultimate.xml work-win7**`

**安全**

qvm-create-windows-qube 是“相当安全的”,因为 [Qubes](https://www.qubes-os.org/) 会拥有它。

*   有气隙吗
*   整个 Windows qube 设置过程是在空气间隙中完成的
    *   在 Windows qube 安装的最后安装软件包有一个例外
*   通过不让 Dom0 shell 脚本解析来自不受信任的`windows-mgmt` qube 的任何输出，消除了整个类的命令注入漏洞
    *   只有退出代码被`qvm-run`通过；没有变量
    *   这也减轻了另一个 shell shock Bash 漏洞的影响
*   Windows ISOs 的下载通过实施以下措施而变得安全:
    *   iso 是直接从微软控制的`microsoft.com`子域名下载的
    *   HTTPS TLS 1.2/1.3
    *   HTTP 公钥锁定(HPKP)将网站的证书列入白名单，而不是依赖证书颁发机构(CAs)
        *   Qubes 旨在[“不信任基础设施”](https://www.qubes-os.org/faq/#what-does-it-mean-to-distrust-the-infrastructure)
        *   记住，`transport security = encryption * authentication`(这允许最大限度的认证)
    *   下载后对文件的 SHA-256 验证
*   Windows 一直被视为不受信任的客户操作系统
*   维护人员的所有提交总是用他们各自的 PGP 密钥签名
    *   如果签署停止，假设妥协
    *   当前维护者 1: [埃利奥特·基里克](https://github.com/elliotkillick)
        *   PGP 密钥:018 f B9 de 6 DFA 13FB 18FB 5552 F9 B9 0d 44 F83D d5f 2
    *   当前维护者 2: [弗雷德里克·皮耶雷](https://github.com/fepitre)(无密钥库账户)
        *   PGP 密钥:9fa 6 4b 92 F95E 706 b F28E 2c a6 4840 10 b5 CD C5 76e 2
        *   最关心的是 Qubes R4.1 支持
            *   查看`release4.1`分支和[qubes-mgmt-salt-windows-mgmt](https://github.com/fepitre/qubes-mgmt-salt-windows-mgmt)
*   Windows ISO 处理中的任何理论漏洞(例如文件系统解析中的漏洞)或应答文件的影响仅限于`windows-mgmt`