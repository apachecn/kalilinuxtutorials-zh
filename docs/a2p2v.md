# A2P2V:自动攻击路径规划和验证

> 原文：<https://kalilinuxtutorials.com/a2p2v/>

[![A2P2V : Automated Attack Path Planning and Validation](img/7e650ead381a743e0edcae7f05673aa9.png "A2P2V : Automated Attack Path Planning and Validation")](https://1.bp.blogspot.com/-nc9dn39X-Sc/YM4H6lPwWjI/AAAAAAAAJoM/Ok_GpERqRDMEDso63D78QXLjg7Mm_y0nACLcBGAsYHQ/s728/APV%2540%25281%2529.png)

A2P2V(自动攻击路径规划和验证)是一个规划和网络攻击工具，它为用户提供了在给定特定攻击者目标的情况下确定一组分级攻击序列的能力。该工具的目的是简化流程，以便非安全专家可以使用尽可能多的自动化从基本输入中生成清晰、可操作的情报，并生成易于解释的报告。

系统使用已知的网络拓扑和系统漏洞信息来确定所有攻击序列集，以获得攻击者的目标，并输出所选序列所需的步骤(作为 Metasploit 命令)。

系统的输入包括:

*   **初始条件**:对攻击者的知识和当前访问进行建模
*   **攻击者目标**:指示状态变化(例如改变 ICS 系统的温度)或对特定目标主机的远程访问
*   **漏洞信息**:Nessus 或 Nmap 扫描结果或数据定制(CVS)输入格式
*   **网络拓扑**:描述主机信息和网络连接的自定义 XML 格式
*   **能力细节**:一种定制的 XML 格式，描述一组已知的服务和利用，使用 PAP(前置条件、动作和后置条件)模型来指定。

**先决条件**

除了在安装过程中通过 requirements.txt 安装的以外，A2P2V 还有以下先决条件:

*   python >= 3.6
*   Metasploit RPC 守护程序正在运行。(默认配置使用端口 55552，用户名 msf，密码 welcome1)
*   python-tk 已安装

在 Ubuntu 上安装 python tk(假设 python 3.9)

**sudo 安装 python3.9-tk**

启动 Metasploit RPC 守护程序

**msfrpcd-P welcome 1-S-U MSF-a 127 . 0 . 0 . 1-f-P 55552**

**安装**

建议在虚拟环境中安装。

首先创建一个 venvs 目录:

**mkdir $HOME/。venvs/**

创建虚拟环境:

**python3 -m venv。venvs/a2 p2v〔t1〕**

激活虚拟环境:

**来源。venvs/a2p2v/bin/activate**

安装:

**cd a2p2v/
pip 安装**

**负载能力定义**

第一次运行该工具时，需要导入功能定义。例如，要加载提供的默认功能定义:

**a2p2v–import db lab _ config/capabilities . XML**

**入门:系统目标**

系统在计划模式下运行，使用以下命令行参数

**$ a2p2v–计划**

将显示以下选项:

| 树# | 得分 | 啤酒花 | 最终功能选项 | 目标 |
| --- | --- | --- | --- | --- |
| Zero | Six point one seven | GW(1)>HMI(4)>OPC(4)>PLC(1) | 辅助/扫描仪/scada/modbusclient | 更改温度 |
| one | Six point one seven | GW(1)>HMI(4)>用户 2(4)>PLC(1) | 辅助/扫描仪/scada/modbusclient | 更改温度 |

**选择要执行的攻击树(或任何其他要退出的值):**

可以在 **reports/** 目录中找到详细的报告和相应的攻击树集。

**入门:单主机目标**

该工具还可以针对单个目标运行，前提是与该目标有网络连接。

通过在命令行参数中指定目标，系统以单主机模式运行:

**a2p2v–目标用户 1**

选择中显示了所有已知漏洞的列表。您可以选择使用特定的漏洞，也可以选择所有的漏洞。

| 树# | 得分 | 能力 |
| --- | --- | --- |
| Zero | Eight point four | exploit/windows/SMB/ms17 _ 010 _ 永恒之蓝 |
| —– | —– | ————————————————– |
| one | Eight point four | exploit/windows/SMB/ms17 _ 010 _ PS exec |
| —– | —– | ————————————————– |
| Two | Eight point four | exploit/windows/SMB/ms10 _ 061 _ spoolss |
| —– | —– | ————————————————– |
| three | Eight point two | exploit/windows/RDP/CVE _ 2019 _ 0708 _ blue keep _ rce |

**选择要执行的功能，选择“a”表示全部，或者选择要跳过的任何其他值:a**

相应的报告类似于为系统用例生成的报告。

[**Download**](https://github.com/pentest-a2p2v/pentest-a2p2v-core#installation)