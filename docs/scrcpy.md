# Scrcpy:显示和控制您的 Android 设备

> 原文：<https://kalilinuxtutorials.com/scrcpy/>

[![](img/2702bd092d8ba01e6db085c806872b5d.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjVjScM9I8fAxORAEBi2aHq3rzrJ2ItbEcOewp1TcrlpPwBt78yScgBZvumcGwVSNQkmhO2rAV8Sif2EubWJf90HMYmMNKnfGu4WgoOUPlK-bUPCJh5jYtnrOys4Ggzkp2Py4L8D_-UcAYvQ_gsYuNuC1SeGL_BvWObIaOW1aZny0I4Y6VdwyQSfmJ9/s728/scrcpy(1).png)

**Scrcpy** 应用程序通过 TCP/IP 提供通过 USB 或[连接的 Android 设备的显示和控制。它不需要任何 root 访问权限。它可以在 GNU/Linux、Windows 和 macOS 上运行。](https://github.com/Genymobile/scrcpy#tcpip-wireless)

它侧重于:

*   **亮度**:原生，仅显示设备屏幕
*   **性能** : 30~120fps，视设备而定
*   **质量** : 1920×1080 以上
*   **低延迟** : [35~70ms](https://github.com/Genymobile/scrcpy/pull/646)
*   **低启动时间**:约 1 秒显示第一张图像
*   **非侵入性**:安卓设备上什么都没有安装
*   **用户利益**:无需账户、无需广告、无需互联网
*   自由:自由和开源软件

其特点包括:

*   [录制](https://github.com/Genymobile/scrcpy#recording)
*   在 [Android 设备屏幕关闭的情况下镜像](https://github.com/Genymobile/scrcpy#turn-screen-off)
*   [双向复制粘贴](https://github.com/Genymobile/scrcpy#copy-paste)
*   [可配置质量](https://github.com/Genymobile/scrcpy#capture-configuration)
*   Android 设备[作为网络摄像头(V4L2)](https://github.com/Genymobile/scrcpy#v4l2loopback) (仅限 Linux)
*   [物理键盘模拟(HID)](https://github.com/Genymobile/scrcpy#physical-keyboard-simulation-hid)
*   [物理鼠标模拟(HID)](https://github.com/Genymobile/scrcpy#physical-mouse-simulation-hid)
*   [OTG 模式](https://github.com/Genymobile/scrcpy#otg)
*   还有更多…

## 要求

Android 设备至少需要 API 21 (Android 5.0)。

确保[在您的设备上启用 adb 调试](https://developer.android.com/studio/command-line/adb.html#Enabling)。

在一些设备上，你还需要启用[一个额外的选项](https://github.com/Genymobile/scrcpy/issues/70#issuecomment-373286323)来使用键盘和鼠标控制它。

## 获取应用程序

[![Packaging status](img/e197205a70d79dbf542be0efd44c4b12.png)](https://repology.org/project/scrcpy/versions)

### 摘要

*   Linux: `apt install scrcpy`
*   Windows: [下载](https://github.com/Genymobile/scrcpy/releases/download/v1.24/scrcpy-win64-v1.24.zip)
*   苹果电脑:`brew install scrcpy`

从源代码构建:[构建](https://github.com/Genymobile/scrcpy/blob/master/BUILD.md) ( [简化流程](https://github.com/Genymobile/scrcpy/blob/master/BUILD.md#simple))

### Linux

在 Debian 和 Ubuntu 上:

```
apt install scrcpy
```

在 Arch Linux 上:

```
pacman -S scrcpy
```

一个 [Snap](https://en.wikipedia.org/wiki/Snappy_(package_manager)) 包可用: [`scrcpy`](https://snapstats.org/snaps/scrcpy) 。

对于 Fedora，有一个 [COPR](https://fedoraproject.org/wiki/Category:Copr) 包可供选择: [`scrcpy`](https://copr.fedorainfracloud.org/coprs/zeno/scrcpy/) 。

对于 Gentoo，有一个 [Ebuild](https://wiki.gentoo.org/wiki/Ebuild) 可用: [`scrcpy/`](https://github.com/maggu2810/maggu2810-overlay/tree/master/app-mobilephone/scrcpy) 。

也可以[手动构建 app](https://github.com/Genymobile/scrcpy/blob/master/BUILD.md)([简化流程](https://github.com/Genymobile/scrcpy/blob/master/BUILD.md#simple))。

### Windows

对于 Windows，有一个预构建的归档文件，其中包含所有依赖项(包括`adb`):

*   [`scrcpy-win64-v1.24.zip`](https://github.com/Genymobile/scrcpy/releases/download/v1.24/scrcpy-win64-v1.24.zip)
    [SHA-256:`6ccb64cba0a3e75715e85a188daeb4f306a1985f8ce123eba92ba74fc9b27367`]

它也可以在[巧克力店里买到](https://chocolatey.org/):

```
choco install scrcpy
choco install adb    # if you don't have it yet
```

并在[勺](https://scoop.sh):

```
scoop install scrcpy
scoop install adb    # if you don't have it yet
```

也可以[手动构建 app](https://github.com/Genymobile/scrcpy/blob/master/BUILD.md)。

### 苹果电脑

该应用可在[家酿](https://brew.sh/)中获得。只需安装:

```
brew install scrcpy
```

您需要`adb`，可从您的`PATH`访问。如果您还没有:

```
brew install android-platform-tools
```

它也可以在 [MacPorts](https://www.macports.org/) 中获得，它为您设置了`adb`:

```
sudo port install scrcpy
```

也可以[手动构建 app](https://github.com/Genymobile/scrcpy/blob/master/BUILD.md)。

## 跑

将 Android 设备插入您的计算机，然后执行:

```
scrcpy
```

它接受命令行参数，如下所示:

```
scrcpy --help
```

## 特性

### 捕获配置

#### 缩小尺寸

有时，以较低的分辨率镜像 Android 设备有助于提高性能。

要将宽度和高度限制为某个值(例如 1024):

```
scrcpy --max-size=1024
scrcpy -m 1024  # short version
```

计算另一个维度，以便保留 Android 设备的纵横比。这样，1920×1080 的设备将被镜像为 1024×576。

#### 改变比特率

默认比特率是 8 Mbps。要更改视频比特率(例如更改为 2 Mbps):

```
scrcpy --bit-rate=2M
scrcpy -b 2M  # short version
```

#### 限制帧速率

可以限制捕获帧速率:

```
scrcpy --max-fps=15
```

这是从 Android 10 开始正式支持的，但可能在更早的版本上工作。

实际的捕获帧速率可以打印到控制台:

```
scrcpy --print-fps
```

也可以用`MOD` + `i`随时启用或禁用。

#### 农作物

设备屏幕可能会被裁剪为仅反映屏幕的一部分。

例如，这对于仅镜像 Oculus Go 的一只眼睛非常有用:

```
scrcpy --crop=1224:1440:0:0   # 1224x1440 at offset (0,0)
```

如果还指定了`--max-size`，则在裁剪后应用调整大小。

#### 锁定视频方向

要锁定镜像的方向:

```
scrcpy --lock-video-orientation     # initial (current) orientation
scrcpy --lock-video-orientation=0   # natural orientation
scrcpy --lock-video-orientation=1   # 90° counterclockwise
scrcpy --lock-video-orientation=2   # 180°
scrcpy --lock-video-orientation=3   # 90° clockwise
```

这会影响录制方向。

[窗口也可以独立旋转](https://github.com/Genymobile/scrcpy#rotation)。

#### 编码器

一些设备有多个编码器，其中一些可能会导致问题或崩溃。可以选择不同的编码器:

```
scrcpy --encoder=OMX.qcom.video.encoder.avc
```

要列出可用的编码器，可以传递一个无效的编码器名称；该错误将给出可用的编码器:

```
scrcpy --encoder=_
```

### 捕获

#### 录音

镜像时可以录制屏幕:

```
scrcpy --record=file.mp4
scrcpy -r file.mkv
```

要在录制时禁用镜像:

```
scrcpy --no-display --record=file.mp4
scrcpy -Nr file.mkv
# interrupt recording with Ctrl+C
```

“跳过的帧”会被记录下来，即使它们不是实时显示的(出于性能原因)。帧在设备上被打上*时间戳*，因此[数据包延迟变化](https://en.wikipedia.org/wiki/Packet_delay_variation)不会影响录制的文件。

#### v4l2 环回

在 Linux 上，可以将视频流发送到 v4l2 环回设备，这样 Android 设备就可以像网络摄像头一样被任何支持 v4l2 的工具打开。

必须安装模块`v4l2loopback`:

```
sudo apt install v4l2loopback-dkms
```

要创建 v4l2 设备:

```
sudo modprobe v4l2loopback
```

这将在`/dev/videoN`中创建一个新的视频设备，其中`N`是一个整数(更多的[选项](https://github.com/umlaeute/v4l2loopback#options)可用于创建多个设备或具有特定 id 的设备)。

要列出已启用的设备:

```
# requires v4l-utils package
v4l2-ctl --list-devices

# simple but might be sufficient
ls /dev/video*
```

使用 v4l2 接收器启动`scrcpy`:

```
scrcpy --v4l2-sink=/dev/videoN
scrcpy --v4l2-sink=/dev/videoN --no-display  # disable mirroring window
scrcpy --v4l2-sink=/dev/videoN -N            # short version
```

(用设备 ID 替换`N`，用`ls /dev/video*`检查)

启用后，您可以使用支持 v4l2 的工具打开视频流:

```
ffplay -i /dev/videoN
vlc v4l2:///dev/videoN   # VLC might add some buffering delay
```

例如，您可以在 [OBS](https://obsproject.com/) 内捕捉视频。

#### 缓冲

可以添加缓冲。这增加了延迟，但减少了抖动(见 [#2464](https://github.com/Genymobile/scrcpy/issues/2464) )。

该选项可用于显示缓冲:

```
scrcpy --display-buffer=50  # add 50 ms buffering for display
```

和 V4L2 接收器:

```
scrcpy --v4l2-buffer=500    # add 500 ms buffering for v4l2 sink
```

### 连接

#### TCP/IP(无线)

*Scrcpy* 使用`adb`与设备通信，`adb`可以[通过 TCP/IP 将](https://developer.android.com/studio/command-line/adb.html#wireless)连接到设备。设备必须与电脑连接在同一个网络上。

##### 自动

选项`--tcpip`允许自动配置连接。有两种变体。

如果设备(在本例中可通过 192.168.1.1 访问)已经在一个端口(通常为 5555)上监听传入的 *adb* 连接，则运行:

```
scrcpy --tcpip=192.168.1.1       # default port is 5555
scrcpy --tcpip=192.168.1.1:5555
```

如果在设备上禁用了 *adb* TCP/IP 模式(或者如果您不知道 IP 地址)，请通过 USB 连接设备，然后运行:

```
scrcpy --tcpip    # without arguments
```

它会自动找到设备的 IP 地址，启用 TCP/IP 模式，然后在启动前连接到设备。

##### 手动

或者，可以使用`adb`手动启用 TCP/IP 连接:

1.  将设备插入电脑的 USB 端口。
2.  将设备连接到与电脑相同的 Wi-Fi 网络。
3.  在“设置”→“关于手机”→“状态”中获取您的设备 IP 地址，或者执行以下命令:ADB shell IP route | awk“{ print $ 9 }”
4.  在您的设备上启用 TCP/IP 上的`adb`:`adb tcpip 5555`。
5.  拔下您的设备。
6.  连接到您的设备:`adb connect DEVICE_IP:5555` *(用您找到的设备 IP 地址替换`DEVICE_IP`)*。
7.  照常运行`scrcpy`。

从 Android 11 开始，[无线调试选项](https://developer.android.com/studio/command-line/adb#connect-to-a-device-over-wi-fi-android-11+)允许绕过将你的设备直接物理连接到你的计算机。

如果连接随机断开，运行`scrcpy`命令重新连接。如果它说没有发现设备/仿真器，尝试再次运行`adb connect DEVICE_IP:5555`，然后照常运行`scrcpy`。如果仍然显示没有找到，尝试运行`adb disconnect`，然后再次运行这两个命令。

降低比特率和分辨率可能是有用的:

```
scrcpy --bit-rate=2M --max-size=800
scrcpy -b2M -m800  # short version
```

#### 多设备

如果`adb devices`中列出了几个设备，您可以指定*序列*:

```
scrcpy --serial=0123456789abcdef
scrcpy -s 0123456789abcdef  # short version
```

也可以通过环境变量`ANDROID_SERIAL`(也由`adb`使用)提供序列号。

如果设备通过 TCP/IP 连接:

```
scrcpy --serial=192.168.0.1:5555
scrcpy -s 192.168.0.1:5555  # short version
```

如果只有一个设备通过 USB 或 TCP/IP 连接，可以自动选择它:

```
# Select the only device connected via USB
scrcpy -d             # like adb -d
scrcpy --select-usb   # long version

# Select the only device connected via TCP/IP
scrcpy -e             # like adb -e
scrcpy --select-tcpip # long version
```

您可以为多个设备启动多个 *scrcpy* 实例。

#### 设备连接时自动启动

你可以使用自动数据库:

```
autoadb scrcpy -s '{}'
```

#### 地道

要连接到远程设备，可以将本地`adb`客户端连接到远程`adb`服务器(前提是它们使用相同版本的 *adb* 协议)。

##### 远程亚行服务器

要连接到远程 *adb 服务器*，让服务器监听所有接口:

```
adb kill-server
adb -a nodaemon server start
# keep this open
```

**警告:客户端和*亚行服务器*之间的所有通信都是不加密的。**

假设此服务器可以通过 192.168.1.2 访问。然后，从另一个终端运行`scrcpy`:

```
# in bash
export ADB_SERVER_SOCKET=tcp:192.168.1.2:5037
scrcpy --tunnel-host=192.168.1.2
```

```
:: in cmd
set ADB_SERVER_SOCKET=tcp:192.168.1.2:5037
scrcpy --tunnel-host=192.168.1.2
```

```
# in PowerShell
$env:ADB_SERVER_SOCKET = 'tcp:192.168.1.2:5037'
scrcpy --tunnel-host=192.168.1.2
```

默认情况下，`scrcpy`使用用于`adb forward`隧道建立的本地端口(通常是`27183`，参见`--port`)。还可以强制使用不同的隧道端口(在涉及更多重定向的更复杂的情况下，这可能很有用):

```
scrcpy --tunnel-port=1234
```

##### 宋承宪地道

为了安全地与远程 *adb 服务器*通信，最好使用 SSH 隧道。

首先，确保 *adb 服务器*正在远程计算机上运行:

```
adb start-server
```

然后，建立一个 SSH 隧道:

```
# local  5038 --> remote  5037
# local 27183 <-- remote 27183
ssh -CN -L5038:localhost:5037 -R27183:localhost:27183 your_remote_computer
# keep this open
```

从另一个终端运行`scrcpy`:

```
# in bash
export ADB_SERVER_SOCKET=tcp:localhost:5038
scrcpy
```

```
:: in cmd
set ADB_SERVER_SOCKET=tcp:localhost:5038
scrcpy
```

```
# in PowerShell
$env:ADB_SERVER_SOCKET = 'tcp:localhost:5038'
scrcpy
```

为了避免启用远程端口转发，您可以改为强制转发连接(注意是`-L`而不是`-R`):

```
# local  5038 --> remote  5037
# local 27183 --> remote 27183
ssh -CN -L5038:localhost:5037 -L27183:localhost:27183 your_remote_computer
# keep this open
```

从另一个终端运行`scrcpy`:

```
# in bash
export ADB_SERVER_SOCKET=tcp:localhost:5038
scrcpy --force-adb-forward
```

```
:: in cmd
set ADB_SERVER_SOCKET=tcp:localhost:5038
scrcpy --force-adb-forward
```

```
# in PowerShell
$env:ADB_SERVER_SOCKET = 'tcp:localhost:5038'
scrcpy --force-adb-forward
```

与无线连接一样，降低质量可能是有用的:

```
scrcpy -b2M -m800 --max-fps=15
```

### 窗口配置

#### Title

默认情况下，窗口标题是设备型号。它可以被改变:

```
scrcpy --window-title='My device'
```

#### 位置和尺寸

可以指定初始窗口位置和大小:

```
scrcpy --window-x=100 --window-y=100 --window-width=800 --window-height=600
```

#### 无国界

若要停用窗口装饰:

```
scrcpy --window-borderless
```

#### 永远在顶端

要保持 *scrcpy* 窗口始终在顶部:

```
scrcpy --always-on-top
```

#### 全屏显示

该应用程序可以直接全屏启动:

```
scrcpy --fullscreen
scrcpy -f  # short version
```

全屏可以通过`MOD` + `f`动态切换。

#### 旋转

该窗口可以旋转:

```
scrcpy --rotation=1
```

可能的值:

*   `0`:无旋转
*   `1`:逆时针旋转 90 度
*   `2` : 180 度
*   `3`:顺时针 90 度

也可以用`MOD` + `←`、*(左)*、`MOD` + `→`、*(右)*动态改变旋转。

注意 *scrcpy* 管理 3 种不同的旋转:

*   `MOD` + `r`请求设备在纵向和横向之间切换(如果当前运行的应用程序不支持所请求的方向，它可能会拒绝)。
*   [`--lock-video-orientation`](https://github.com/Genymobile/scrcpy#lock-video-orientation) 改变镜像方向(从设备发送到电脑的视频方向)。这会影响录制。
*   `--rotation`(或`MOD` + `←` / `MOD` + `→`)只旋转窗口内容。这只会影响显示，不会影响录制。

### 其他镜像选项

#### 只读

禁用控件(可以与设备交互的一切:输入键、鼠标事件、拖放文件):

```
scrcpy --no-control
scrcpy -n
```

#### 显示

如果有几个显示器可用，可以选择要镜像的显示器:

```
scrcpy --display=1
```

可以通过以下方式检索显示 id 列表:

```
adb shell dumpsys display   # search "mDisplayId=" in the output
```

只有在设备运行至少 Android 10 的情况下，辅助显示器才可以被控制(否则它会被镜像为只读)。

#### 保持清醒

要防止设备在插入电源后延迟睡眠:

```
scrcpy --stay-awake
scrcpy -w
```

当 *scrcpy* 关闭时，恢复初始状态。

#### 关闭屏幕

在启动镜像时，可以使用命令行选项关闭设备屏幕:

```
scrcpy --turn-screen-off
scrcpy -S
```

或者随时按下`MOD` + `o`。

要重新开机，按下`MOD` + `Shift` + `o`。

在 Android 上，`POWER`按钮总是打开屏幕。为了方便起见，如果通过 *scrcpy* (通过右击或`MOD` + `p`)发送`POWER`，它将在一小段延迟后强制关闭屏幕(尽最大努力)。物理的`POWER`按钮仍然会打开屏幕。

防止设备休眠也很有用:

```
scrcpy --turn-screen-off --stay-awake
scrcpy -Sw
```

#### 关闭时断电

关闭 *scrcpy* 时关闭设备屏幕:

```
scrcpy --power-off-on-close
```

#### 开机启动

默认情况下，启动时，设备通电。

要防止这种行为:

```
scrcpy --no-power-on
```

#### 展示感动

对于演示，显示物理触摸(在物理设备上)可能是有用的。

Android 在*开发者选项*中提供了这个功能。

*Scrcpy* 提供了一个在启动时启用该功能并在退出时恢复初始值的选项:

```
scrcpy --show-touches
scrcpy -t
```

请注意，它仅显示*物理*触摸(手指在设备上的触摸)。

#### 禁用屏幕保护

默认情况下， *scrcpy* 不会阻止屏幕保护程序在电脑上运行。

要禁用它:

```
scrcpy --disable-screensaver
```

### 输入控制

#### 旋转设备屏幕

按`MOD` + `r`在纵向和横向模式之间切换。

请注意，只有当前台应用程序支持所请求的方向时，它才会旋转。

#### 复制-粘贴

任何时候 Android 剪贴板发生变化，都会自动同步到电脑剪贴板。

任何`Ctrl`快捷方式都会被转发到设备。特别是:

*   `Ctrl` + `c`典型副本
*   `Ctrl` + `x`典型切割
*   `Ctrl` + `v`通常粘贴(在计算机到设备剪贴板同步之后)

这通常如您所料。

但是实际的行为取决于活动的应用程序。例如， *Termux* 改为在`Ctrl` + `c`发送 SIGINT， *K-9 邮件*撰写新消息。

要在这种情况下复制、剪切和粘贴(但仅支持 Android >= 7):

*   `MOD` + `c`注入`COPY`
*   `MOD` + `x`注入`CUT`
*   `MOD` + `v`注入`PASTE`(计算机到设备剪贴板同步后)

此外，`MOD` + `Shift` + `v`将电脑剪贴板文本作为按键事件序列注入。当组件不接受文本粘贴时(例如在 *Termux* 中)，这很有用，但它可以中断非 ASCII 内容。

**警告:**将电脑剪贴板粘贴到设备(通过`Ctrl` + `v`或`MOD` + `v`)将内容复制到安卓剪贴板。因此，任何 Android 应用程序都可以读取其内容。您应该避免以这种方式粘贴敏感内容(如密码)。

当以编程方式设置设备剪贴板时，一些 Android 设备的行为不符合预期。提供了一个选项`--legacy-paste`来改变`Ctrl` + `v`和`MOD` + `v`的行为，以便它们也将计算机剪贴板文本作为按键事件序列注入(与`MOD` + `Shift` + `v`的方式相同)。

要禁用自动剪贴板同步，请使用`--no-clipboard-autosync`。

#### 缩放

模拟“缩放”:`Ctrl` + *点击移动*。

更准确地说，按住左键的同时按住`Ctrl`。在释放左键之前，所有鼠标移动都会相对于屏幕中心缩放和旋转内容(如果应用程序支持)。

从技术上来说， *scrcpy* 在通过屏幕中心反转的位置从“虚拟手指”产生额外的触摸事件。

#### 物理键盘模拟(HID)

默认情况下， *scrcpy* 使用 Android 键或文本注入:它在任何地方都可以工作，但仅限于 ASCII。

或者，`scrcpy`可以在 Android 上模拟物理 USB 键盘，以提供更好的输入体验(使用 AOAv2 上的 [USB HID):虚拟键盘被禁用，它适用于所有角色和 IME。](https://source.android.com/devices/accessories/aoa2#hid-support)

然而，它只有在设备通过 USB 连接时才能工作。

注意:在 Windows 上，它可能只能在 [OTG 模式](https://github.com/Genymobile/scrcpy#otg)下工作，而不能在镜像时工作(如果 USB 设备已经被另一个进程打开，如 *adb 守护进程*，则无法打开该设备)。

要启用此模式:

```
scrcpy --hid-keyboard
scrcpy -K  # short version
```

如果由于某种原因失败(例如，因为设备没有通过 USB 连接)，它会自动退回到默认模式(控制台中有一个日志)。这允许在通过 USB 和 TCP/IP 连接时使用相同的命令行选项。

在这种模式下，原始按键事件(扫描码)被发送到设备，与主机按键映射无关。所以如果你的键盘布局不匹配，必须在 Android 设备上配置，在设置→系统→语言和输入→ [物理键盘](https://github.com/Genymobile/scrcpy/pull/2632#issuecomment-923756915)中。

该设置页面可以直接启动:

```
adb shell am start -a android.settings.HARD_KEYBOARD_SETTINGS
```

但是，该选项仅在启用 HID 键盘时(或连接了物理键盘时)才可用。

#### 物理鼠标模拟(HID)

与物理键盘模拟类似，也可以模拟物理鼠标。同样，它只有在设备通过 USB 连接时才能工作。

默认情况下， *scrcpy* 使用绝对坐标的 Android 鼠标事件注入。通过模拟物理鼠标，鼠标指针出现在 Android 设备上，并注入相对鼠标运动、点击和滚动。

要启用此模式:

```
scrcpy --hid-mouse
scrcpy -M  # short version
```

您还可以将`--forward-all-clicks`添加到[中，转发所有鼠标按键](https://github.com/Genymobile/scrcpy#right-click-and-middle-click)。

启用此模式时，电脑鼠标被“捕获”(鼠标指针从电脑上消失，转而出现在 Android 设备上)。

特殊的捕获键`Alt`或`Super`，切换(禁用或启用)鼠标捕获。用其中一个把鼠标的控制权还给电脑。

#### OTG

仅使用物理键盘和鼠标模拟(HID)就可以运行 *scrcpy* ，就好像计算机键盘和鼠标通过 OTG 电缆直接插入设备一样。

在此模式下，不需要`adb` (USB 调试)，镜像被禁用。

要启用 OTG 模式:

```
scrcpy --otg
# Pass the serial if several USB devices are available
scrcpy --otg -s 0123456789abcdef
```

可以只启用 HID 键盘或 HID 鼠标:

```
scrcpy --otg --hid-keyboard              # keyboard only
scrcpy --otg --hid-mouse                 # mouse only
scrcpy --otg --hid-keyboard --hid-mouse  # keyboard and mouse
# for convenience, enable both by default
scrcpy --otg                             # keyboard and mouse
```

和`--hid-keyboard`和`--hid-mouse`一样，只有设备通过 USB 连接才起作用。

#### 文本注射偏好

键入文本时会产生两种[事件](https://blog.rom1v.com/2018/03/introducing-scrcpy/#handle-text-input):

*   *按键事件*，表示按键被按下或释放；
*   *文本事件*，表示已经输入了文本。

默认情况下，字母是使用键事件注入的，因此键盘的行为与游戏中的预期一样(通常是 WASD 键)。

但是这可能[导致问题](https://github.com/Genymobile/scrcpy/issues/650#issuecomment-512945343)。如果您遇到这样的问题，可以通过以下方法来避免:

```
scrcpy --prefer-text
```

(但这会破坏游戏中的键盘行为)

相反，您可以强制总是注入原始的关键事件:

```
scrcpy --raw-key-events
```

这些选项对 HID 键盘没有影响(在此模式下，所有按键事件都作为扫描代码发送)。

#### 键重复

默认情况下，按住键会生成重复的键事件。这可能会在一些游戏中导致性能问题，在这些游戏中这些事件是没有用的。

为了避免转发重复的关键事件:

```
scrcpy --no-key-repeat
```

该选项对 HID 键盘没有影响(该模式下按键重复由 Android 直接处理)。

#### 右击和中击

默认情况下，右键触发返回(或开机)，中键触发主页。要禁用这些快捷方式并将点击转发到设备:

```
scrcpy --forward-all-clicks
```

### 文件删除

#### 安装 APK

要安装 APK，拖放一个 APK 文件(以`.apk`结尾)到 *scrcpy* 窗口。

没有视觉反馈，日志被打印到控制台。

#### 将文件推送到设备

要将文件推送到设备上的`/sdcard/Download/`，请将&文件拖放到 *scrcpy* 窗口。

没有视觉反馈，日志被打印到控制台。

可以在开始时更改目标目录:

```
scrcpy --push-target=/sdcard/Movies/
```

### 音频转发

音频不由 *scrcpy* 转发。使用 [sndcpy](https://github.com/rom1v/sndcpy) 。

另请参见[第 14 期](https://github.com/Genymobile/scrcpy/issues/14)。

## 快捷方式

在下面的列表中，`MOD`是快捷修饰符。默认情况下，它是(左)`Alt`或(左)`Super`。

可以使用`--shortcut-mod`进行更改。可能的按键有`lctrl`、`rctrl`、`lalt`、`ralt`、`lsuper`和`rsuper`。例如:

```
# use RCtrl for shortcuts
scrcpy --shortcut-mod=rctrl

# use either LCtrl+LAlt or LSuper for shortcuts
scrcpy --shortcut-mod=lctrl+lalt,lsuper
```

*`[Super](https://en.wikipedia.org/wiki/Super_key_(keyboard_button))`通常是`Windows`或`Cmd`键。*

| 行动 | 捷径 |
| --- | --- |
| 切换全屏模式 | `MOD` + `f` |
| 向左旋转显示 | `MOD` + `←` *(左)* |
| 向右旋转显示 | `MOD` + `→` *(右)* |
| 将窗口大小调整为 1:1(像素完美) | `MOD` + `g` |
| 调整窗口大小以移除黑色边框 | `MOD` + `w` &#124; *双击左键* |
| 点击`HOME` | `MOD` + `h` &#124; *中键点击* |
| 点击`BACK` | `MOD` + `b` &#124; *右键* |
| 点击`APP_SWITCH` | `MOD` + `s` &#124; *第四次点击* |
| 点击`MENU`(解锁 screen)⁴ | `MOD` + `m` |
| 点击`VOLUME_UP` | `MOD` + `↑` *(上升)* |
| 点击`VOLUME_DOWN` | `MOD` + `↓` *(下)* |
| 点击`POWER` | `MOD` + `p` |
| 通电 | *右击* |
| 关闭设备屏幕(保持镜像) | `MOD` + `o` |
| 打开设备屏幕 | `MOD` + `Shift` + `o` |
| 旋转设备屏幕 | `MOD` + `r` |
| 展开通知面板 | `MOD` + `n` &#124; *第五次点击* |
| 展开设置面板 | `MOD` + `n` + `n` &#124; *双击 5 次* |
| 折叠面板 | `MOD` + `Shift` + `n` |
| 复制到 clipboard⁵ | `MOD` + `c` |
| 切到 clipboard⁵ | `MOD` + `x` |
| 同步剪贴板和 paste⁵ | `MOD` + `v` |
| 插入计算机剪贴板文本 | `MOD` + `Shift` + `v` |
| 启用/禁用 FPS 计数器(在 stdout 上) | `MOD` + `i` |
| 双指缩放 | `Ctrl` + *点击移动* |
| 拖放 APK 文件 | 从计算机安装 APK |
| 拖放非 APK 文件 | [将文件推送到设备](https://github.com/Genymobile/scrcpy#push-file-to-device) |

*双击黑色边框将其移除。*
*右键打开屏幕，否则按返回。*
*第四和第五个鼠标按钮，如果您的鼠标有它们的话。*
*⁴for react-开发中的原生应用，`MENU`触发开发菜单。*
*安卓上的⁵only>= 7。*

重复按键的快捷方式通过再次释放并按下按键来执行。例如，要执行“扩展设置面板”:

1.  按住`MOD`。
2.  然后双击`n`。
3.  最后释放`MOD`。

所有的`Ctrl` + *键*快捷键都被转发到设备，因此它们由活动的应用程序处理。

## 自定义路径

要使用特定的`adb`二进制文件，请在环境变量`ADB`中配置其路径:

```
ADB=/path/to/adb scrcpy
```

要覆盖`scrcpy-server`文件的路径，请在`SCRCPY_SERVER_PATH`中配置其路径。

要覆盖图标，在`SCRCPY_ICON_PATH`中配置其路径。