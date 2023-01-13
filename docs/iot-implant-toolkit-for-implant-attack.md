# 物联网植入:物联网设备植入攻击工具包

> 原文：<https://kalilinuxtutorials.com/iot-implant-toolkit-for-implant-attack/>

**物联网植入** Toolkit 是一个有用的工具框架，用于物联网设备的恶意软件植入研究。这是一个工具包，包括固件修改，串口调试，软件分析和稳定的间谍客户端的基本软件工具。

IoT-Implant-Toolkit 具有易于使用和可扩展的类似外壳的环境，是一种一站式工具包，简化了物联网恶意软件植入的复杂程序。

在我们的研究中，我们已经成功地用 IoT-Implant-Toolkit 在智能音箱、摄像头、行车记录仪、移动翻译机等八个设备中植入了木马。

**也可阅读-[Unicorn-Bios:Unicorn 引擎的基本 Bios 仿真器](https://kalilinuxtutorials.com/unicorn-bios/)**

**如何使用**？

**安装**

确保你已经安装了 git、python3 和 setuptools。
音频处理和播放，要安装 alsa(Linux 内置)、sox 和 ffplay。在 ubuntu18.04 上:

**【sudo apt 安装 Sox ffmpeg】**

从我们的 Github 下载源代码:

**$ git 克隆 https://github.com/arthastang/IoT-Implant-Toolkit.git**

设置环境并安装依赖项:

**$ CD IoT-Implant-Toolkit/
$ python 3 setup . py 安装**

**跑**

运行工具包:

$ python 3-B IoT-Implant-Toolkit . py
命令:
List–列出所有工具
Run–运行特定工具
Exit–Exit
【Implant-Toolkit】>

支持三个命令:
list:列出所有插件
run:用“运行[插件][参数]”
运行特定插件:exit

**特色**

每个软件工具就像一个插件，可以很容易地添加到框架中。

有四个类别的十多个插件，包括串口调试，固件打包和解包，软件分析和植入间谍程序的主题。

**插件列表**

我们框架中的现有插件:

| 种类 | 工具 | 描述 | 参考 |
| --- | --- | --- | --- |
| 串口调试 | pyserial | 调制解调器控制和终端仿真程序 | [https://github.com/pyserial/pyserial](https://github.com/pyserial/pyserial) |
| 串口调试 | baudrate.py | 找到正确的波特率 | [https://github . com/devttys 0/波特率](https://github.com/devttys0/baudrate) |
| 固件打包和解包 | mksquashfs | 创建并提取 Squashfs 文件系统 | [https://github.com/plougher/squashfs-tools](https://github.com/plougher/squashfs-tools) |
| 固件打包和解包 | mkbootimg_tools | 为 Android 解包并重新打包 boot.img | [https://github.com/xiaolu/mkbootimg_tools](https://github.com/xiaolu/mkbootimg_tools) |
| 固件打包和解包 | cramfs | 创建 cramfs 文件系统 | [https://sourceforge.net/projects/cramfs/files/cramfs/1.1/](https://sourceforge.net/projects/cramfs/files/cramfs/1.1/) |
| 固件打包和解包 | 增加 | 为 Android system.img&data.img 挂载和卸载 ext4 文件系统 | 在 github 上 |
| 软件分析 | setools-android | 带策略注入的 Android setools | [https://github.com/xmikos/setools-android](https://github.com/xmikos/setools-android) |
| 软件分析 | 交叉编译 | arm 的交叉编译工具链 | 在我们的 Github 上 |
| 软件分析 | odex 打开包装 | Android 版 Odex to smali | 在 Github 上 |
| 二元植入物 | 间谍客户端和服务器 | 一个稳定的间谍客户端和服务器，源和预建箱 | 在 Github 上 |
| 二元植入物 | 降噪工具 | 用于音频处理降噪工具 | 在 Github 上 |

**创建新插件**

代码结构:

–IoT-Implant _ toolkit . py #启动脚本
–outputs/#输出的默认文件夹
–toolkit/
|—core/
|—Basic/#基本插件类定义
|—CLI/#类 Shell CLI 定义
|—tool list/#自动更新工具插件列表
|—Plugins/
|—固件/#固件修改插件
|—Implant/#生成间谍程序插件
|—串口/#串口调试插件【T8

创建[newplugin]。py 在相应的文件夹(类别)中，并定义 init 属性以向 IoT-Implant-Toolkit 添加新插件。框架会在启动时自动检测新插件。

**其他工具**

**五金工具**

恶意软件植入研究的基本硬件工具。参见 HardwareTools/中的图片。

| 名字 | 描述 |
| --- | --- |
| 烙铁 | 焊接工具 |
| 钎料丝 | 焊接工具 |
| 焊膏 | 焊接工具 |
| 焊料芯 | 焊接工具 |
| 热风枪 | 焊接工具 |
| 重新打包工具 | 重新打包工具 |
| usb 转 ttl | 调试/控制台电缆 |
| 杜邦电线 | 电线 |
| EPROM 刻录机编程器 | 燃烧器编程器 |

**其他有用的软件工具**

由于时间限制，我们没有添加更多的插件。

下面的图表是工具，不适合我们的框架，但可能有用。

我们希望 IoT-Implant-Tookit 将成为恶意软件植入的基本工具包。

| 种类 | 工具 | 描述 | 参考 |
| --- | --- | --- | --- |
| 固件分析 | 滨河路 | 一个快速、易用的工具，用于分析、逆向工程和提取固件映像 | [https://github.com/ReFirmLabs/binwalk](https://github.com/ReFirmLabs/binwalk) |
| 固件修改 | 固件模块套件 | 用于提取和重建基于 linux 的固件映像的脚本和实用程序的集合 | [https://github.com/rampageX/firmware-mod-kit](https://github.com/rampageX/firmware-mod-kit) |
| 交叉编译程序 | buildroot | arm mips powerpc 交叉编译器 | [https://buildroot.org/](https://buildroot.org/) |

[**Download**](https://github.com/arthastang/IoT-Implant-Toolkit)