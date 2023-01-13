# Wacker:一个 WPA3 字典破解程序

> 原文：<https://kalilinuxtutorials.com/wacker/>

[![Wacker : A WPA3 Dictionary Cracker](img/524a06941e90778c683a1e9389965912.png "Wacker : A WPA3 Dictionary Cracker")](https://1.bp.blogspot.com/-68NNODw4V_s/X3Mtx308QLI/AAAAAAAAHr8/9AOrfq8LzvgS2zT2bOCs0D8dQ-kaj4E5QCLcBGAsYHQ/s728/Wacker.png)

Wacker 是一组帮助对 WPA3 接入点进行在线字典攻击的脚本。Wacker 利用 wpa_supplicant 控制接口来控制请求者守护程序的操作，并获取状态信息和事件通知，最终帮助在暴力攻击期间加速连接尝试。

**找到要使用的 wpa 3 AP**

如果你已经有一个 WPA3 应用程序，那就太好了。作为替代，您可以使用 mac80211_hwsim(详情如下)或使用 RF Hackers Sanctuary 提供的虚拟机来设置本地环境(强烈推荐)。测试几乎是使用模拟的 mac80211 环境执行的。很少有人关注真正的美联社…现在…所以你的 YMWV。

**本地模拟电台**

要设置您自己的 802.11 无线电软件模拟器，只需配置并加载正确的 mac80211_hwsim 模块。

**# modprobe MAC 80211 _ HW sim radios = 4
# iwconfig**
WLAN 0 IEEE 802.11 ESSID:off/any
模式:受管接入点:非关联 Tx-Power=20 dBm
重试短限:7 RTS thr:off Fragment thr:off
电源管理:on

WLAN 1 IEEE 802.11 ESSID:off/any
模式:受管接入点:非 IEEE 802.11 ESSID:off/any
模式:管理接入点:非关联 Tx-Power=20 dBm
重试短限值:7 RTS thr:off 碎片 thr:off
电源管理:on

选择一个新接口作为您的 WPA3 接入点，并使用以下配置文件。

**# cat hostapd . conf**
interface = WLAN 0
ssid = WCTF _ 18
driver = nl 80211
HW _ mode = g
channel = 1
logger _ syslog =-1
logger _ syslog _ level = 3
wpa = 2
wpa _ pass phrase = aero mechanics
wpa _ key _ mgmt = SAE
rsn _ pairwise = CCMP
IEEE 800

并使用启动 hostapd

**# hostapd-K-DD hostapd . conf**

**拆分一个词表**

如果您打算将破解工作分散到一系列网卡上，提供的 split.sh 脚本将为您划分一个单词列表。

**#。/split . sh 10 cyber punk . words**
50916 cyber punk . words . AAA
50916 cyber punk . words . aab
50916 cyber punk . words . AAC
50916 cyber punk . words . aad
50916 cyber punk . words . aae
50916 cyber punk . words . AAF
50916 cyber punk . words . AAG
50916

**建设 WPA _ 申请人**

我们提供了自己的 wpa_supplicant，以保证设置了某些配置以及一些需要在源代码本身中发生的修改。要构建，只需执行以下操作。希望在未来这将成为一个不赞成的步骤。

# apt-get install-y pkg-config libnl-3-dev gcc libssl-dev libnl-genl-3-dev
# CD wpa _ supplicant-2.8/wpa _ supplicant/
# CP def config _ brute _ force。配置
# make-j4
# ls-al wpa _ supplicant
-rwxr-xr-x1 root root 13541416 年 5 月 31 日 16:30 wpa_supplicant

令人感兴趣的是一些新的事件消息，它们被添加到 wpa 恳求者控制界面，以帮助进一步区分 wacker 脚本挂钩的结果。

/**我们的蛮力验证成功(WPA 3)*/# define WPA _ EVENT _ BRUTE _ SUCCESS " CTRL-EVENT-BRUTE-SUCCESS "
/* *我们的蛮力验证失败(WPA 3)*/# define WPA _ EVENT _ BRUTE _ FAILURE " CTRL-EVENT-BRUTE-FAILURE "

**Python 需求**

在其他 python 3-ism 中，wacker.py 脚本使用了一些 f 字符串。为了更快地发布代码，这个需求被保留了下来。如果需要，这里有一些 Python3.7 的通用安装说明。我知道在未来这将成为一个不赞成的步骤。

# apt-get install build-essential tk-dev libncurses S5-dev libncursesw 5-dev libreadline 6-dev libgdbm-dev libsqlite 3-dev libssl-dev libbz 2-dev libexpat 1-dev liblzma-dev zlib 1g-dev libffi-dev-y
# wget https://www.python.org/ftp/python/3.7.0/Python-3.7.0.tar.xz
# tar xf Python-3 . 7 . 0 . tar . xz
# CD Python-3 . 7 . 0
#。/configure
# make-j4
# make alt install

**运行瓦克**

wacker.py 脚本旨在执行所有繁重的工作。

**#。/wacker . py–help**
用法:wacker . py[-h]–WORD list WORD list–INTERFACE 接口–BSSID BSSID
–SSID SSID–freq FREQ[–START START _ WORD][–debug]
一个 WPA3 字典破解程序。必须以 root 用户身份运行！
可选参数:
-h，–help 显示此帮助信息并退出
–wordlist WORD list 要使用的 WORD list
–INTERFACE INTERFACE
要使用的 INTERFACE
–目标的 BSSID BSSID BSSID
–SSID SSID wpa 3 AP 的 SSID
–AP 的 freq FREQ 频率
–START _ WORD 要在 WORD list 中开始使用的 WORD
–调试增加日志输出

如果运气好的话…只使用一个实例来运行攻击…

#./wacker . py–wordlist cyber punk . words–ssid WCTF _ 18–bssid 02:00:00:00:00:00–接口 WLAN 2–freq 2412
开始时间:2020 年 8 月 21 日 07:40:11
开始 wpa _ 恳求者…
5795 / 509151 字(1.14%) : 79.41 字/秒:0.020 小时过去时间:1.76 小时

如果您有备用网卡，运行 wacker 的多个实例是很容易的。别忘了把单词表也分开。

#./wacker . py–wordlist cyber punk . words . AAA–ssid WCTF _ 18–bssid 02:00:00:00:00:00–接口 WLAN 1–freq 2412
#。/wacker . py–wordlist cyber punk . words . aab–ssid WCTF _ 18–bssid 02:00:00:00:00:00–接口 WLAN 2–freq 2412
#。/wacker . py–wordlist cyber punk . words . AAC–ssid WCTF _ 18–bssid 02:00:00:00:00:00–接口 WLAN 3–freq 2412

**感兴趣的文件**

瓦克相当啰嗦。感兴趣的文件可以在 **/tmp/wpa_supplicant/** 下找到

*   WLAN 1:uds 的一端
*   WLAN 1 _ client:uds 的一端
*   wlan1.conf:需要初始 wpa_supplicant conf
*   wlan1.log:请求者输出(仅当使用–debug 选项时)
*   WLAN 1 . pid:wpa _ suppliant 实例的 PID 文件
*   wlan1_wacker.log : wacker 调试输出

**注意事项**

wacker 不处理由目标 WPA3 AP 设置的 ACL。也就是说，当前代码总是使用相同的 MAC 地址。如果目标 AP 将我们的 MAC 地址列入黑名单，那么脚本不会区分真正的认证失败和我们被拒绝的黑名单 MAC。这将意味着我们会认为真正的密码是失败的。解决…的一种方法。我们必须以降低速度为代价将 macchanger 添加到源中。

wacker 似乎经常暂停一切，因为 AP 会发出退避超时。这将导致指标显示看似暂停，然后又重新开始。这是预期的行为。

**常见问题**

*   当你的客户端驱动不支持正确的 AKM 时，你会看到这个。通常，在您尝试并运行 wacker 脚本后，这在 wpa_supplicant 输出中表现出来。请求者将实质上挂起，等待 AKM 问题的进一步指示，详情如下。在 WPA3 的情况下，所需的 AKM 是 00-0F-AC:8 (SAE)。

u631_3: WPA: AP 组 0x10 网络概要组 0x18 可用组 0x10 u631_3: WPA:使用 GTK CCMP
u631_3: WPA: AP 成对 0x10 网络配置文件成对 0x18 可用成对 0x10 u631_3: WPA:使用 PTK CCMP
u631 _ 3:WPA:AP key _ mgmt 0x 400 网络配置文件 key _ mgmt 0x 400；available key _ mgmt 0x 400
u631 _ 3:WPA:无法选择已验证的密钥管理类型
u631_3: WPA:无法设置 WPA 密钥管理和加密套件

**待办事项**

*   创建一个包装脚本来跨多个网卡启动 wacker。这将避免为每个网卡手动实例化 wacker。让包装器也拆分单词列表并合并统计数据。

[**Download**](https://github.com/blunderbuss-wctf/wacker)