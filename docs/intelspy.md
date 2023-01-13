# IntelSpy:执行自动网络侦察扫描

> 原文：<https://kalilinuxtutorials.com/intelspy/>

[![IntelSpy : Perform Automated Network Reconnaissance Scans](img/505db85c403520dae3c2e950aa95e744.png "IntelSpy : Perform Automated Network Reconnaissance Scans")](https://1.bp.blogspot.com/-XAS1qidoFIg/XytHZmWwzdI/AAAAAAAAHLE/SVc-ZqGO3HYaUiCulPJBQQ5POIscDEknACLcBGAsYHQ/s728/IntelSpy%25281%2529.png)

IntelSpy 是一种用于执行自动网络侦察扫描以收集网络情报的工具。

它是一个多线程的网络智能工具，执行自动网络服务枚举。它可以执行实时主机检测扫描、端口扫描、服务枚举扫描、网页内容扫描、暴力破解、详细的离线漏洞搜索等等。

该工具还将使用许多不同的工具为每个检测到的服务启动进一步的枚举扫描。

**特性**

*   以 IP 地址、IP 范围(CIDR 表示法)和可解析主机名的形式扫描多个目标。
*   同时扫描目标。
*   检测 IP 范围(CIDR)网络中的活动主机。
*   可定制的端口扫描配置文件和服务枚举命令。
*   为结果收集和报告创建目录结构。
*   记录执行的每个命令。
*   生成包含要手动运行的命令的 shell 脚本。
*   以 txt 和 markdown 格式提取重要信息以备进一步检查。
*   将数据存储到 SQLite 数据库。
*   生成 HTML 报告。

**要求**

*   Python 3 ( `**sudo apt install python3**`)
*   Linux(最好是 Kali Linux 或任何其他包含以下工具的黑客发行版。)
    *   [https://www.kali.org/downloads/](https://www.kali.org/downloads/)
*   toml([https://github . com/toml-lang/toml](https://github.com/toml-lang/toml)
*   秘书([https://github.com/danielmiessler/SecLists](https://github.com/danielmiessler/SecLists))
*   卷曲(*先决条件* ) ( `**sudo apt install curl**`)
*   enum4linux ( *先决条件* ) ( `**sudo apt install enum4linux**`)
*   gobuster ( *先决条件* ) ( `**sudo apt install gobuster**`)
*   九头蛇(T1)【可选的】T2)(`**sudo apt install hydra**`
*   ldapsearch ( *可选* ) ( `**sudo apt install ldap-utils**`)
*   美杜莎(T1)【可选的】T2)(`**sudo apt install medusa**`
*   nbtscan ( *先决条件* ) ( `**sudo apt install nbtscan**`)
*   nikto ( *先决条件* ) ( `**sudo apt install nikto**`)
*   nmap ( *先决条件* ) ( `**sudo apt install nma**p`)
*   onesixtyone ( *先决条件* ) ( `**sudo apt install onesixtyone**`)
*   振荡器(*可选* ) ( `**sudo apt install oscanner**`)
*   pandoc ( *先决条件* ) ( `**sudo apt install pando**c`)
*   potator _ *可选* ) _ `**sudo apt install patator**`
*   showmount ( *先决条件*)(‘系统工具’)
*   smbclient ( *先决条件* ) ( `**sudo apt install smbclient**`)
*   smbmap ( *先决条件* ) ( `**sudo apt install smbmap**`)
*   SMTP-用户-枚举(*先决条件* ) ( `**sudo apt install smtp-user-enum**`)
*   snmpwalk ( *先决条件* ) ( `**sudo apt install snmp**`)
*   sslscan ( *先决条件* ) ( `**sudo apt install sslscan**`)
*   svwar ( *先决条件* ) ( `**sudo apt install sipvicious**`)
*   tnscmd10g ( *先决条件* ) ( `**sudo apt install tnscmd10g**`)
*   whatweb ( *先决条件* ) ( `**sudo apt install whatweb**`)
*   wkhtmltoimage ( *先决条件*)(【https://github.com/wkhtmltopdf/wkhtmltopdf/】T2)
*   wpscan ( *可选* ) ( `**sudo apt install wpscan**`)

**pip 3 install-r requirements . txt**

**用途**

```
$ python3 intelspy.py -h

 ___               __        
  |  ._ _|_  _  | (_  ._     
 _|_ | | |_ (/_ | __) |_) \/ 
                      |   /  

IntelSpy v2.0 - Perform automated network reconnaissance scans to gather network intelligence.
IntelSpy is an open source tool licensed under GPLv3.
Written by: @maldevel | Logisek ICT
Web: https://logisek.com | https://pentest-labs.com
Project: https://github.com/maldevel/intelspy

usage: intelspy.py [-h] [-ts TARGET_FILE] -p PROJECT_NAME -w WORKING_DIR
                   [--exclude <host1[,host2][,host3],...>] [-s SPEED]
                   [-ct <number>] [-cs <number>] [--profile PROFILE_NAME]
                   [--livehost-profile LIVEHOST_PROFILE_NAME]
                   [--heartbeat HEARTBEAT] [-v]
                   [targets [targets ...]]

positional arguments:
  targets               IP addresses (e.g. 10.0.0.1), CIDR notation (e.g.
                        10.0.0.1/24), or resolvable hostnames (e.g.
                        example.com) to scan.

optional arguments:
  -h, --help            show this help message and exit
  -ts TARGET_FILE, --targets TARGET_FILE
                        Read targets from file.
  -p PROJECT_NAME, --project-name PROJECT_NAME
                        project name
  -w WORKING_DIR, --working-dir WORKING_DIR
                        working directory
  --exclude <host1[,host2][,host3],...>
                        exclude hosts/networks
  -s SPEED, --speed SPEED
                        0-5, set timing template (higher is faster) (default:
                        4)
  -ct <number>, --concurrent-targets <number>
                        The maximum number of target hosts to scan
                        concurrently. Default: 5
  -cs <number>, --concurrent-scans <number>
                        The maximum number of scans to perform per target
                        host. Default: 10
  --profile PROFILE_NAME
                        The port scanning profile to use (defined in port-
                        scan-profiles.toml). Default: default
  --livehost-profile LIVEHOST_PROFILE_NAME
                        The live host scanning profile to use (defined in
                        live-host-scan-profiles.toml). Default: default
  --heartbeat HEARTBEAT
                        Specifies the heartbeat interval (in seconds) for task
                        status messages. Default: 60
  -v, --verbose         Enable verbose output. Repeat for more verbosity (-v,
                        -vv, -vvv).
```

**用法举例**

*   **扫描单个目标**

sudo python 3 intelspy . py-p my project name-w/home/user/pt/projects/192 . 168 . 10 . 15
sudo python 3 intelspy . py-p my project name-w/home/user/pt/projects/192 . 168 . 10 . 15-v
sudo python 3 intelspy . py-p my project name-w/home/user/pt/projects/192 . 168 . 10 . 15

*   **扫描主机名**

sudo python 3 intelspy . py-p my project name-w/home/user/pt/projects/example.com

*   **扫描网络范围(CIDR)**

sudo python 3 intelspy . py-p my project name-w/home/user/pt/projects/192 . 168 . 10 . 0/24

*   **扫描多个目标(逗号分隔)**

sudo python 3 intelspy . py-p my project name-w/home/user/pt/projects/192 . 168 . 10 . 15 192 . 168 . 10 . 0/24 example.com

*   **扫描文件中的目标**

sudo python 3 intelspy . py-p my project name-w/home/user/pt/projects/-ts/home/user/targets . txt

*   **排除一台主机**

sudo python 3 intelspy . py-p my project name-w/home/user/pt/projects/–exclude 192 . 168 . 10 . 9 192 . 168 . 10 . 0/24

*   **排除许多主机**

sudo python 3 intelspy . py-p my project name-w/home/user/pt/projects/–exclude 192 . 168 . 10 . 9，192.168.10.24 1

[**Download**](https://github.com/maldevel/intelspy)