# 使用暴力获取站点仪表板的工具

> 原文：<https://kalilinuxtutorials.com/cangibrina-tool-obtain-dashboard/>

Cangibrina 是一个多平台设备，这意味着利用暴力获取网站的仪表板，包括 wordlist、google、nmap 和 robots.txt。

它通过允许你检查利用 TOR 网络来鼓励你伪装你的 IP 传送。它影响的网络索引是 Google 和 DuckDuckGo。它同样可以让您利用定制的客户端专家字符串进行检查。

尽管有 Nmap 和 TOR，它使用的 Python 包有 automate、PySocks、BeautifulSoup4、html5lib。你同样可以指示呆子去寻找它发现的任何权威仪表板，包括另一层安全。

## **对卡吉布丽娜**的要求

*   Python 2.7
*   使机械化
*   PySocks
*   beautifulsoup4
*   html5lib
*   nmap(–nmap)
*   TOR (–tor)

**也读作[E013——微软 Windows 的 WiFi 密码窃取者](http://kalilinuxtutorials.com/e013-wifi-password-stealer/)**

### **如何在 Linux 中安装 Cangibrina？**

`**git clone http://github.com/fnk0c/cangibrina.git 
cd cangibrina 
pip install -r requirements.txt**`

#### **用法** 

```
usage: cangibrina.py [-h] -u U [-w W] [-t T] [-v] [--ext EXT] [--user-agent]
[--tor] [--search] [--dork DORK] [--nmap [NMAP]]

Fast and powerful admin finder

optional arguments:
-h, --help show this help message and exit
-u U target site
-w W set wordlist (default: wl_medium)
-t T set threads number (default: 5)
-v enable verbose
--ext EXT filter path by target extension
--user-agent modify user-agent
--sub-domain search for sub domains instead of directories
--tor set TOR proxy
--search use google and duckduckgo to search
--dork DORK set custom dork
--nmap [NMAP] use nmap to scan ports and services
```

#### **例句**

```
python cangibrina.py -u facebook.com**
**python cangibrina.py -u facebook.com -v	
python cangibrina.py -u facebook.com -w /root/diretorios.txt -t 10 -v
python cangibrina.py -u facebook.com --search -v
python cangibrina.py -u facebook.com --search --dork 'site:facebook.com inurl:login'
python cangibrina.py -u facebook.com -v --nmap
python cangibrina.py -u facebook.com -v --nmap 'sudo nmap -D 127.0.0.1 -F facebook.com'
python cangibrina.py -u facebook.com --user-agent
python cangibrina.py -u facebook.com --ext php**
[IMPORTANT] DORK MUST BE WRITE BETWEEN QUOTES !
[Example] 'inurl:login.php'
```

[![](img/a51de913dc60eee505c4a68651ee8e4d.png)](https://github.com/fnk0c/cangibrina)