# WAFw00f:识别保护网站的 Web 应用程序防火墙(WAF)产品并采集其指纹

> 原文：<https://kalilinuxtutorials.com/wafw00f-2/>

[![WAFw00f : Identify & Fingerprint Web Application Firewall (WAF) Products Protecting A Website](img/90f43aca81a62b30c10a6f84841bd1df.png "WAFw00f : Identify & Fingerprint Web Application Firewall (WAF) Products Protecting A Website")](https://4.bp.blogspot.com/-9xI_8XX5B6g/XNwDA7pIgdI/AAAAAAAAAV8/39k2DshfWy8SnANrZAtqpQERBv0sDXsrwCLcBGAs/s1600/wafw00f%25281%2529.png)

**WAFW00F** 识别并采集网络应用防火墙(WAF)产品的指纹。为了发挥它的魔力，WAFW00F 做了以下事情:

*   发送一个普通的 HTTP 请求并分析响应；这确定了许多 WAF 解决方案。
*   如果不成功，它会发送许多(潜在的恶意)HTTP 请求，并使用简单的逻辑来推断它是哪个 WAF。
*   如果还是不成功，它会分析之前返回的响应，并使用另一种简单的算法来猜测 WAF 或安全解决方案是否正在积极响应我们的攻击。

您还可以使用各种方法检查 [**是否是该网站安全的**](https://gbhackers.com/how-to-check-if-a-website-is-malicious/) 。

**也可阅读-[Pe-Sieve:识别&转储各种潜在恶意植入](https://kalilinuxtutorials.com/pe-sieve-malicious-implants/)**

它检测到一些 waf。使用`-l`选项查看能够检测到哪些 waf，运行 WAFW00F。在编写时，输出如下:

$ waf w00 f-l

waf w00 f–Web 应用防火墙检测工具

可以对这些 waf 进行测试:
block dos(block dos)
Armor Defense(Armor)
ACE XML Gateway(Cisco)
Malcare(in activ)
RS Firewall(RSJoomla！)
perimerx(perimerx)
Varnish(OWASP)
Barracuda 应用防火墙(Barracuda Networks)
anquan Bao(anquan Bao)
net continuum(Barracuda Networks)
HyperGuard(Art of Defense)
in capsula(imper va Inc .)
safe dog(safe dog)
NevisProxy(AdNovum)
SEnginx(东软)
BitNinja(
Cloudfront(亚马逊)
aeSecure(aeSecure)
eEye securei is(beyond trust)
virus die(virus die LLC)
dos arrest(dos arrest Internet Security)
site ground(site ground)
于闯之盾(Yunaq)
云索(Yunsuo)
纳克斯(NBS Systems)
UTM Web Protection(Sophos)
方法(Approach)
网络规模
灰巫师(Grey Wizard)
神盾局安全(一元插件)
ASP.NET 通用防护(微软)
CacheWall (Varnish)
表情引擎(EllisLab)
气闸(Phion/Ergon)
WatchGuard(WatchGuard Technologies)
WP Cerber Security(Cerber Tech)
yun jiasu(百度云计算)
DenyALL (Rohde & Schwarz 网络安全)
AnYu
WebSEAL (IBM)
绿盟科技(NSFocus Global Inc .)
360 网展宝(360 Technologies)
Squarespace(Squarespace)
imper va SecureSphere
blue don(IST 蓝登)
阿里云盾(阿里云计算)
Wordfence (Feedjit)
帕洛阿尔托下一代防火墙(帕洛阿尔托网络)
腾讯
AWS 弹性负载均衡器(亚马逊)
cloud BRIC(Penta Security)
stack path(stack path)
URLScan(微软)
Sucuri(Sucuri Inc .)
TransIP Web 防火墙(TransIP)
on message Shield(BlackBaud)
distilt Networks
pro fence(armor logic)
ModSecurity(spider labs)
forti Web(Fortinet)
CdnNS 应用网关(CdnNS/WdidcNet)
data power(IBM)
web knight(AQTRONIX)
BIG-IP 应用安全管理器(F5 Networks)
Barikode(伦理忍者)
Zen edge(Zen edge)
SonicWall(戴尔)
dot defender(Applicure Technologies)
USP 安全入口服务器
AppWall (Radware)

我如何使用它？

如需帮助，请使用–help 选项。基本用法是将 URL 作为参数传递给它。示例:

**$ WAF w00 f https://example.org

WAF w00 f——Web 应用防火墙检测工具

检查 https://example.org
网站 https://example.org 在 Edgecast(威瑞森数字媒体)WAF 之后。
请求数量:1**

如何安装它？

以下内容应该可以解决问题:

**python setup.py 安装**

[**Download**](https://github.com/EnableSecurity/wafw00f)