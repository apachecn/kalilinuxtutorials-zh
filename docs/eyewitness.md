# 目击者:截图网站

> 原文：<https://kalilinuxtutorials.com/eyewitness/>

[![](img/f5c36895982b611945807ae572aad219.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjlPsTOHoGWUFOQiq1t4jXr6Kc-gsl6ok-rejwYcaNGm4kOi23ec70yX48r2gWCs4yIXHZencvScjK9Jgo0TPuyz9DUO9ewVMC6fVC6AHUVrNU4x30CRnkc4LOvap8HuwFiPUtgLH-if4mXByTCdkkCkrqub8oDrdOCAi87gn9ypukJK9zHRHYPh4a4/s728/2%20(1).png)

**witness**旨在获取网站截图，提供一些服务器标题信息，并识别默认凭据(如果已知)。

Witness 被设计为在 Kali Linux 上运行。它会自动检测您用-f 标志给它的文件，要么是每行都有 URL 的文本文件，要么是 nmap xml 输出，要么是 nessus xml 输出。–time out 标志是完全可选的，它允许您在尝试呈现和截屏网页时提供等待的最长时间。

完整的使用指南记录了目击者的特征及其典型使用案例，可在此处获得——https://www . Christopher truncar . com/witness-2-0-release-and-user-guide/

## Windows

FortyNorth Security 已经创建了一个 Windows 客户端(感谢 Matt Grandy (@Matt_Grandy_)在稳定性修复方面的巨大帮助)。您所需要做的就是在本地构建它(或者检查发布版本)，然后提供一个包含您想要扫描的 URL 的文件的路径！Witness 将在您的“AppData\Roaming”目录中生成报告。最新版本的 C # EyeWitness 支持解析和截图 Internet Explorer 和 Chrome 书签，而无需提供 URL 列表。这个版本也足够小，可以通过 Cobalt Strike 的执行装配来交付。

### 设置

*   导航到 CS 目录
*   将 Witness.sln 加载到 Visual Studio
*   转到顶部的构建，然后构建解决方案(如果不需要修改)

### 用法

**EyeWitness.exe–帮助
EyeWitness.exe–书签
EyeWitness.exe-f C:\ Path \ to \ URLs . txt
EyeWitness.exe–file C:\ Path \ to \ URLs . txt–延迟【超时秒数】–压缩**

## Linux 操作系统

###### 支持的 Linux 发行版

*   Kali Linux
*   Debian 7+(至少稳定，正在测试中)(感谢@ themightyshiv)
*   CentOS 7
*   洛基 Linux 8

电子邮件:目击者[@] christophertruncer [dot] com

### 设置

*   导航到 Python/setup 目录
*   运行 setup.sh 脚本

### 用法

**。/witness . py-f filename–超时选项 timeout**

例子

**。/witness-f URLs . txt–web
。/witness-x URLs . XML–超时 8
。/witness . py-f URLs . txt–web–proxy-IP 127 . 0 . 0 . 1–proxy-port 8080–proxy-type socks 5–time out 120**

### 代理使用

通过 socks 代理人代理目击者的最佳指南是由@raikia 编写的，可在此处获得-# 458

要在需要通过代理的情况下从系统安装 Witness，可以使用以下命令(感谢@digininja)。

### 码头工人

现在，您可以在 docker 容器中执行 Witness，并防止您在主机中安装不必要依赖项。

**注意:**执行 *docker run* 用主机中保存你的结果的文件夹路径(**/path/to/results**)
**注意 2:** 如果你想从一个文件中扫描 URL，确保你把它放在 volume 文件夹中(如果你把 *urls.txt* 放在 */path/to/results* 中，那么参数应该是*-f/tmp/witness/*

[**Download**](https://github.com/FortyNorthSecurity/EyeWitness)