# CertCrunchy——愚蠢的侦察工具，使用 SSL 证书中的数据来查找潜在的主机名

> 原文：<https://kalilinuxtutorials.com/certcrunchy-data-ssl-certificates/>

CertCrunchy 只是一个愚蠢的 python 脚本，它要么从在线来源检索基于 SSL 证书的数据，目前是[https://crt.sh/](https://crt.sh/)、[https://certdb.com/](https://certdb.com/)、[https://sslmate.com/certspotter/](https://sslmate.com/certspotter/)和 [https://censys.io](https://censys.io) ，要么给定一个 IP 范围，它将尝试从 SSL 证书中提取主机信息。如果你想使用 Censys.io，你需要注册一个 API 密匙。

![](img/75ad274895061f11e72bbc4483481b0a.png)

**也读作[Hcxdumptool——从无线局域网设备中捕获数据包的小工具](https://kalilinuxtutorials.com/hcxdumptool-wlan-devices/)**

## **如何安装 CertCrunchy**

```
git clone https://github.com/joda32/CertCrunchy.git
cd CertCrunchy
sudo pip3 install -r requirements.txt 
```

## **怎么用？**

非常简单——获取特定域的主机名

*   **-D** 获取域名列表的主机名(只需将其填充到一个以行分隔的文本文件中)
*   **-i** 从网络块/ ip 范围(如 192.168.0.0/24)内的主机检索和解析证书
*   线程计数，使东西更快，但不要过度
*   **-O** 以秒为单位设置 HTTP api 请求的超时时间(默认为 3 秒)
*   **-o** 输出文件名
*   **-f** 输出格式 csv 或 json，默认为 csv

## **API 键&配置**

所有 api 密钥都存储在 api_keys.py 文件中，下面是需要 API 密钥的受支持 API 的列表。

*   [Censys.oi](https://censys.io)
*   [VirusTotal](https://www.virustotal.com/en/documentation/public-api/)
*   [被动总计](https://community.riskiq.com/registration)

[![https://github.com/Nekmo/dirhunt](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/joda32/CertCrunchy)