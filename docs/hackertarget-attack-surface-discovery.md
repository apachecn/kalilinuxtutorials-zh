# 黑客目标:帮助组织发现攻击面的工具和网络智能

> 原文：<https://kalilinuxtutorials.com/hackertarget-attack-surface-discovery/>

Hackertarget 是一款开源工具和网络智能工具，帮助组织发现和识别攻击面的安全漏洞。如果没有关于网络足迹的战术情报，识别组织的漏洞是不可能的任务。

通过将开源智能与世界上最好的开源安全扫描工具相结合，我们能够发现您的攻击面。由于能够在几秒钟内部署互联网资产，攻击面变得更加动态且不断增长。

这个事实使得映射您的外部网络足迹成为一个难题。我们旨在提供解决这一问题的方案。从我们的域和 IP 地址数据工具开始，然后转向使用托管的开源扫描器来映射暴露。

**又读[SMWYG(Show-Me-What-You-Got):对组织或个人进行 OSINT &侦察的工具](https://kalilinuxtutorials.com/smwyg/)**

## **如何运营 Hackertarget？**

```
git clone https://github.com/ismailtasdelen/hackertarget.git
cd hackertarget/
python hackertarget.py
```

##### **视图:**

```
root@ismailtasdelen:~# python hackertarget.py 

  _               _              _                          _   
 | |_   __ _  __ | |__ ___  _ _ | |_  __ _  _ _  __ _  ___ | |_ 
 | ' \ / _` |/ _|| / // -_)| '_||  _|/ _` || '_|/ _` |/ -_)|  _|
 |_||_|\__,_|\__||_\_\___||_|   \__|\__,_||_|  \__, |\___| \__|
                                                |___/           
		         Ismail Tasdelen
 | github.com/ismailtasdelen | linkedin.com/in/ismailtasdelen |

[1] Traceroute
[2] Ping Test
[3] DNS Lookup
[4] Reverse DNS
[5] Find DNS Host
[6] Find Shared DNS
[7] Zone Transfer
[8] Whois Lookup
[9] IP Location Lookup
[10] Reverse IP Lookup
[11] TCP Port Scan
[12] Subnet Lookup
[13] HTTP Header Check
[14] Extract Page Links
[15] Exit

Which option number :
```

##### **克隆现有存储库(使用 HTTPS 克隆)**

```
root@ismailtasdelen:~# git clone https://github.com/ismailtasdelen/hackertarget.git
```

##### **克隆现有存储库(使用 SSH 克隆)**

```
root@ismailtasdelen:~# git clone git@github.com:ismailtasdelen/hackertarget.git
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/ismailtasdelen/hackertarget)