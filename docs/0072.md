# airbase——一个用于自动 wpa psk 握手捕获的 shell 脚本

> 原文：<https://kalilinuxtutorials.com/airbash-shell-script/>

Airbash 是一个 POSIX 兼容的，完全计算机化的 WPA PSK 握手捕获脚本，用于渗透测试。它非常适合 Bash 和 Android Shell(在 Kali Linux 和 Cyanogenmod 10.2 上试用过)，并利用 aircrack-ng 来过滤目前与接入点(AP)相关联的客户。然后，这些客户将被取消身份验证，记住最终目标是在尝试重新连接到 AP 时捕获握手。对被捕捉握手的确认是利用空中捕捉来完成的。如果设计合理的话，至少有一次握手被捕捉到的可能性很小，它们会被输入 SQLite3 数据库，与捕获季节和潮起潮落的 GPS 信息一起输入。

捕获后，可以使用 crackdefault.sh 对数据库中易受攻击的路由器模型进行尝试。它将扫描与实现的模块相匹配的段落，这些模块目前包含计算 Speedport 500-700 排列、Thomson/SpeedTouch 和 UPC 7 位数(UPC1234567)交换机的默认键的算法。

**亦读[SAWEF–发送攻击网页表单](https://kalilinuxtutorials.com/sawef-send-attack/)**

## **对吹气的要求**

监控模式下的 WiFi 接口 aircrack-ng SQLite3 openssl 用于编译 hcxtools 中的模块 discretionary wlanhc2hcx。

记住记录握手的 GPS 方向的最终目标，设计你的便利记录软件来记录。Airbash 将可靠地利用猫科动物“$ path $ loc”*的产量。txt 2 >/dev/invalid | awk ' NR = = 0；END{print} '，相当于细读所有。txt 记录在。loc/并拾取第二行。这些用法背后的解释是 GPS 记录器的有用性，它被用在开发设备上。

## **计算默认键**

在捕获新的握手之后，可以在数据库中查询易受攻击的路由器型号。如果模块适用，则会计算此路由器系列的默认密钥，并将其用作 aircrack-ng 的输入，以尝试恢复密码短语。

## **编译模块**

用于计算[汤姆逊/速度触摸](https://packetstormsecurity.com/files/84788/STKeys-Thomson-WPA-Key-Recovery-Tool-1.0.html)和 [UPC1234567](https://haxx.in/) (7 个随机数字)默认密钥的模块包含在`src/`中

该代码的功劳归于作者凯文·迪瓦恩和中的[彼得@哈克斯。](mailto:peter@haxx.in)

```
On Linux:
gcc -fomit-frame-pointer -O3 -funroll-all-loops -o modules/st modules/stkeys.c -lcrypto
gcc -O2 -o modules/upckeys modules/upc_keys.c -lcrypto
```

如果在 Android 上，您可能需要将二进制文件复制到/system/xbin/或另一个允许执行二进制文件的目录。

## **用法**

运行`install.sh`将创建数据库，准备文件夹结构，并创建指向两个脚本的快捷链接，这两个脚本可以移动到 PATH 上的一个目录中，以允许从任何位置执行。

安装后，您可能需要手动调整`airba.sh`中第 46 行的`INTERFACE`。这将在以后自动确定，但目前默认设置为`wlan0`，以允许与 Android 上的 [bcmon](https://code.google.com/archive/p/bcmon/) 的开箱即用兼容性。

`./airba.sh`启动脚本，自动扫描并攻击数据库中没有的目标。`./crackdefault.sh`试图破解已知的默认密钥算法。

要查看数据库内容，请在主目录中运行`sqlite3 .db.sqlite3 "SELECT * FROM hs"`。

## **输出**

`**_n**`:发现的接入点数量

`**__c/m**` **:** 分别表示找到的客户端数和最大客户端数

`**-**` **:** 接入点被列入黑名单

`**x**` **:** 接入点已在数据库中

`**?**` **:** 接入点超出范围(对 airodump 不再可见)

## **数据库**

数据库包含一个名为`hs`的表，有七列。

**`id` :** 增加表格条目的计数器

**`lat`** 和 **`lon` :** 握手的 GPS 坐标(如果可用)

**`bssid` :** 接入点 MAC 地址

**`essid` :** 名称标识符

**`psk` :** WPA 密码，如果知道的话

**`prcsd` :** 由 crackdefault.sh 设置的标志，用于防止在使用自定义密码短语时重复计算默认密钥。

目前，SQLite3 数据库没有密码保护。

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/tehw0lf/airbash/)