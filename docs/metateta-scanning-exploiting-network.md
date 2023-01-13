# meta eta–扫描和利用网络协议的自动化工具

> 原文：<https://kalilinuxtutorials.com/metateta-scanning-exploiting-network/>

Metateta 是一个自动化工具，使用 metasploit 扫描和利用网络协议，并为大型网络提供更快的 pen 测试。网络协议是包含规则、技术和格式的正式模型和策略，这些规则、技术和格式表征网络上至少两个小工具之间的通信。网络协议监督适时、安全和受管理的信息或网络通信的端到端过程。

**也看 [如何使用 Masscan 快速枚举大量主机](https://kalilinuxtutorials.com/masscan/)**

## **你可以用梅塔塔做什么**

*   使用所有 metasploit 模块扫描特定的网络协议，如 smb、smtp、snmp
*   根据特定网络协议运行所有辅助模块
*   针对特定网络协议运行所有可能的 Metasploit 漏洞利用`That's is not recommended for real pen testing`
*   可以针对一个目标或网络运行，甚至可以针对带有目标的文本文件运行

## **利用例子的**

```
run.py -R 192.168.1.15-255 -p smb -x exploit 

run.py -r 192.168.1.15 -p smtp -x scan 

run.py -f hosts.txt -p smb -x auxiliary
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/WazeHell/metateta)