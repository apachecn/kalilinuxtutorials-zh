# Libssh-Scanner:用于识别易受 CVE 攻击的主机的脚本-2018-10933

> 原文：<https://kalilinuxtutorials.com/libssh-scanner-vulnerable-cve-2018-10933/>

**Libssh-Scanner** 是一个基于 python 的脚本，用于识别易受 CVE 攻击的主机-2018-10933。Libssh 扫描程序有两种模式:被动(横幅抓取)和主动(绕过验证)来验证漏洞的存在。默认情况下，libssh 扫描程序使用被动模式，但提供-a 参数，将使用主动模式，这将提供更准确的结果。

**也读作[Nameles——基于开源熵的无效流量检测&预竞价过滤](https://kalilinuxtutorials.com/nameles/)**

## **Libssh-扫描仪安装**

```
Run pip install -r requirements.txt within the cloned libssh-scanner directory.
```

## **帮助**

```
libssh Scanner - Find vulnerable libssh services by Leap Security (@LeapSecurity)**

**positional arguments:**
**target An ip address or new line delimited file containing**
**IPs to search for the vulnerability.**

**optional arguments:**
**-h, --help show this help message and exit**
**-v, --version show program's version number and exit**
**-p PORT, --port PORT Set port of SSH service**
**-a, --aggressive Identify vulnerable hosts by bypassing authentication
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/leapsecurity/libssh-scanner)