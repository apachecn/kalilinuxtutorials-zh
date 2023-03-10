# 易受攻击的 Android 应用程序

> 原文：<https://kalilinuxtutorials.com/injuredandroid/>

[![InjuredAndroid : A Vulnerable Android Application](img/0922da70e28e385c8f858688f356517c.png "InjuredAndroid : A Vulnerable Android Application")](https://1.bp.blogspot.com/-t0CXNcNCBDM/XkHx-A3myPI/AAAAAAAAE4k/Cjg3VR_ogGk76ibUFG_jh_pUlwCOPSNKACLcBGAsYHQ/s1600/Android.png)

**InjuredAndroid** 是一个易受攻击的 Android 应用程序，其 ctf 示例基于 bug bounty 发现、利用概念和纯创意。

**物理设备的设置**

*   从 Github 下载 injuredandroid.apk
*   在 Android 测试手机上启用 USB 调试。
*   用 usb 线连接你的手机和电脑。
*   通过亚行安装。`**adb install injuredandroid.apk**`。注意:您需要使用。apk 文件或位于同一目录中。

**又读-[NFStream:一个灵活的网络数据分析框架](https://kalilinuxtutorials.com/nfstream/)**

**使用 Android Studio 设置 Android 模拟器**

*   下载 apk 文件。
*   从 Android Studio 启动模拟器(我建议下载一个带有 Google APIs 的模拟器，这样可以启用 root adb)。
*   拖放。模拟器上的 apk 文件，然后将安装 injuredandroid.apk。

**提示和 CTF 概述**

强烈建议对 Android 应用程序进行反编译。

*   XSSTEST 只是为了好玩，并提高人们对网页浏览量如何容易受到 XSS 攻击的认识。
*   登录标志只需要提交的标志。
*   没有提交演示概念的标志将自动在“标志概述”活动中注册。
*   最后两个标志没有注册，因为目前没有远程验证方法(我计划在未来的更新中改变这一点)。这样做是为了防止使用以前的标志方法来跳过利用技术。
*   有一面旗帜带有 Pentesterlab 1 个月礼品钥匙。密钥在被读取后存储在一个自毁注释中，在复制 url 之前不要关闭浏览器标签。
*   右下角的感叹号按钮将为用户提供最多三个提示。

[**Download**](https://github.com/B3nac/InjuredAndroid)