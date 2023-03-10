# can gibrina——快速而强大的仪表板(管理)查找工具

> 原文：<https://kalilinuxtutorials.com/cangibrina-dashboard-admin-finder/>

Cangibrina 是一个多平台工具，旨在通过暴力破解 wordlist、google、nmap 和 robots.txt 来获取站点仪表板

## **要求:**

*   Python 2.7
*   使机械化
*   PySocks
*   beautifulsoup4
*   html5lib
*   nmap(–nmap)
*   TOR (–tor)

**也可理解为[pwn back–Burp Extender 插件，使用 Wayback 机器](https://kalilinuxtutorials.com/pwnback-burp-extender-plugin/)** 生成网站的站点地图

## **Cangibrina 安装**

### **Linux**

```
git clone https://github.com/fnk0c/cangibrina.git
cd cangibrina
pip install -r requirements.txt
```

### **用法**

```
usage: cangibrina.py [-h] -u U [-w W] [-t T] [-v] [--ext EXT] [--user-agent]
                     [--tor] [--search] [--dork DORK] [--nmap [NMAP]]

Fast and powerful admin finder

optional arguments:
  -h, --help     show this help message and exit
  -u U           target site
  -w W           set wordlist (default: wl_medium)
  -t T           set threads number (default: 5)
  -v             enable verbose
  --ext EXT      filter path by target extension
  --user-agent   modify user-agent
  --sub-domain   search for sub domains instead of directories
  --tor          set TOR proxy
  --search       use google and duckduckgo to search
  --dork DORK    set custom dork
  --nmap [NMAP]  use nmap to scan ports and services
```

## **例子**

```
python cangibrina.py -u facebook.com

python cangibrina.py -u facebook.com -v

python cangibrina.py -u facebook.com -w /root/diretorios.txt -t 10 -v

python cangibrina.py -u facebook.com --search -v

python cangibrina.py -u facebook.com --search --dork 'site:facebook.com inurl:login'

python cangibrina.py -u facebook.com -v --nmap

python cangibrina.py -u facebook.com -v --nmap 'sudo nmap -D 127.0.0.1 -F facebook.com'

python cangibrina.py -u facebook.com --user-agent

python cangibrina.py -u facebook.com --ext php

[IMPORTANT] DORK MUST BE WRITE BETWEEN QUOTES !
[Example] 'inurl:login.php'
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/fnk0c/cangibrina)