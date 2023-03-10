# SPF–针对网络钓鱼练习的 SpeedPhish 框架

> 原文：<https://kalilinuxtutorials.com/spf-speedphish-framework/>

SPF 只不过是一个 SpeedPhish 框架工具，使用 python 设计，允许快速侦察和部署简单的社会工程网络钓鱼练习。

## **对 SPF 的要求**

1.  dnspython
2.  扭曲的
3.  幻象

**亦读 [幽灵钓鱼者——无线&以太网攻击软件应用](https://kalilinuxtutorials.com/ghost-phisher-wireless-attack/)**

## **如何安装 SPF？**

运行以下命令安装 SPF 工具；

```
pip install dnspython
pip install pycrypto

apt-get install python-twisted-web
apt-get install phantomjs

git clone --recursive https://github.com/tatanus/SPF.git
```

## **RunningSPF**

```
usage: spf.py [-h] [-f <list.txt>] [-C <config.txt>] [--all] [--test] [-e]
              [-g] [-s] [--simulate] [-w] [-W] [-d <domain>]
              [-c <company's name>] [--ip <IP address>] [-v] [-y]

optional arguments:
  -h, --help           show this help message and exit
  -d <domain>          domain name to phish
  -c <company's name>  name of company to phish
  --ip <IP address>    IP of webserver defaults to [192.168.1.124]
  -v, --verbosity      increase output verbosity

input files:
  -f <list.txt>        file containing list of email addresses
  -C <config.txt>      config file

enable flags:
  --all                enable ALL flags... same as (-e -g -s -w)
  --test               enable all flags EXCEPT sending of emails... same as
                       (-e -g --simulate -w -y -v -v)
  -e                   enable external tool utilization
  -g                   enable automated gathering of email targets
  -s                   enable automated sending of phishing emails to targets
  --simulate           simulate the sending of phishing emails to targets
  -w                   enable generation of phishing web sites
  -W                   leave web server running after termination of spf.py

misc:
  -y                   automatically answer yes to all questions
```

## **执行:**

```
cd spf
python spf.py --test -d example.com
```

**或者只是测试网站:**

```
cd spf
python web.py default.cfg
```

## **样本视频**

**德比康 2015 视频**

[https://www.youtube.com/embed/uyUyD1hwL9k?feature=oembed](https://www.youtube.com/embed/uyUyD1hwL9k?feature=oembed)

**BsidesLV 2015 视频**

[https://www.youtube.com/embed/TtgJ3DaMtAo?feature=oembed](https://www.youtube.com/embed/TtgJ3DaMtAo?feature=oembed)

**BsidesKnox 2015 视频**

[https://www.youtube.com/embed/85QQwOduH6A?feature=oembed](https://www.youtube.com/embed/85QQwOduH6A?feature=oembed)

**样品使用视频**

[https://www.youtube.com/embed/wMPlO41lo80?feature=oembed](https://www.youtube.com/embed/wMPlO41lo80?feature=oembed)

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/tatanus/SPF)