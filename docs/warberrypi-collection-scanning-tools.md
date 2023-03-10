# WarBerryPi–用于战术开发的扫描工具集

> 原文：<https://kalilinuxtutorials.com/warberrypi-collection-scanning-tools/>

WarBerryPi 是为了在 red teaming 场景中用作硬件植入而设计的，在这种场景中，我们希望在尽可能隐蔽的情况下，在短时间内获得尽可能多的信息。找个网口插上就行了。脚本的设计方式使得该方法旨在避免网络中可能导致检测的噪声，并尽可能提高效率。WarBerry 脚本是为提供该功能而组合在一起的扫描工具的集合。

**也读作 [鹰眼——一种抓取文件系统或目录的工具](https://kalilinuxtutorials.com/hawkeye-crawl-filesystem-directory/)**

## **WarBerryPi 用法**

要获得所有选项和开关的列表，请使用:

T2`**python warberry.py -h**`

```
 **Options:**

 **--version                             show program's version number and exit
  -h, --help                            show this help message and exit
  -p PACKETS, --packets=PACKETS         Number of Network Packets to capture
  -I IFACE, --interface=IFACE           Network Interface to use. Default: eth0
  -N NAME, --name=NAME                  Hostname to use. Default: Auto
  -i INTENSITY, --intensity=INTENSITY   Port scan intensity. Default: T4
  -Q, --quick                           Scan using threats. Default: Off
  -P, --poison                          Turn Poisoning on/off. Default: On
  -H, --hostname                        Do not Change WarBerry hostname Default: Off
  -e, --enumeration                     Disable Enumeration mode. Default: Off
  -M, --malicious                       Enable Malicious only mode. Default: Off
  -B, --bluetooth                       Enable Bluetooth scanning. Default: Off
  -r, --recon                           Enable Recon only mode. Default: Off
  -W, --wifi                            Enable WiFi scanning. Default: Off
  -S, --sniffer                         Enable Sniffer only mode. Default: Off
  -C, --clear                           Clear previous output folders in ../Results
  -m, --man                             Print WarBerry man pages**

**example usage: sudo python warberry.py -a -T                Attack all TCP Ports
               sudo python warberry.py -r                   Use only the recon modules
               sudo python warberry.py -H -I wlan0          Use the wlan0 interface and dont change hostname
               sudo python warberry.py -I eth0 -i -T3       Use the eth0 interface and T3 scanning intensity
               sudo python warberry.py -I eth0 -N HackerPC  Use the eth0 interface and change hostname to HackerPC
```

## **安装**

跑 **`sudo bash setup.sh`**

## **报告**

根据您的操作系统和设置，将 **/RESULTS** 文件夹下载到/var/www、/Library/Webserver/Documents/或 XAMPP web 目录中。

在本地下载 warberry.db 文件并保存到 **Reporting/** 中。

将 Reporting/WarberryReporting/SQLiteConnection/PHP 下的文件 Config.php 更改为使用 warberry.db 的正确路径

在**报告/** 下运行 index.html

#### **免责声明**

该工具仅用于学术目的和受控环境下的测试。未经测试网络所有者的适当授权，请勿使用。作者对该工具的任何误用不负任何责任。

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/secgroundzero/warberry)