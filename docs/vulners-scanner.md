# 漏洞扫描器:基于 Vulners.com 审计 API 的漏洞扫描器

> 原文：<https://kalilinuxtutorials.com/vulners-scanner/>

vulneraners-Scanner 是一个基于 PoC 主机的漏洞扫描器，它使用 vulners.com API。检测操作系统，收集已安装的软件包并检查其中的漏洞。它目前支持收集基于 Debian(Debian，kali，kali)和基于 Rhel(red hat，centos，fedora)的操作系统的包。

实验支持检测运行 docker 容器中的漏洞(仅限高级脚本)。需要在 **linuxScanner.py** 中将`**checkDocker=False**`改为`**checkDocker=True**`来激活它

**也读[Darling–Darwin/Mac OS 仿真层 For Linux](https://kalilinuxtutorials.com/darling-mac-os-linux/)**

## **如何使用 Vulners-Scanner**

*   懒惰扫描程序展示 vulners.com API 能力的最简单的脚本。只需运行脚本，它将返回所有发现的漏洞:

```
# git clone https://github.com/videns/vulners-scanner
# cd vulners-scanner
# ./lazyScanner.py
OS Name - debian, OS Version - 8
Total provided packages: 315**
**{
    "data": {
        "vulnerabilities": [
            "DSA-3644",
            "DSA-3626"
        ],
        "packages": {            
            "openssh-client 1:6.7p1-5+deb8u2 amd64": {
                "DSA-3626": [
                    {
                        "bulletinVersion": "1:6.7p1-5+deb8u3",
                        "providedVersion": "1:6.7p1-5+deb8u2",
                        "bulletinPackage": "openssh-client_1:6.7p1-5+deb8u3_all.deb",
                        "result": true,
                        "operator": "lt",
                        "OSVersion": "8",
                        "providedPackage": "openssh-client 1:6.7p1-5+deb8u2 amd64"
                    }
                ]
            }
            "fontconfig-config 2.11.0-6.3 all": {
                "DSA-3644": [
                    {
                        "bulletinVersion": "2.11.0-6.3+deb8u1",
                        "providedVersion": "2.11.0-6.3",
                        "bulletinPackage": "fontconfig-config_2.11.0-6.3+deb8u1_all.deb",
                        "result": true,
                        "operator": "lt",
                        "OSVersion": "8",
                        "providedPackage": "fontconfig-config 2.11.0-6.3 all"
                    }
                ]
            },
            "libfontconfig1 2.11.0-6.3 amd64": {
                "DSA-3644": [
                    {
                        "bulletinVersion": "2.11.0-6.3+deb8u1",
                        "providedVersion": "2.11.0-6.3",
                        "bulletinPackage": "libfontconfig1_2.11.0-6.3+deb8u1_all.deb",
                        "result": true,
                        "operator": "lt",
                        "OSVersion": "8",
                        "providedPackage"**: "libfontconfig1 2.11.0-6.3 amd64"
     **}
                ]
            }
        }
    },
    "result": "OK"
}
Vulnerabilities:
DSA-3644
DSA-3626
```

*   高级扫描仪。用几种方法检测操作系统。支持运行 docker 容器扫描(需要在文件中手动激活)

```
# git clone https://github.com/videns/vulners-scanner
# cd vulners-scanner
# ./linuxScanner.py

             _
__   ___   _| |_ __   ___ _ __ ___
\ \ / / | | | | '_ \ / _ \ '__/ __|
 \ V /| |_| | | | | |  __/ |  \__ \
  \_/  \__,_|_|_| |_|\___|_|  |___/

==========================================
Host info - Host machine
OS Name - Darwin, OS Version - 15.6.0
Total found packages: 0
==========================================
Host info - docker container "java:8-jre"
OS Name - debian, OS Version - 8
Total found packages: 166
Vulnerable packages:
    libgcrypt20 1.6.3-2+deb8u1 amd64
        DSA-3650 - 'libgcrypt20 -- security update', cvss.score - 0.0
    libexpat1 2.1.0-6+deb8u2 amd64
        DSA-3597 - 'expat -- security update', cvss.score - 7.8
    perl-base 5.20.2-3+deb8u4 amd64
        DSA-3628 - 'perl -- security update', cvss.score - 0.0
    gnupg 1.4.18-7+deb8u1 amd64
        DSA-3649 - 'gnupg -- security update', cvss.score - 0.0
    gpgv 1.4.18-7+deb8u1 amd64
        DSA-3649 - 'gnupg -- security update', cvss.score - 0.0
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/vulnersCom/vulners-scanner)