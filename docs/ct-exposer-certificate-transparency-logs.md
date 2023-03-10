# ct-exposer:一个通过搜索证书透明性日志来发现子域的 OSINT 工具

> 原文：<https://kalilinuxtutorials.com/ct-exposer-certificate-transparency-logs/>

ct-exposer 将查询给定域的 ct 日志，然后尝试对这些域进行 DNS 查找，以查看哪些域存在于 DNS 中。根据我的经验，到目前为止，我已经找到了许多子域名，这些子域名并没有在谷歌搜索中找到。

请记住，无法解析的域可能是旧域，也可能是仅限内部的域(例如，您需要访问内部 DNS 服务器来解析它们)。

证书透明性(CT)是一个实验性的 IETF 标准。它的目标是允许公众审核哪些证书是由证书颁发机构(CA)创建的。TLS 有一个弱点，它来自于您的浏览器隐式信任的大量 ca 列表。

如果这些 ca 中的任何一个恶意地为一个域创建一个新的证书，您的浏览器就会信任它。CT 为 TLS 证书信任增加了好处:公司可以监控谁在为他们拥有的域创建证书。

它还允许浏览器验证给定域的证书是否在公共日志记录中。这些日志最终成为渗透测试人员和红队的信息金矿。

## **ct 暴露用途**

```
usage: ct-exposer.py [-h] -d DOMAIN [-u] [-m]

optional arguments:
 -h, --help            show this help message and exit
 -d DOMAIN, --domain DOMAIN
 domain to query for CT logs, ex: domain.com
 -u, --urls            ouput results with https:// urls for domains that
 resolve, one per line.
 -m, --masscan         output resolved IP address, one per line. Useful for
 masscan IP list import "-iL" format. 
```

**亦读[Infog——信息搜集工具](https://kalilinuxtutorials.com/infog-information-gathering-tool/)**

## **示例输出**

```
python3 ct-exposer.py -d teslamotors.com
[+]: Downloading domain list...
[+]: Download of domain list complete.
[+]: Parsed 76 domain(s) from list.

[+]: Domains found:
205.234.27.243	adfs.teslamotors.com
104.92.115.166	akamaisecure.qualtrics.com
211.147.80.202	cn.auth.teslamotors.com
211.147.88.104	cnvpn.teslamotors.com
209.10.208.24	energystorage.teslamotors.com
209.11.133.110	epc.teslamotors.com
149.14.82.93	euvpn.teslamotors.com
209.11.133.50	extconfl.teslamotors.com
209.11.133.35	extissues.teslamotors.com
209.10.208.31	fleetview.teslamotors.com
64.125.183.134	leaseapp.teslamotors.com
64.125.183.134	leaseappde.teslamotors.com
209.11.133.11	lync.teslamotors.com
211.147.80.201	mycn-origin.teslamotors.com
205.234.27.211	origin-www45.teslamotors.com
205.234.31.120	owner-api.teslamotors.com
12.201.132.70	plcvpn.teslamotors.com
205.234.27.246	quickbase.teslamotors.com
104.86.205.249	resources.teslamotors.com
209.10.208.55	sdlcvpn.teslamotors.com
209.11.133.37	service.teslamotors.com
205.234.27.226	sftp.teslamotors.com
23.227.38.64	shop.eu.teslamotors.com
209.133.79.61	shop.teslamotors.com
23.227.38.64	shop.uk.teslamotors.com
205.234.27.197	smswsproxy.teslamotors.com
209.11.133.36	supercharger.teslamotors.com
209.133.79.59	suppliers.teslamotors.com
209.133.79.61	tesla.com
209.11.133.106	teslamotors.com
205.234.27.200	teslaplm-external.teslamotors.com
209.11.133.107	toolbox.teslamotors.com
209.10.208.20	trt.teslamotors.com
205.234.27.250	upload.teslamotors.com
209.10.208.27	us.auth.teslamotors.com
205.234.27.218	vpn.teslamotors.com
211.147.80.205	wechat.teslamotors.com
205.234.27.212	wsproxy.teslamotors.com
209.133.79.54	www-origin.teslamotors.com
104.86.216.34	www.teslamotors.com
209.11.133.61	xmail.teslamotors.com
211.147.80.203	xmailcn.teslamotors.com

[+]: Domains with no DNS record:
none	cdn02.c3edge.net
none	creditauction.teslamotors.com
none	evprd.teslamotors.com
none	imail.teslamotors.com
none	jupytersvn.teslamotors.com
none	leadgen.teslamotors.com
none	lockit.teslamotors.com
none	lockpay.teslamotors.com
none	neovi-vpn.teslamotors.com
none	origin-wte.teslamotors.com
none	referral.teslamotors.com
none	resources.tesla.com
none	securemail.teslamotors.com
none	shop.ca.teslamotors.com
none	shop.no.teslamotors.com
none	sip.teslamotors.com
none	sjc04p2staap04.teslamotors.com
none	sling.teslamotors.com
none	tesla3dx.teslamotors.com
none	testimail.teslamotors.com
none	toolbox-energy.teslamotors.com
none	vpn-node0.teslamotors.com
none	wd.s3.teslamotors.com
none	www-uat2.teslamotors.com
none	www45.teslamotors.com 
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/chris408/ct-exposer)