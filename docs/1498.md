# HawkScan:用于网站侦察和信息收集的安全工具

> 原文：<https://kalilinuxtutorials.com/hawkscan/>

*   **HawkScan** 是一款在网站上进行侦察和信息收集的安全工具。(python 2.x & 3.x)。
*   这个脚本在第一步使用“WafW00f”来检测晶片([https://github.com/EnableSecurity/wafw00f](https://github.com/EnableSecurity/wafw00f))
*   这个脚本使用“Sublist3r”来扫描子域([https://github.com/aboul3la/Sublist3r](https://github.com/aboul3la/Sublist3r))
*   这个脚本使用“waybacktool”来检入 way back machine([https://github.com/Rhynorater/waybacktool](https://github.com/Rhynorater/waybacktool))

**新闻**

**！**1.5 版
T3！如果网站满 JS 扫描时自动激活 JS(网站 2.0)
**！**添加 Dockerfile

**特性**

*   URL 模糊和目录/文件检测
*   在所有找到的文件上测试备份/旧文件(index.php.bak，index.php~ …)
*   检查标题信息
*   检查 DNS 信息
*   检查 whois 信息
*   用户代理随机或个人
*   提取文件
*   保留扫描的痕迹
*   检查网站中的@mail，检查@ mail 是否泄露
*   CMS 检测+版本和漏洞
*   子域检查器
*   备份系统(如果脚本停止，它在相同的地方再次采取)
*   晶片检测
*   添加个人前缀
*   自动更新脚本
*   扫描的自动或个人输出(scan.txt)
*   检查 Github
*   Recursif dir/file
*   使用验证 cookie 扫描
*   选项–profil 在扫描期间通过配置文件页面
*   HTML 报告
*   与 py2 和 py3 一起工作
*   如果应用程序不稳定，添加选项速率限制(–timesleep)
*   检入 waybackmachine
*   对晶圆的响应错误
*   检查数据库 firebaseio 是否存在并且可以访问
*   根据对网站的响应自动执行线程(如果 WAF 检测次数过多，则重新配置)。最大:30
*   在源代码页中搜索 S3 存储桶
*   如果检测到，测试 waf 旁路
*   测试是否可以使用“本地主机”主机进行扫描
*   Dockerfile
*   网站 2.0 上的活动 JavaScript(全 js)

**待办事项**

**P1 是最重要的**

*   JS 解析和分析[P1]
*   分析 html 代码网页[P1]
*   即时写作报告[P1]
*   检查 HTTP 头/ssl 安全性[P2]
*   毛茸茸的亚马逊鹦鹉 S3 水桶[P2]
*   通过某个代理的匿名路由(http/s 代理列表)[P2]
*   检查 pastebin [P2]
*   访问令牌[P2]
*   检查源代码并验证 Github [P2]中的泄漏或敏感数据
*   检查 phpmyadmin 版本[P3]
*   扫描 API 端点/信息泄漏[尽快]

**用途**

pip(3)install-r requirements . txt
如果 pip3 有问题:
sudo python 3-m pip install-r requirements . txt

用法:hawks can . py[-h][-u URL][-w WORDLIST][-s 子域] [-t 线程] [-a 用户代理][–重定向] [-r]

**可选参数:**
-h，–help 显示此帮助信息并退出
-u URL 要扫描的 URL【必需】
-w WORDLIST 用于 URL 模糊化的 WORDLIST。default:dico . txt
-s Subdomain s Subdomain tester
-t THREAD 用于 URL 模糊化的线程数。默认:20
-a USER _ AGENT Choice USER-AGENT
-redirect For scan with redirect response(301/302)
-r Recursive dir/files
-p PREFIX 在 wordlist 中添加前缀进行扫描
-o OUTPUT Output 到 site_scan.txt(默认在网站目录中)
-b 添加备份文件扫描如' example . com/~ example/，exemple.com/ex.php.bak…'但更长
-H HEADER _ modify HEADER
-EXCLUDE 定义 max:30
–自动更新的更新

**例题**

//基础
python hawks can . py-u https://www.exemple.com-w dico _ extra . txt
//带重定向
python hawks can . py-u https://www.exemple.com-w dico _ extra . txt-t 5–重定向
//带备份文件扫描
python hawks can . py-u https://www.exemple.com-w dico _ extra . txt-t 5-b
//带排除页面
python hawks can . py-u https://www.exemple.com-w dico _ extra . txt-t 5–排除 https://www.exemple.com/profile.php?id=1
//带

**信用:**莱诺&血滴子&赛博 _Ph4ntoM

[**Download**](https://github.com/c0dejump/HawkScan)