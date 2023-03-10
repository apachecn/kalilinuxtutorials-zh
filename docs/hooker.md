# hooker:Android 应用程序的自动动态分析

> 原文：<https://kalilinuxtutorials.com/hooker/>

Hooker 是一家开源公司，致力于 Android 应用程序的动态分析。这个项目提供了不同的设备和应用程序，可以用来捕获和调整目标应用程序发出的任何 API 调用。

它使用 Android 底层系统来捕获这些调用，并汇总所有相关数据(参数、返回值等)。收集的数据可以放在 ElasticSearch 或 JSON 记录中。

另外给出了 python 脚本的安排，以自动执行检查来收集由一组应用程序进行的任何 API 调用。

#### **也读[insta gram-Py–Python 脚本来蛮力攻击](http://kalilinuxtutorials.com/instagram-py-python-script/)**

Android-Hooker 是一个基于底层系统的想法证明。这意味着，如果基板没有准确地引入你的设备，胡克无法工作。在这种情况下，创造者们有效地在 Android 和 4.2 版本的小工具上引入了 Substrate。

## **胡克技术描述**

Hooker 由多个模块组成:

1.  **APK 仪器**是一个 Android 应用程序，必须在分析之前安装在 Android 设备上(例如，仿真器)。
2.  **hooker_xp** 是一个 python 工具，可以用来控制 android 设备，并触发其上应用程序的安装和激励。
3.  **hooker_analysis** 是一个 python 脚本，可用于收集存储在 elasticsearch 数据库中的结果。
4.  **tools/APK-contact generator**是一款 Android 应用，由 hooker_xp 自动安装在 Android 设备上，注入虚假的联系信息。
5.  tools/apk_retriever 是一个 Python 工具，可以用来从各种在线公开 Android 市场下载 apk。
6.  tools/emulatorCreator 是一个脚本集合，可以用来准备一个仿真器。

[![](img/a51de913dc60eee505c4a68651ee8e4d.png)](https://github.com/AndroidHooker/hooker)