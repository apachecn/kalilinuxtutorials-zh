# Discover:用于自动化各种渗透测试任务的定制 Bash 脚本

> 原文：<https://kalilinuxtutorials.com/discover-scripts-automate-penetration-testing/>

[![Discover : Custom Bash Scripts Used To Automate Various Penetration Testing Tasks](img/724087afcc26afe8b3648a18be139ea9.png "Discover : Custom Bash Scripts Used To Automate Various Penetration Testing Tasks")](https://1.bp.blogspot.com/-VRaTK1qh18k/Xa0_pHVKwBI/AAAAAAAADCM/IRDAnt43U5I-WcK2jIXUb-OGEza-bL82ACLcBGAsYHQ/s1600/discover%25281%2529.png)

**发现**用于自动化各种渗透测试任务的定制 bash 脚本，包括侦察、扫描、解析以及使用 Metasploit 创建恶意负载和监听器。用于 Kali Linux 和渗透测试框架(PTF)。

**下载、设置和使用**

git 克隆[https://github.com/leebaird/discover](https://github.com/leebaird/discover)/opt/discover/
所有脚本都必须从这个位置运行。
cd /opt/discover/
。/update.sh

*   **侦察**
    *   领域
    *   人
    *   解析 salesforce
*   **扫描**
    *   生成目标列表
    *   无类域内路由选择(Classless Inter-Domain Routing)
    *   目录
    *   IP、范围或域
    *   重新运行 Nmap 脚本和 MSF aux
*   **网页**
    *   不安全的直接对象引用
    *   在 Firefox 中打开多个标签
    *   Nikto
    *   加密套接字协议层
*   **杂项**
    *   解析 XML
    *   生成恶意负载
    *   启动 Metasploit 侦听器
    *   更新
    *   出口

**也可阅读-[丽塔:真实情报威胁分析](http://kalilinuxtutorials.com/rita-real-intelligence-threat-analytics/)**

**侦察**

**域**

*   侦察
    *   消极的
    *   活跃的
    *   将名称导入现有的识别工作区
    *   上一个菜单

被动使用 ARIN、dnsrecon、goofile、goog-mail、goohost、theHarvester、Metasploit、URLCrazy、Whois、多个网站和 recon-ng。

Active 使用 dnsrecon、WAF00W、traceroute、Whatweb 和 recon-ng。

[*]获取 Bing、Builtwith、Fullcontact、GitHub、Google、Hashes、Hunter、SecurityTrails 和 Shodan 的 API 密钥，以获得 recon-ng 和 theHarvester 的最大效果。

API 键位置:
recon-ng
show keys
keys 添加 bing _ API
the harvester
/opt/the harvester/API-keys . YAML

*   人
    *   侦察
        *   名字:
        *   姓氏:

*   结合来自多个网站的信息。

**解析 salesforce**

*   在 salesforce 创建免费帐户(https://connect.data.com/login)。
*   对目标公司执行搜索>选择公司名称>查看全部。
*   将结果复制到新文件中。

输入列表的位置:

*   将姓名和职位收集到一个干净的列表中。

**扫描**

**生成目标列表**

*   扫描
    *   局域网
    *   网络基本输入输出系统(Network Basic Input / Output System)
    *   网络发现
    *   Ping 扫描
    *   上一个菜单

*   使用不同的工具创建一个目标列表，包括愤怒的 IP 扫描器，arp 扫描，网络发现和 nmap pingsweep。

**CIDR、列表、IP、范围或 URL**

*   扫描类型:
    *   外部的
    *   内部的
    *   上一个菜单

*   外部扫描会将 nmap 源端口设置为 53，并将 max-rrt-timeout 设置为 1500ms。
*   内部扫描会将 nmap 源端口设置为 88，并将最大 rrt 超时设置为 500 毫秒。
*   Nmap 用于执行主机发现、端口扫描、服务枚举和操作系统识别。
*   匹配的 nmap 脚本用于额外的枚举。
*   附加工具:enum4linux、smbclient 和 ike-scan。
*   还利用了匹配的 Metasploit 辅助模块。

**网**

**不安全的直接对象引用**

使用 Burp，认证到一个网站，地图和蜘蛛，然后注销。**目标>站点地图>选择网址>右键>复制本主机中的网址**。将结果粘贴到新文件中。

输入你的文件的位置:

**在火狐打开多个标签**

*   使用以下功能在 Firefox 中打开多个标签:
    *   目录
    *   robots.txt 中的目录
    *   上一个菜单

*   使用包含 IP 和/或 URL 的列表。
*   使用 wget 提取一个域的 robot.txt 文件，然后打开所有目录。

**Nikto**

*   并行运行 Nikto 的多个实例。
    *   IP 列表。
    *   IP:端口列表。
    *   上一个菜单

**SSL**

检查 SSL 证书问题。
输入您的列表的位置:

*   使用 sslscan 和 sslyze 检查 SSL/TLS 证书问题。

**杂项**

**解析 XML**

*   将 XML 解析为 CSV。
    *   打嗝(Base64)
    *   Nessus(。nessus)
    *   Nexpose (XML 2.0)
    *   Nmap
    *   Qualys
    *   上一个菜单

**生成恶意有效载荷**

*   恶意负载
    *   Android/meter preter/reverse _ TCP
    *   cmd/windows/reverse_powershell
    *   java/jsp_shell_reverse_tcp
    *   Java/JSP _ shell _ reverse _ TCP(Windows)
    *   Linux/x64/meter preter _ reverse _ https
    *   Linux/x64/meter preter _ reverse _ TCP
    *   linux/x64/shell/reverse_tcp
    *   OS x/x64/meter preter _ reverse _ https
    *   OS x/x64/meter preter _ reverse _ TCP
    *   php/meterpreter/reverse_tcp
    *   python/meter preter _ reverse _ https
    *   python/meterpreter_reverse_tcp
    *   windows/x64/meter preter _ reverse _ https
    *   windows/x64/meter preter _ reverse _ TCP
    *   上一个菜单

**启动一个 Metasploit 监听器**

*   Metasploit 侦听器
    *   Android/meter preter/reverse _ TCP
    *   cmd/windows/reverse_powershell
    *   java/jsp_shell_reverse_tcp
    *   Linux/x64/meter preter _ reverse _ https
    *   Linux/x64/meter preter _ reverse _ TCP
    *   linux/x64/shell/reverse_tcp
    *   OS x/x64/meter preter _ reverse _ https
    *   OS x/x64/meter preter _ reverse _ TCP
    *   php/meterpreter/reverse_tcp
    *   python/meter preter _ reverse _ https
    *   python/meterpreter_reverse_tcp
    *   windows/x64/meter preter _ reverse _ https
    *   windows/x64/meter preter _ reverse _ TCP
    *   上一个菜单

**更新**

*   用于更新 Kali Linux、发现脚本、各种工具和定位数据库。

[**Download**](https://github.com/leebaird/discover)