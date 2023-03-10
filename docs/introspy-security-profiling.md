# intro spy–针对黑盒 iOS 的安全分析

> 原文：<https://kalilinuxtutorials.com/introspy-security-profiling/>

Introspy 是一个黑盒工具，帮助理解 iOS 应用程序在运行时正在做什么，并帮助识别潜在的安全问题。

## **intro spy 工具介绍**

这是 Introspy-iOS 跟踪程序的存储库。

tracer 可以安装在越狱设备上，以挂钩和记录设备上运行的应用程序调用的安全敏感的 iOS APIs。该工具记录相关 API 调用的详细信息，包括参数和返回值，并将它们保存在数据库中。此外，呼叫也被发送到控制台进行实时分析。

然后，可以将数据库提供给 Introspy-Analyzer，这是一个 Python 脚本，用于生成 HTML 报告，其中包含记录的函数调用列表以及影响应用程序的潜在漏洞列表。

**也读作[BLEAH——一款针对智能设备黑客攻击的 BLE 扫描仪](https://kalilinuxtutorials.com/bleah-ble-scanner-devices-hacking/)**

## **依赖**

追踪器只能在越狱设备上运行。使用 Cydia，确保安装了以下软件包:

*   dpkg
*   Cydia 基质
*   首选加载程序
*   Applist

## **如何安装**

下载 Debian 包并复制到设备上；安装它:

```
scp <package.deb> root@<device_ip>:~
ssh root@<device_ip>
dpkg -i <package.deb>
```

重新喷涂设备:

```
killall -HUP SpringBoard
```

在设备的设置中应该有两个新菜单。“应用程序”菜单允许您选择要分析的应用程序，而“设置”菜单定义要挂钩的 API 组。

最后，杀死并重启你要监控的 App。

## **如何卸载**

```
**dpkg -r com.isecpartners.introspy**
```

## **生成 HTML 报表**

追踪器将把应用程序进行的 API 调用的数据存储在存储在设备上的数据库中(实际上每个应用程序的文件夹中有一个数据库)。这个数据库可以被提供给一个 Python 脚本调用 Introspy-Analyzer，以便生成 HTML 报告，这使得查看跟踪器收集的数据变得容易得多。该脚本还将分析和标记危险的 API 调用，以便于识别 iOS 应用程序中的漏洞。

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/iSECPartners/Introspy-iOS#dependencies)