# EDRHunt:扫描 Windows 上安装的 edr 和 AVs

> 原文：<https://kalilinuxtutorials.com/edrhunt/>

[![](img/8436291281dec90cdec46cc0edf08856.png)](https://blogger.googleusercontent.com/img/a/AVvXsEj1yD3sxtw8ppEk3AY3DJIW1UpcIVlwOguOUGyVWBTGV0Ds8ihM6HZG6CAmcMmgePxHsuD_Vw31XUVDOxkkb0Sy5l5D6oUv5BJsjFqvUiyaNE1ySnSeuPV-2KZa3dApQDgXVH2eBYcacfIP378TimKaKAmv5yPzOnPr20qXcwA4PHHY1Ff_dxvvfbkm=s728)

**EDRHunt** 扫描 Windows 服务、驱动程序、进程和注册表，寻找已安装的 edr(端点检测和响应)。阅读更多关于 EDRHunt 的信息

## 安装

*   二进制的
    *   从版本部分下载最新版本。版本是为 windows/amd64 构建的。
*   去
    *   需要在系统上安装 Go。在 Go1.17+上测试。
    *   `**go install github.com/FourCoreLabs/EDRHunt/cmd/EDRHunt@master**`

## 用法

*   查找已安装的 EDRs

**$。\EDRHunt.exe 扫描
【EDR】
检测到 EDR: Windows Defender
检测到 EDR:卡巴斯基安全**

扫描一切

**$。\EDRHunt.exe all
在用户模式下运行，请上报给管理员以了解更多详细信息。
扫描进程、服务、驱动、注册表……
【进程】
可疑进程名称:MsMpEng.exe
描述:MsMpEng.exe
字幕:MsMpEng.exe
二进制:
ProcessID: 6764
父进程:1148
进程 CmdLine :
文件元数据:
匹配关键字:【msmpeng】
可疑进程名称:NisSrv.exe
描述:NisSrv.exe
字幕:NisSrv.exe
二进制:** 

查找匹配 EDR 关键字的驱动程序

**/*/_ \/_ \/_ \///////|//////////////////|/////
//*///*//*， */_*////*///|///*/*/*/|/*|/*//*/_ _ _ _ _ _*/*/|*//_/
四核实验室(https://fourcore.vision) |版本:1.1
在用户模式下运行，请向管理员升级以了解更多详细信息。
【驱动】
可疑驱动模块:WdFilter.sys
驱动文件 path:c:\ windows \ system32 \ DRIVERS \ wd \ wd filter . sys
驱动文件元数据:
产品名称:微软 Windows 操作系统
original filename:wd filter . sys
internal filename:wd filter
公司名称:微软公司
文件描述:微软反恶意软件文件系统过滤驱动
产品版本:4.18.2109 保留所有权利。
合法商标:
匹配关键字:【反恶意软件】
可疑驱动模块:hvsifltr.sys
驱动文件路径:c:\ windows \ system32 \ drivers \ hvsifltr . sys
驱动文件元数据:
产品名称:微软 Windows 操作系统
original filename:hvsifltr . sys . mui
internal filename:hvsifltr . sys
公司名称:微软公司
文件描述保留所有权利。
legal trade mark:
匹配关键字:[defender]
可疑驱动模块:WdNisDrv.sys
驱动文件路径:c:\ windows \ system32 \ drivers \ wd \ wdnisdrv . sys
驱动文件元数据:
产品名称:微软 Windows 操作系统
original filename:wdnisdrv . sys
internal filename:wdnisdrv . sys
公司名称:微软公司
文件描述:Windows Defender 保留所有权利。
legal trade mark:
匹配关键字:[defender]
……**

## 侦查

EDR 检测目前可用

*   Windows Defender
*   卡巴斯基安全
*   赛门铁克安全性
*   Crowdstrike 安全
*   迈克菲安全
*   资金安全
*   炭黑
*   SentinelOne
*   火眼
*   弹性 EDR

更多将很快添加

[**Download**](https://github.com/FourCoreLabs/EDRHunt)