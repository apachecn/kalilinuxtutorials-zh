# 用于识别错误配置的 CloudFront 域的工具

> 原文：<https://kalilinuxtutorials.com/cloudfrunt-misconfigured-domains/>

CloudFrunt 是一个用于识别错误配置的 CloudFront 域的工具。CloudFront 是亚马逊网络服务(AWS)给出的内容交付网络(CDN)。CloudFront 客户端进行“分发”,提供来自特定来源的内容(例如，一个 S3 容器)。

每一个 CloudFront 发行版都有一个显著的端点，客户端可以将它们的 DNS 记录指向这个端点(例如 d111111abcdef8.cloudfront.net)。使用特定分布的大部分区域应记录在该分布选项的“备用域名(CNAMEs)”字段中。

当 CloudFront 端点收到请求时，它不会从相关的发行版提供内容。相反，CloudFront 利用需求的主机头来决定使用哪个发行版。这意味着两件事:

*   如果主机报头不协调所提议的循环的“备用域名(CNAMEs)”字段中的条目，则需求将不足。
*   在主机头中包含特定区域的任何其他发行版都将获得需求并定期对其做出反应。

**也读作 [最好的 SQL 注入工具](http://kalilinuxtutorials.com/sql-injection/)**

这就是空间被劫持的原因。在很多情况下，CloudFront 客户端会忽略列出主机头中可能包含的所有重要区域。例如:

*   域名“test . disloops.com”是一项 CNAME 记录，重点是“dissolops . com”。
*   “dissolo PS . com”区域是为了利用 CloudFront 发行版而建立的。
*   由于“test.disloops.com”未添加到分发的“备用域名(CNAMEs)”字段，因此对“test.disloops.com”的请求将失败。
*   另一个客户端可以进行 CloudFront 分发，并在“备用域名(CNAMEs)”字段中包含“test.disloops.com”来劫持该域。

这暗示了一个显著的终点，即云锋绑定到一个单独的环流是完全没有好处的。对一个特定的 CloudFront 子域的请求并不局限于与之相关的发行版。

### **安装云安装**

```
$ git clone --recursive https://github.com/MindPointGroup/cloudfrunt
$ pip install -r requirements.txt
```

CloudFrunt 希望将 *dnsrecon* 脚本克隆到一个名为 *dnsrecon* 的子目录中。

### **用法**

```
cloudfrunt.py [-h] [-l TARGET_FILE] [-d DOMAINS] [-o ORIGIN] [-i ORIGIN_ID] [-s] [-N]

-h, --help                      Show this message and exit
-s, --save                      Save the results to results.txt
-N, --no-dns                    Do not use dnsrecon to expand scope
-l, --target-file TARGET_FILE   File containing a list of domains (one per line)
-d, --domains DOMAINS           Comma-separated list of domains to scan
-o, --origin ORIGIN             Add vulnerable domains to new distributions with this origin
-i, --origin-id ORIGIN_ID       The origin ID to use with new distributions
```

### **例子**

```
$ python cloudfrunt.py -o cloudfrunt.com.s3-website-us-east-1.amazonaws.com -i S3-cloudfrunt -l list.txt

 CloudFrunt v1.0.4

 [+] Enumerating DNS entries for google.com
 [-] No issues found for google.com

 [+] Enumerating DNS entries for disloops.com
 [+] Found CloudFront domain --> cdn.disloops.com
 [+] Found CloudFront domain --> test.disloops.com
 [-] Potentially misconfigured CloudFront domains:
 [#] --> test.disloops.com
 [+] Created new CloudFront distribution EXBC12DE3F45G
 [+] Added test.disloops.com to CloudFront distribution EXBC12DE3F45G
```

[![](img/a51de913dc60eee505c4a68651ee8e4d.png)](https://github.com/MindPointGroup/cloudfrunt#installation)