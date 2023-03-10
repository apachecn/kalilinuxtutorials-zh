# dnsReaper:攻击者、Bug 赏金猎人和蓝队的子域接管工具！

> 原文：<https://kalilinuxtutorials.com/dnsreaper/>

[![](img/944cd09ca16398c025afb63b34ae12d4.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEipto8t3cxiYROFfCnVie9xM9JO5htfHeOuiTyFsap5kDjyJZpcLZDvGA_URqlFbq2r40a81cVkZoqJsYyuIDjviBqLUAa-T_cfoX31V5ZVu4WlPWn0rVEmkZaw9ZFptu1t54XTRCTfmNItACcVpPUVH-kR8HE-TYq_SLXAK-7A4oG9xE73QCfLr4kE/s728/dns-yellow.png)

**DNS Reaper** 是另一个子域名接管工具，但重点是准确性、速度和我们武库中的签名数量！

我们每秒可以扫描大约 50 个子域，用超过 50 个接管签名测试每个子域。这意味着大多数组织可以在不到 10 秒的时间内扫描其整个 DNS 资产。

### 你可以使用 DNS Reaper 作为攻击者或 bug 猎人！

您可以通过在文件中提供一个域列表或在命令行上提供一个域来运行它。然后，DNS Reaper 将扫描带有所有签名的域名，生成一个 CSV 文件。

### 可以用 DNS Reaper 做防御者！

你可以运行它，让它为你获取你的 DNS 记录！是的，这是正确的，你可以运行它与凭证和测试您所有的域配置快速而容易。DNS Reaper 将连接到 DNS 提供商并获取您的所有记录，然后测试它们。

我们目前支持 AWS Route53、Cloudflare 和 Azure。关于添加您自己的提供者的文档可以在这里找到

### 可以用 DNS Reaper 当 DevSecOps Pro！

Punk Security 是一家 DevSecOps 公司，DNS Reaper 植根于现代安全最佳实践。

您可以在管道中运行 DNS Reaper，向它提供一个您打算提供的域列表，如果它检测到接管是可能的，它将非零退出。你可以在接管发生之前就阻止它们！

## 用法

要运行 DNS Reaper，可以使用 docker 镜像或者用 python 3.10 运行。

**结果将在输出中返回，更多详细信息将在本地“results.csv”文件中提供。我们也支持 json 输出作为一个选项。**

### 用 docker 运行它

**码头工运行 punk security/dnsreopen–help**

用 python 运行它

**pip install-r requirements . txt
python main . py–help**

### 常见命令

*   扫描 aws 帐户:`**docker run punksecurity/dnsreaper aws --aws-access-key-id <key> --aws-access-key-secret <secret>**`有关更多信息，请参阅 AWS 提供程序的文档
*   扫描文件中的所有域:`**docker run -v $(pwd):/etc/dnsreaper punksecurity/dnsreaper file --filename /etc/dnsreaper/<filename>**`
*   扫描单个域`**docker run punksecurity/dnsreaper single --domain <domain>**`
*   扫描单个域并输出到 stdout:您应该使用>`**docker run** **punksecurity/dnsreaper single --domain <domain> --out stdout --out-format=json > output**`重定向 stderr 输出或保存 stdout 输出

**完全使用**

```
 **    ____              __   _____                      _ __
     / __ \__  ______  / /__/ ___/___  _______  _______(_) /___  __
    / /_/ / / / / __ \/ //_/\__ \/ _ \/ ___/ / / / ___/ / __/ / / /
   / ____/ /_/ / / / / ,<  ___/ /  __/ /__/ /_/ / /  / / /_/ /_/ /
  /_/    \__,_/_/ /_/_/|_|/____/\___/\___/\__,_/_/  /_/\__/\__, /
                                         PRESENTS         /____/
                          DNS Reaper ☠️
         Scan all your DNS records for subdomain takeovers!
```

**用法:
。\main.py provider【选项】
输出:
结果输出到屏幕和(默认)results.csv
帮助:
。\ main . py–help
providers:
AWS–通过从 AWS Route53
azure 获取域来扫描多个域–通过从 Azure DNS 服务获取域来扫描多个域
BIND–从 DNS 绑定区域文件读取域，或多个
cloudflare 的路径–通过从 Cloudflare
文件获取域来扫描多个域–从文件读取域， 每行一个
single–通过在命令行上提供一个域来扫描单个域
zone transfer–通过 DNS zone transfer 获取记录来扫描多个域
位置参数:
{aws，azure，bind，cloudflare，file，single，zonetransfer}
选项:
h， –帮助显示此帮助消息并退出
out OUT 输出文件(默认:结果)–使用“stdout”输出
out-format {csv，json}
解析器解析器
提供自定义 DNS 解析器(或多个以逗号分隔)
并行度并行度
要并行测试的域数量–太高，您可能会看到奇数 DNS 结果(默认:30)
禁用-可能不检查可能的条件
启用-不太可能检查更多条件， 但是误报率很高
签名签名
仅使用此签名扫描(接受多个)
EXCLUDE-SIGNATURE EXCLUDE _ SIGNATURE
不使用此签名扫描(接受多个)
检测时管道出口非零(用于使管道失败)
v，–verbose-v 表示详细， -vv for extra verbose
no colour 关闭彩色文本
aws:
通过从 AWS route 53
AWS-ACCESS-KEY-ID AWS _ ACCESS _ KEY _ ID
可选
AWS-ACCESS-KEY-SECRET AWS _ ACCESS _ KEY _ SECRET
可选 azure:
通过从 Azure DNS 服务提取扫描多个域
AZ-SUBSCRIPTION-ID AZ _ SUBSCRIPTION _ ID【t4t 或路径到多个
BIND-ZONE-FILE BIND _ ZONE _ FILE
Required
cloudflare:
通过从 cloud flare 获取域来扫描多个域
cloud flare-TOKEN cloud flare _ TOKEN
Required
FILE:
从文件中读取域，每行一个
FILENAME FILENAME Required
single:
通过在命令行上提供域来扫描单个域
DOMAIN DOMAIN Required
ZONE transfer:】**

[**Download**](https://github.com/punk-security/dnsReaper)