# Sub.sh:在线子域检测脚本

> 原文：<https://kalilinuxtutorials.com/sub-sh-online-subdomain-detect-script/>

[![Sub.sh : Online Subdomain Detect Script](img/aa278c15c78f9e3a5971cc2fbf36abff.png "Sub.sh : Online Subdomain Detect Script")](https://1.bp.blogspot.com/-2owD-69s75I/XZbg1R8zZrI/AAAAAAAACys/KdfnlB-5peM5bG2eKYfo7jaSNEE3eJsvACLcBGAsYHQ/s1600/Subdomain%2B%25281%2529.png)

**subsh**是一个在线检测子域的脚本。所以让我们来看看它的用法。

**脚本**

痛击 webscantest.com
。/sub . sh webscantest.com

![](img/70aee20bebf28cf615476b0ee01791f1.png)

**卷曲**

curl-s-L https://raw . githubusercontent . com/cihanmehmet/sub . sh/master/sub . sh | bash-s webscantest.com

![](img/86d175fc1ff3c3b03f8832ca003d23f3.png)

**也可阅读-[重组:随机更改 Win32/64 PE 文件，以便“更安全”地上传到恶意软件&沙盒网站](https://kalilinuxtutorials.com/recomposer-randomly-changes-win32-64/)**

**子域存活检查**

bash sub _ alive . sh bing.com
curl-s-L https://raw . githubusercontent . com/cihanmehmet/sub . sh/master/sub _ alive . sh | bash-s bing . com "

**需要 Fping】**

![](img/1fd2ed6d413d459e37096e5ec094a8b1.png)

**Nmap -sn(无端口扫描)扫描实时 IP 检测脚本**

**fping -f ip.txt**

**用法**用法`**bash nmap_sn.sh ip.txt**`

![](img/43edb72e61baf69f5e9535f1be3db59f.png)

#!/bin/bash

nmap-sn-iL $ 1 | grep " grep-Eo 的 Nmap 扫描报告"(25[0-5]|2[0-4][0-9]|[01]？[0-9][0-9]?).(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?).(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?).(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)" | sort-u | tee $ 1 . txt

echo " Detect IP $(WC-l $ 1 . txt | awk ' { print $ 1 } ')" " =>result _ $ { 1 } " " saved "
echo "文件位置:" $(pwd)/"result_$1 "

**样品用途**

**用法 1(平)平镖**

cat domains . txt | dnsgen –| fping | grep " alive " | cut-d " "-f1 > resolvers . txt

**用法 2(http probe)dart**

cat domains . txt | DNS gen –| http probe | cut-d "/"-F3 | sort-u | tee resolvers . txt

![](img/aca5d9df1bde7f9814e3d2da90507325.png)[**Download**](https://github.com/cihanmehmet/sub.sh)