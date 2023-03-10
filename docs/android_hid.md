# Android_Hid:使用 Android 作为对抗另一个 Android 设备的橡皮鸭

> 原文：<https://kalilinuxtutorials.com/android_hid/>

[![Android_Hid : Use Android As Rubber Ducky Against Another Android Device](img/5851309951e19af58224eaffac0ae27c.png "Android_Hid : Use Android As Rubber Ducky Against Another Android Device")](https://1.bp.blogspot.com/-vwtuWoPejaE/YG4nktLSDwI/AAAAAAAAIrM/7uS4f3kHD4kp1F0dCHetzcry58eH9-3aACLcBGAsYHQ/s728/Android%25281%2529.png)

**android_Hid** 是一款被 Android 当做橡皮鸭来对付目标 Android 设备或 PC 的工具。

**使用 Android 的 HID 攻击**

用安卓做橡皮鸭对抗安卓或 Windows。这不是一个新技术，只是一个演示如何使用 Android 而不是橡胶 ducky 执行 HID 攻击。对于目标 Android 设备，没有必要进行 root，启用 ADB/USB 调试并授权设备，因为攻击者的智能手机表现为连接的键盘。

hid _ attack–脚本包含针对目标 Android 设备执行(键入)的定制命令 hid _ PC–脚本包含针对目标 Windows 10 执行(键入)的定制命令

**如何防止这种情况在 Android 上发生？**

*   使用您自己的适配器为您的智能手机充电
*   使用重要的 PIN 或密码锁屏保护
*   使用移动安全软件来检测和阻止有效载荷的发射

**如何防止这种情况在 PC 上发生？**

*   不要让任何人在你的电脑上给他们的智能手机充电
*   使用将检测 Metasploit 有效负载的安全软件
*   USB 避孕套应该有帮助

**概念验证**

*   **安卓:**【https://youtu.be/aOWr6rWhsIs】T2PC:[https://youtu.be/PJbqZm73MOc](https://youtu.be/PJbqZm73MOc)

**先决条件**

*   具有 HID 内核支持的根 Android(例如 NetHunter ROM)
*   OTG 电缆公司

**脚本信息**

这是自定义脚本，可能不适用于您的测试用例场景。因此，你必须摆弄发送到目标设备的按键。网站与我的测试有效负载不再活跃。所有可能的密钥列表可以在下面的链接中找到。

**执行命令**

**bash hid_attack bash hid_pc**

**如何 flash 自定义 ROM 带 HID 支持**？

[https://github.com/pelya/android-keyboard-gadget](https://github.com/pelya/android-keyboard-gadget)

**使用 Android 作为 HID 的强力 pin 码**

[https://github.com/urbanadventurer/Android-PIN-Bruteforce](https://github.com/urbanadventurer/Android-PIN-Bruteforce)

**所有按键列表**

[https://github . com/an bud/DroidDucky/blob/master/DroidDucky . sh](https://github.com/anbud/DroidDucky/blob/master/droidducky.sh)

[**Download**](https://github.com/androidmalware/android_hid)