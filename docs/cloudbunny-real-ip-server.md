# cloud bunny——cloud bunny 是一个捕捉服务器真实 IP 的工具

> 原文：<https://kalilinuxtutorials.com/cloudbunny-real-ip-server/>

CloudBunny 是一个工具，用于捕获使用 WAF 作为代理或保护的服务器的真实 IP。在这个工具中，我们使用了三个搜索引擎来搜索领域信息:Shodan、Censys 和 Zoomeye。 CloudBunny 是一个捕获使用 WAF 作为代理或保护的源服务器的工具。

## 【CloudBunny 如何工作

在这个工具中，我们使用了三个搜索引擎来搜索领域信息:Shodan、Censys 和 Zoomeye。要使用您需要的工具 API 键，您可以选择以下链接:

```
Shodan** - https://account.shodan.io/
**Censys** - https://censys.io/account/api
**ZoomEye** - https://www.zoomeye.org/profile 
```

**注意**:在 Zoomeye 中，你需要输入登录名和密码，它会生成一个动态 api 密匙，我已经为你做了这项工作。只需输入您的登录名和密码。

之后，您需要将凭证放在 **api.conf** 文件中。

安装要求:

```
$ sudo pip install -r requirements.txt
```

**也可阅读 [Hackertarget:工具和网络情报帮助组织进行攻击面发现](https://kalilinuxtutorials.com/hackertarget-attack-surface-discovery/)**

## **用途**

默认情况下，该工具会在所有搜索引擎上进行搜索(您可以通过参数进行设置)，但是您需要如上所述输入凭证。加载凭证并安装要求后，执行:

```
$ python cloudbunny.py -u securityattack.com.br 
```

查看我们的帮助区域:

```
$ python cloudbunny.py -h 
```

为您选择的域名更改**securityattack.com.br**。

## **例子**

```
$ python cloudbunny.py -u site_example.com.br

	            /|      __  
	           / |   ,-~ /  
	          Y :|  //  /    
	          | jj /( .^  
	          >-"~"-v"  
	         /       Y    
	        jo  o    |  
	       ( ~T~     j   
	        >._-' _./   
	       /   "~"  |    
	      Y     _,  |      
	     /| ;-"~ _  l    
	    / l/ ,-"~    \  
	    \//\/      .- \  
	     Y        /    Y*  
	     l       I     ! 
	     ]\      _\    /"\ 
	    (" ~----( ~   Y.  )   
	~~~~~~~~~~~~~~~~~~~~~~~~~~    
CloudBunny - Bypass WAF with Search Engines 
Author: Eddy Oliveira (@Warflop)
https://github.com/Warflop 

[+] Looking for target on Shodan...
[+] Looking for target on Censys...
[+] Looking for certificates on Censys...
[+] Looking for target on ZoomEye...
[-] Just more some seconds...

+---------------+------------+-----------+----------------------------+
|   IP Address  |    ISP     |   Ports   |        Last Update         |
+---------------+------------+-----------+----------------------------+
|  55.14.232.4  | Amazon.com | [80, 443] | 2018-11-02T16:02:51.074543 |
| 54.222.146.40 | Amazon.com |    [80]   | 2018-11-02T10:16:38.166829 |
| 18.235.52.237 | Amazon.com | [443, 80] | 2018-11-08T01:22:11.323980 |
| 54.237.93.127 | Amazon.com | [443, 80] | 2018-11-05T15:54:40.248599 |
| 53.222.94.157 | Amazon.com | [443, 80] | 2018-11-06T08:46:03.377082 |
+---------------+------------+-----------+----------------------------+
    We may have some false positives :) 
```

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/Warflop/CloudBunny) ** *您可以在 [Linkedin](https://www.linkedin.com/company/gbhackers/) 、 [Twitter](https://twitter.com/GbhackerOn) 、[脸书](https://www.facebook.com/gbhackersadmin)上关注我们的日常网络安全更新，您还可以在线参加[最佳网络安全课程](https://ethicalhackersacademy.com/)以保持自我更新。***