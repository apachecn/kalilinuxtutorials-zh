# Killshot:信息收集工具

> 原文：<https://kalilinuxtutorials.com/killshot-information-gathering-tool/>

KillShot 是一个渗透测试框架，信息收集工具和网站漏洞扫描器。

您可以使用此工具对您的网站进行蜘蛛搜索，获取重要信息，并使用 what web-host-traceroute-dig-凶-wafw00f 自动收集信息，或者使用 cms 漏洞扫描器和 WebApp Vul 扫描器识别 Cms 并找到您网站中的漏洞，您还可以使用它通过 nmap 和 unicorn 自动扫描多种类型的扫描。有了这个工具，你可以生成 PHP 简单的后门，手动上传，并使用它连接到目标。

这个工具承载了一个简单的 Ruby Fuzzer 在 VULSERV.exe 和 Linux 上测试的 Log clear 脚本来改变登录路径蜘蛛的内容，可以帮助你找到站点的参数并扫描 xss 和 sql。

**也读作**[**xs strike——最先进的 XSS 探测套件**](https://kalilinuxtutorials.com/xsstrike-xss-detection-suite/)

## **Killshot 菜单**

```
{0} Spider 
{1} Web technologie 
{2} WebApp Vul Scanner
{3} Port Scanner
{4} CMS Scanner
{5} Fuzzers 
{6} Cms Exploit Scanner
{7} Backdoor Generation
{8} Linux Log Clear
```

## **WebApp Vul 扫描器**

```
{1} Xss scanner
{2} Sql Scanner
{3} Tomcat RCE
```

## **端口扫描仪**

```
 `[0] Nmap Scan
 [1] Unicorn Scan
Nmap Scan 
 [2] Nmap Os Scan 
 [3] Nmap TCP Scan
 [4] Nmap UDB Scan 
 [5] Nmap All scan
 [6] Nmap Http Option Scan 
 [7] Nmap Live target In Network
Unicorn Scan
[8] Services OS 
[9] TCP SYN Scan on a whole network 
[01] UDP scan on the whole network
```

## **借壳代**

```
 **{1} Generate Shell
 {2} Connect Shell
```

## **用途**

```
1 ----- Help Command 
[site]  MAKE YOUR TARGET
[help] show this MESSAGE
[exit] show this MESSAGE
2 ------ Site command 
Put your target www.example.com
without the http
```

## **Linux 设置**

```
git clone https://github.com/bahaabdelwahed/killshot
cd killshot
ruby setup.rb (if setup show any error just try to install the gems/tool manual )
ruby killshot.rb
```

## **视频教程**

[https://www.youtube.com/embed/SEGRh86J6vk?feature=oembed](https://www.youtube.com/embed/SEGRh86J6vk?feature=oembed)

[https://www.youtube.com/embed/QPF-rppYSOY?feature=oembed](https://www.youtube.com/embed/QPF-rppYSOY?feature=oembed)

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/bahaabdelwahed/killshot)