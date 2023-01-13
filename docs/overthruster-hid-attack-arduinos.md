# 推翻者–Arduinos 的 HID 攻击有效载荷生成器

> 原文：<https://kalilinuxtutorials.com/overthruster-hid-attack-arduinos/>

当用作 HID 攻击时，OverThruster 是一个为 Arduinos 生成草图的工具。它是围绕装有 ATMEGA32U4 芯片的设备设计的，如 CJMCU-BEETLE，或 ebay 和 aliexpress 上出现的新 lily go“bad USB”设备，这些设备看起来像 USB 棒，但包含 Arduino。我这样写是因为其他几个类似的工具没有像 UAC 绕过选项或通知气泡选项那样多的定制选项。

我想创建一个可以快速生成自定义有效负载的东西，并且除了标准 Python 库和 Arduino IDE 之外，不需要安装任何额外的东西。我写这个也是为了更好地学习 Python。这是我第一次发布任何东西，所以预计会有问题。

**也读作[evil ginx–MITM 攻击框架为钓鱼凭证&会话 cookie](https://kalilinuxtutorials.com/evilginx-mitm-attack/)**

## **使用推翻者**

*   首先启动 OverThruster.py
*   选择目标的操作系统
*   选择特定的有效负载
*   填写所需的设置
*   生成。ino 文件
*   打开。Arduino IDE 中的 ino 文件
*   将草图刷新到您的 Arduino 设备

## **备注**

*   在闪烁有效载荷之后，Arduino IDE 将断开 Arduino，然后它将自动重新连接，并传送有效载荷。准备好字符突然被输入到屏幕上；我建议打开记事本或类似的东西，当你闪现草图的时候保持专注
*   推翻者目前放弃了。ino 文件和 Metasploit。rc 文件，所以在那里寻找它们。
*   对于 UAC 旁路技术，时机是关键。旧设备将以较慢的速度打开具有管理员权限的终端，因此您可能需要调整草图中 BypassUAC 函数的延迟()
*   这只是开始。更多的有效载荷、功能、选项和附加功能即将推出。
*   如果你有什么要补充的，请投稿。

## **要求**

*   支持键盘模拟的 Arduino
*   Python 2.7 (Python 3 版本即将推出)
*   Arduino IDE
*   尼科胡德的 HID:[https://github.com/NicoHood/HID/](https://github.com/NicoHood/HID/)(这可以直接从 Arduino IDE 的菜单中安装:草图- >。包含库- >管理库并搜索“HID-Project”)

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/RedLectroid/OverThruster)