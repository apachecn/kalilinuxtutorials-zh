# Introspy-iOS:运行时分析 iOS 应用程序的安全工具

> 原文：<https://kalilinuxtutorials.com/introspy-ios-security-profiling/>

Introspy-iOS 是一个黑盒工具，帮助理解 iOS 应用程序在运行时正在做什么，并帮助识别潜在的安全问题。这是 Introspy-iOS 跟踪程序的存储库。

tracer 可以安装在越狱设备上，以挂钩和记录设备上运行的应用程序调用的安全敏感的 iOS APIs。该工具记录相关 API 调用的详细信息，包括参数和返回值，并将它们保存在数据库中。此外，呼叫也被发送到控制台进行实时分析。

然后，可以将数据库提供给 Introspy-Analyzer，这是一个 Python 脚本，用于生成 HTML 报告，其中包含记录的函数调用列表以及影响应用程序的潜在漏洞列表。

**又读[Ua-tester——用户代理 WAF、IDS/IPS、重定向测试的工具](https://kalilinuxtutorials.com/ua-tester/)**

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
dpkg -r com.isecpartners.introspy
```

## **构建 Introspy-iOS**

大多数用户应该只是下载并安装预编译的 Debian 包。然而，如果你想修改库的功能，你必须自己构建 Debian 包。

构建需要 Theos 套件，关于如何安装 Theos 的一般说明，[点击这里](https://github.com/theos/theos/wiki/Installation.)

您还必须在您的环境中设置$THEOS 变量，并将其导出，以便在您运行它时让会看到它的值

```
export THEOS=/absolute/path/to/theos
export PATH=$THEOS/bin:$PATH
```

然后，可以使用以下方法构建包:

```
make package
```

一旦您成功地创建了 Debian 软件包，您就可以使用 Theos 自动安装软件包，并通过在 THEOS_DEVICE_IP 环境变量中指定设备的 IP 地址来重新启动设备:

```
export THEOS_DEVICE_IP=192.168.1.127
make install
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/iSECPartners/Introspy-iOS)