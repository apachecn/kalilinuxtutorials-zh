# hcxdumptool–从 WLAN 设备捕获数据包的小工具

> 原文：<https://kalilinuxtutorials.com/hcxdumptool-wlan-devices/>

Hcxdumptool 是一个小型工具，用于捕获来自 wlan 设备的数据包。在捕获之后，上传“未清除”的 cap [到这里](https://wpa-sec.stanev.org/?submit)，通过使用常见单词列表来查看您的应用程序或客户端是否易受攻击。使用 hcxpcaptool (hcxtools)将 cap 转换为 hccapx 和/或 WPA-PMKID-PBKDF2 hashline (16800 ),并检查 wlan-key 或 plainmasterkey 是否未加密传输。

独立的二进制文件——设计为在安装了 Arch Linux 的 Raspberry Pi 上运行。它应该也能在其他 Linux 系统(笔记本、台式机)和发行版上工作。

**又读[Whatsapp _ Automation:API 集合与运行在 Android 模拟器中的 Whatsapp 交互](https://kalilinuxtutorials.com/whatsapp_automation-android-emulator/)**

## **详细描述**

| 工具 | 描述 |
| --- | --- |
| hcxdumptool | 运行多项测试以确定接入点或客户端是否易受攻击的工具 |
| 皮奥夫 | 通过 GPIO 开关关闭树莓 Pi |

## **Hcxdumptool 编译**

只需运行:

```
make
make install (as super user)
```

或者(带 GPIO 支持–需要硬件模块)

```
make GPIOSUPPORT=on
make GPIOSUPPORT=on install (as super user)
```

## **为 Android 编译**

您需要:

*   Android NDK 安装在您的系统和路径变量
*   该库克隆有所有子模块(**`--recursive`**`**git clone**`中的标志或`**git submodules update**`命令运行)
*   只需运行`**ndk-build**`——一些架构的构建可执行文件应该在 **`libs`** 目录下创建。复制到你的手机上，享受吧。

## **要求**

*   **操作系统:** Arch Linux(严格)，内核> = 4.14(严格)。它应该可以在其他 Linux 系统(笔记本、台式机)和发行版上运行(不支持其他发行版)。不要用内核 4.4 (rt2x00 驱动回归)
*   已安装 libpthread 和 pthread-dev
*   Raspberry Pi:另外安装了 libwiringpi 和 wiring Pi dev(Raspberry Pi GPIO 支持)
*   芯片组必须能够在监控模式下运行(严格按照:ip 和 iw)。推荐:雷凌芯片组(接收机灵敏度好)，rt2x00 驱动(稳定快速)
*   树莓 Pi A，B，A+，B+(推荐:A+ =极低功耗或 B+)，但笔记本和台式机也可以工作。
*   GPIO 硬件模块推荐

## **支持的适配器(严格)**

*   USB ID 148f:7601 雷凌科技公司 MT7601U 无线适配器
*   USB ID 148f:3070 雷凌科技公司 RT2870/RT3070 无线适配器
*   USB ID 148f:5370 雷凌科技公司 RT5370 无线适配器
*   USB ID 0bda:8187 Realtek 半导体公司 RTL8187 无线适配器

USB ID 0 BDA:8189 Realtek Semiconductor corp . RTL 8187 b 无线 802.11g 54Mbps 网络适配器

## **有用的脚本**

| 脚本 | 描述 |
| --- | --- |
| bash_profile | Raspberry Pi 的自动启动(复制到/root/)。bash_profile) |
| pireadcard | 备份 Pi SD 卡 |
| piwritecard | 恢复 Pi SD 卡 |
| makemonnb | 激活监控模式的示例脚本 |
| killmonnb | 停用监控模式的示例脚本 |

## **硬件模块–参见文档 gpiowait.odg** 

*   如果 hcxdumptool 成功启动，LED 闪烁 5 次
*   如果一切正常，LED 每 5 秒闪烁一次
*   按住按钮至少 5 秒以上，直到 LED 亮起(如果 hcxdumptool 终止，LED 亮起)
*   绿色 ACT LED 闪烁 10 次
*   Raspberry Pi 已关闭，可以断开电源
*   不要同时使用 hcxdumptool 和 hcxpioff！

## **硬件模式–参见文档 gpiowait.odg (hcxpioff)**

*   如果 hcxpioff 成功启动，LED 每 10 秒闪烁 2 次
*   按住按钮至少 10 秒以上，直到 LED 亮起(hcxpioff 将安全关闭 Raspberry Pi)
*   绿色 ACT LED 闪烁 10 次
*   Raspberry Pi 已关闭，可以断开电源
*   不要同时使用 hcxdumptool 或 hcxpioff！

## **警告**

您必须仅在您有权限的网络上使用 hcxdumptool，因为

*   hcxdumptool 能够阻止完整的 wlan 流量
*   hcxdumptool 能够从访问点捕获 PMKID(从一个访问点只需要一个 pm kid)
*   hcxdumptool 能够捕获来自未连接客户端的握手(仅需要来自客户端的一个 M2)
*   hcxdumptool 能够在 2.4GHz 上捕获来自 5GHz 客户端的握手(仅需要来自客户端的一个 M2)
*   hcxdumptool 能够捕获扩展的 EAPOL (RADIUS、GSM-SIM、WPS)
*   hcxdumptool 能够从 wlan 流量中捕获密码
*   hcxdumptool 能够从 wlan 流量中捕获 plainmasterkeys
*   hcxdumptool 能够从 wlan 流量中捕获用户名和身份

[![https://github.com/Nekmo/dirhunt](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/ZerBea/hcxdumptool)