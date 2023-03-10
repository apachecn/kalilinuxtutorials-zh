# Sniffer:蓝牙 5 和 4 的嗅探器。x 乐

> 原文：<https://kalilinuxtutorials.com/sniffle/>

[![Sniffle : A Sniffer For Bluetooth 5 And 4.X LE](img/3b6b5639c7a6f80b7c71e7293bda7eb6.png "Sniffle : A Sniffer For Bluetooth 5 And 4.X LE")](https://1.bp.blogspot.com/-VRgITaA6eco/YQOSd3FfzWI/AAAAAAAAKTM/cR6icI5SbH4kpzvIufKL4mSC2_sqT-92gCLcBGAsYHQ/s718/download.png)

**sniffe 是一款使用 TI CC1352/CC26x2 硬件的蓝牙 5 和 4.x (LE)的嗅探器。**

抽噎有很多有用的功能，包括:

*   支持 BT5/4.2 扩展长度广告和数据包
*   支持 BT5 通道选择算法#1 和#2
*   支持所有 BT5 PHY 模式(常规 1M、2M 和编码模式)
*   支持只嗅探广告和忽略连接
*   支持频道映射、连接参数和 PHY 改变操作
*   支持通过 MAC 地址和 RSSI 过滤广告
*   支持 BT5 扩展广告(非定期)
*   支持使用单个嗅探器从目标 MAC 上捕获所有三个主要广告渠道上的广告。这使得连接检测的可靠性比其他大多数只嗅探一个广告频道的嗅探器高出近 3 倍。
*   用 Python 编写的易于扩展的主机端软件
*   PCAP 出口兼容 Ubertooth

**先决条件**

*   TI CC26x2R 启动板:https://www.ti.com/tool/LAUNCHXL-CC26X2R1
*   或 TI CC2652RB 启动板:https://www.ti.com/tool/LP-CC2652RB
*   或 TI CC1352R Launchpad 板:https://www.ti.com/tool/LAUNCHXL-CC1352R1
*   或 TI CC1352P1 Launchpad 板:https://www.ti.com/tool/LAUNCHXL-CC1352P
*   GNU ARM 嵌入式工具链:https://developer . ARM . com/open-source/GNU-tool chain/GNU-RM/downloads
*   TI cc26x 2 SDK 5 . 10 . 00 . 48:https://www.ti.com/tool/download/SIMPLELINK-CC13X2-26X2-SDK
*   TI DSLite 编程器软件:见下文
*   Python 3.5+安装了 PySerial

如果您不想为固件设置构建环境，您可以使用 UniFlash/DSLite 刷新预构建的固件二进制文件。预构建的固件二进制文件附加到该项目的 GitHub releases 选项卡上的版本中。当使用预构建的固件时，一定要使用对应于 release 标签的 Python 代码，而不是 master，以避免与 master 分支后面的固件的兼容性问题。

注意:应该可以通过最小的修改来编译 Sniffle，使其在 CC1352P Launchpad 板上运行，但是我还没有尝试过。

**安装 GCC**

通过各种 Linux 发行版的包管理器提供的`**arm-none-eabi-gcc**`通常缺少一些头文件，或者需要对链接器配置进行一些更改。为了减少麻烦，我建议使用上面链接的 ARM GCC。您可以下载并解压缩预构建的可执行文件。

**安装 TI SDK**

TI SDK 是作为一个可执行的二进制文件提供的，一旦您接受许可协议，它就会提取大量源代码。在 Linux 和 Mac 上，默认的安装目录在 **`~/ti/`里面。**这工作得很好，我的 makefiles 需要这个路径，所以我建议使用这里的默认值。这同样适用于 TI SysConfig 工具。

一旦提取了 SDK，您将需要编辑一个 makefile 来匹配您的构建环境。在`**~/ti/simplelink_cc13x2_26x2_sdk_5_10_00_48**`(或者安装 SDK 的地方)有一个名为`**imports.mak**`的 makefile。这里需要设置的唯一路径是 GCC、XDC 和 SysConfig。我们不需要 CCS 编译器。请参见下面的差异示例，并适应您的安装环境。

**diff–git a/imports . mak b/imports . mak
index d 815 a4e 94..731d 49419 100644
—a/imports . mak
+++ b/imports . mak
@ @-18，14 +18，14 @@
#将使用每个非空*_ARMCOMPILER cgtool 进行编译。
#
-XDC _ 安装 _ 目录？=/home/username/ti/xdc tools _ 3 _ 62 _ 00 _ 08 _ core
-sys config _ TOOL？=/home/username/ti/CCS 1030/CCS/utils/sys config _ 1 . 8 . 0/sys config _ CLI . sh
+XDC _ 安装 _ 目录？= $(HOME)/ti/xdc tools _ 3 _ 62 _ 00 _ 08 _ core
+sys config _ TOOL？= $(HOME)/ti/sys config _ 1 . 8 . 0/sys config _ CLI . sh
freer tos _ INSTALL _ DIR？=/home/username/freer tosv 10 . 2 . 1
CCS _ arm compiler？=/home/username/ti/CCS 1030/CCS/tools/compiler/ti-CGT-arm _ 20 . 2 . 4 . lts
TIC lang _ arm compiler？=/home/username/ti/CCS 1030/CCS/tools/compiler/1 . 2 . 1 . STS
-GCC _ arm compiler？=/home/username/ti/CCS 1030/CCS/tools/compiler/9.2019 . Q4 . major
+GCC _ arm compiler？= $(HOME)/arm _ tools/gcc-arm-none-eabi-9-2019-Q4-major
# Linux 上不支持 IAR 编译器
# IAR_ARMCOMPILER？=**

**获取 DSLite**

DSLite 是 TI 用于 XDS110 调试器的命令行编程和调试服务器工具。CC26xx 和 CC13xx 启动板都包括 XDS110 调试器。不幸的是，TI 不提供独立的命令行 DSLite 下载。获得 DSLite 最简单的方法是安装 TI 的 UniFlash。它适用于 Linux、Mac 和 Windows。DSLite 可执行文件将位于相对于 UniFlash 安装目录的`**deskdb/content/TICloudAgent/linux/ccs_base/DebugServer/bin/DSLite**`位置。在 Linux 上，默认的 UniFlash 安装目录在**T1 里面。**

您应该将 DSLite 可执行文件目录放在您的`**$PATH**`中。

**建筑安装**

一旦 GCC、DSLite 和 SDK 安装完毕并投入运行，构建 Sniffle 就应该很简单了。只需导航到 **`fw`** 目录并运行`**make**`。如果你没有将 SDK 安装到默认目录，你可能需要在 makefile 中编辑`**SIMPLELINK_SDK_INSTALL_DIR**`。

要使用 DSLite 在(插上电源的)CC26x2 Launchpad 上安装 Sniffle，请在`**fw**`目录下运行`**make load**`。您还可以使用 UniFlash GUI 刷新编译后的`**sniffle.out**`二进制文件。

如果构建或安装在某个版本的 Launchpad 或高于 CC26x2R 的版本上，则必须指定 **`PLATFORM=xxx`，**作为 make 的参数，或者在调用 make 之前将其定义为环境变量。`**PLATFORM**`支持的值有`**CC2642R1F**`、`**CC2652R1F**`、`**CC1352R1F3**`、`**CC2652RB1F**`和`**CC1352P1F3**`。在为不同的平台构建之前，一定要执行 **`make clean`** 。

**嗅探器用法**

**【skhan @ serpent python _ CLI】$。/sniff _ receiver . py–help
用法:sniff _ receiver . py[-H][-s SERPORT][-c { 37，38，39 }][-p][-r RSSI][-m MAC]
[-I IRK][-a][-e][-H][-l][-Q][-Q PRELOAD][-o OUTPUT]
sniff BLE5 Sniffer
可选参数:
-h，–help 显示此帮助 –rssi RSSI 按最小 RSSI 过滤数据包
-m MAC，–MAC MAC MAC 按广告商 MAC 过滤数据包
-i IRK，–IRK IRK 按广告商 IRK 过滤数据包
-a，–adv 仅嗅探广告，不跟踪连接
-e，–ext adv 捕获 BT5 扩展(辅助)广告
-H，–Hop Hop 扩展模式下的主广告频道
-l，–远程使用远程(编码)PHY 进行主广告
-q**

Launchpad 板上的 XDS110 调试器创建两个串行端口。在 Linux 上，它们通常被命名为 **`ttyACM0`** 和`**ttyACM1**`。创建的两个串行端口中的第一个用于与 Sniffle 通信。默认情况下，Python CLI 使用`**/dev/ttyACM0**`进行通信，但是如果您没有在 Linux 上运行或者连接了额外的 USB CDC-ACM 设备，您可能需要使用`**-s**`命令行选项来覆盖它。

对于`**-r**` (RSSI 滤波器)选项，如果嗅探器非常接近或几乎接触到传输设备，值-40 往往工作良好。RSSI 滤波器对于在繁忙的射频环境中忽略不相关的广告非常有用。RSSI 滤波器仅在捕获广告时有效，因为您总是希望捕获被跟踪的连接的数据信道流量。当 MAC 过滤处于活动状态时，您可能不想使用 RSSI 过滤器，因为当 RSSI 太低时，您可能会丢失来自感兴趣的 MAC 地址的广告。

为了跟随广告并进行可靠的连接嗅探，您需要用`**-m**`选项设置一个 MAC 过滤器。您应该指定外围设备的 MAC 地址，而不是中心设备。要确定要嗅探哪个 MAC 地址，您可以运行带有 RSSI 滤波的嗅探器，同时将嗅探器放在目标附近。这将向您显示来自目标设备的广告，包括其 MAC 地址。应该注意的是，许多 BLE 设备用随机的 MAC 地址而不是写在标签上的“真正的”固定 MAC 地址来做广告。

为了方便起见，MAC 过滤器有一个特殊的模式，即使用`**-m top**`调用脚本，而不是使用 MAC 地址调用 **`-m`** 。在这种模式下，嗅探器将锁定它看到的第一个通过 RSSI 过滤器的广告商 MAC 地址。因此，`**-m top**`模式应该总是与 RSSI 过滤器一起使用，以避免锁定到虚假的 MAC 地址。一旦嗅探器锁定了一个 MAC 地址，嗅探接收器脚本将自动禁用 RSSI 过滤器(除非使用了`**-e**`选项)。

大多数新的 BLE 设备使用可解析私有地址(RPA ),而不是固定的静态或公有地址。虽然您可以为特定 RPA 设置 MAC 筛选器，但设备会定期更改其 RPA。如果身份解析密钥(IRK)已知，则可以解析 RPA(与特定设备相关联)。如果提供了 IRK，则 Sniffle 支持自动 RPA 解析。这避免了每当 RPA 改变时就需要不断更新 MAC 过滤器。您可以使用`**-i**`选项为抽泣指定一个 IRKIRK 应以十六进制格式提供，最高有效字节(MSB)在前。指定一个 IRK 允许 Sniffle 像使用 MAC 过滤器一样与广告商进行频道跳转。基于 IRK 的 MAC 过滤特性 **( `-i`** )与静态 MAC 过滤特性 **( `-m`** )互斥。

要在蓝牙 5 扩展广告中启用以下辅助指针，请启用`**-e**`选项。为了提高扩展广告捕捉的性能和可靠性，即使设置了 MAC 过滤器，此选项也会禁用主广告频道上的跳转。如果您不确定是通过传统广告还是扩展广告来建立连接，您可以将`**-H**`标志与`**-e**`一起启用，以通过传统广告执行主频道跳跃，并计划收听扩展广告辅助数据包。当组合`**-e**`和`**-H**`时，与仅在主要(传统)或次要(扩展)广告信道上跳跃相比，连接检测的可靠性可能会降低。

要在主要广告渠道上嗅探远程 PHY，请指定`**-l**`选项。注意，在远程模式中不支持主广告频道之间的跳跃，因为所有远程广告都使用 BT5 扩展机制。在扩展机制下，所有三个主信道上的辅助指针都指向同一个辅助分组，因此主信道之间的跳跃是不必要的。

为了在连接后不在屏幕上打印空数据包，使用`**-q**`标志。这使得实时观察有意义的通信变得更容易，但是当连接不稳定或丢失时，可能会变得模糊。

对于加密的连接，即使加密密钥未知，Sniffle 也支持检测连接参数更新，并尝试测量新参数。但是，如果您知道加密连接参数更新中预期的新连接间隔和即时增量，您可以使用`**--preload**` / `**-Q**`选项来指定它们，以提高性能/可靠性。预期的 Interval:DeltaInstant 对应以冒号分隔的整数形式提供。Interval 是一个整数，表示 1.25 ms 的倍数(如 LL_CONNECTION_UPDATE_IND 中所定义)。DeltaInstant 是在传输连接更新包和应用新参数之间的连接事件的数量。根据蓝牙规范对主设备的要求，DeltaInstant 必须大于或等于 6。如果需要多个加密参数更新，您可以提供多个参数对，用逗号分隔(例如`**6:7,39:8**`)。

如果由于某种原因，嗅探器固件锁定，并拒绝捕捉任何流量，即使过滤器禁用，你应该重置嗅探器 MCU。在 Launchpad 板上，重置按钮位于微型 USB 端口旁边。

**扫描仪用法**

**用法:Scanner . py[-h][-s SERPORT][-c { 37，38，39}][-r RSSI][-l]
Sniffer ble Sniffer
可选参数:
-h，–help 显示此帮助消息并退出
-s SERPORT，–SERPORT SERPORT
Sniffer 串口名称
-c {37，38，39 }，–adv chan { 37，38，39}** 

扫描仪命令行参数的工作方式与嗅探器相同。scanner 实用程序的目的是收集附近设备广告的列表，并主动发出对被观察设备的扫描请求，而不像 sniffer 实用程序那样需要大量快速滚动的数据。硬件/固件将进入主动扫描模式，其中它将报告接收到的广告，发出对可扫描广告的扫描请求，并报告接收到的扫描响应。scanner 实用程序将只记录和报告一次观察到的 MAC 地址，而不会显示垃圾邮件。一旦你捕获完广告，按 Ctrl-C 停止扫描并报告结果。扫描仪将显示最后一个广告，并扫描每个目标的响应。扫描结果将按 RSSI 降序排列。

**用法举例**

嗅探 38 频道上的所有广告，忽略 RSSI < -50，即使看到 CONNECT_REQs 也保持在广告频道上。

**。/sniff _ receiver . py-c 38-r-50-a**

嗅探来自 MAC 12:34:56:78:9A:BC 的广告，即使看到 CONNECT_REQs 也保持在广告频道上，将广告保存到`**data1.pcap**`。

**。/sniff _ receiver . py-m 12:34:56:78:9A:BC-a-o data1 . pcap**

嗅探 RSSI >= -40 的第一个 MAC 地址的广告和连接。一旦锁定了一个 MAC 地址，RSSI 过滤器将自动禁用。将捕获的数据保存到 **`data2.pcap`。**

**。/sniff _ receiver . py-m top-r-40-o data 2 . pcap**

用 big endian IRK 4 E0 bea 5355866 be 38 ef 0 AC 2 E3 f 0 ebc 22 嗅探来自外设的广告和连接。预加载两个预期的加密连接参数更新；第一个间隔为 6，在嗅探器观察到加密的 LL_CONNECTION_UPDATE_IND 之后的瞬间发生 6 个连接事件。第二次预期的加密连接更新的时间间隔为 39，DeltaInstant 也为 6。

**。/sniff _ receiver . py-I 4 E0 bea 5355866 be 38 ef 0 AC 2 E3 f 0 ebc 22-Q 6:6，39:6**

嗅探来自附近(RSSI >= -55)设备的 BT5 扩展广告和连接。

**。/sniff_receiver.py -r -55 -e**

从具有指定 MAC 地址的设备中嗅探旧的和扩展的广告和连接。将捕获的数据保存到 **`data3.pcap`。**

**。/sniff _ receiver . py-eH-m 12:34:56:78:9A:BC-o data 3 . pcap**

使用信道 38 上的远程主 PHY 监听扩展广告和连接。

**。/sniff_receiver.py -le -c 38**

积极扫描 39 频道上 RSSI 大于-50 的广告。

**。/scanner.py -c 39 -r -50**

**获得 IRK**

如果你有一个根 Android 手机，你可以在 Bluedroid 配置文件中找到 irk(和 ltk)。在 Android 8.1 上，这个位于 **`/data/misc/bluedroid/bt_config.conf`** 。`**LE_LOCAL_KEY_IRK**`指定 Android 设备自己的 IRK，文件中每个绑定设备的`**LE_KEY_PID**`的前 16 个字节表示绑定设备的 IRK。注意，存储在这个文件中的键是小端的，所以这个文件中键的字节顺序需要颠倒。比如 little endian IRK 22 BC 0 e 3f 2 eacf 08 ee 36 b 865553 ea 0 B4 e 在用`**-i**`选项传递给 Sniffle 时需要改成 4 E0 bea 5355866 be 38 ef 0 AC 2 E3 f 0 ebc 22(big endian)。

[**Download**](https://github.com/nccgroup/Sniffle)