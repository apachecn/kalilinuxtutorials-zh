# FreeVulnSearch:通过 cve-search.org API 查询漏洞的脚本

> 原文：<https://kalilinuxtutorials.com/freevulnsearch-script-vulnerabilities/>

这个 NMAP NSE 脚本是免费 OCSAF 项目 FreeVulnSearch 的一部分。

结合 NMAP 的版本扫描“-sV”，使用 CVE(常见漏洞和暴露)自动指定相应的漏洞，并使用 CVSS(常见漏洞评分系统)指定漏洞的严重性。

为了更加清楚，CVSS 仍然被分配给相应的 3.0 版 CVSS 分级:

*   关键(CVSS 9.0–10.0)
*   高(CVSS 7.0–8.9)
*   中等(CVSS 4.0–6.9)
*   低(CVSS 0.1-3.9)
*   无(CVSS 0.0)

默认情况下，通过 circl.lu 提供的项目的巧妙的公共 API，使用由确定的 CPE 来查询 CVE

通过 circl.lu API 使用确定的 CPE 进行查询。有关 circl.lu API 保密性的更多信息，请直接访问[网站](https://www.circl.lu/services/cve-search/)。

最好的方法是在本地安装 [cve-search](http://(https://github.com/cve-search/cve-search) 并使用你自己的 API

**也可以阅读-[Kali Linux 最有用的命令](https://kalilinuxtutorials.com/useful-commands-kali-linux/)？**

**nmap-sV–script freevulnsearch–script-args API path =**

**安装**:

您可以直接在 NMAP 命令中指定脚本路径，例如

**nmap-sV–script ~/freevulnsearch**

或者将脚本复制到 NMAP 安装的适当目录中。

**以 KALI LINUX 为例:/usr/share/nmap/scripts/
sudo nmap–script-ubdatedb**

重要提示:首先阅读保密信息。建议单独运行 freevulnsearch.nse，无需额外的 nse 脚本。如果您不想对类别 safe、vuln 和 external 进行分配，则不要执行上面提到的 nmap–script-updatedb 命令。

**用法:**

用法很简单，只需使用 NMAP -sV 和这个脚本。

**nmap-sV–脚本自由搜索**

根据我的测试，出于稳定性的原因，当查询 API 以处理多个并发请求时，应该只使用不带 TLS 的 http。

因此，您可以选择使用输入参数禁用 TLS。重要的是，此后对 circl.lu 的 API 查询是不加密的。

**nmap-sV–script freevulnsearch–script-args notls = yes**

如果您使用类别 safe 或 vuln 进行扫描，请排除该脚本或类别 external，或者不要将该脚本添加到 NMAP 默认目录中。建议单独运行 freevulnsearch.nse，无需额外的 nse 脚本。

**格式的 CPE 异常处理:**

如果 NMAP CPE 不明确，freevulnsearch.nse 脚本中的几个函数会检查 CPE 的格式是否不准确。例如:

*   (MySQL) 5.0.51a-3ubuntu5 到 5.0.51a
*   (进出口 smtpd) 4.90_1 到 4.90
*   (OpenSSH) 6.6.1p1 到 6.6:p1
*   (OpenSSH) 7.5p1 到 7.5:p1

[**Download**](https://github.com/OCSAF/freevulnsearch)