# magicRecon:一个强大的 Shell 脚本，可以最大化目标的侦察和数据收集过程，并找到常见的漏洞

> 原文：<https://kalilinuxtutorials.com/magicrecon/>

[![magicRecon : A Powerful Shell Script To Maximize The Recon And Data Collection Process Of An Objective And Finding Common Vulnerabilities](img/b4463939d5debad3c29ab912237618d3.png "magicRecon : A Powerful Shell Script To Maximize The Recon And Data Collection Process Of An Objective And Finding Common Vulnerabilities")](https://1.bp.blogspot.com/-KPlW25cDlcg/YMTBx4Xz8sI/AAAAAAAAJfU/NTqq4xvjT1cXXm5hGzsglW97j0IIL3LlwCLcBGAsYHQ/s640/magicRecon.gif)

MagicRecon 是一个强大的 shell 脚本，可以最大化目标的侦察和数据收集过程，并找到常见的漏洞，所有这些都以有组织的方式以各种格式保存所获得的结果。

MagicRecon 的新版本拥有大量新工具，可以尽可能自动化从目标收集数据和搜索漏洞的过程。它还有一个菜单，用户可以在其中选择想要执行的选项。

这个新版本还有“安装依赖项”选项，用户可以通过它轻松安装运行 MagicRecon 所需的所有工具和依赖项。脚本代码以模块化的方式制作，因此任何用户都可以根据自己的喜好进行修改。使用 MagicRecon，您可以轻松找到:

*   敏感信息泄露。
*   缺少 HTTP 头。
*   打开 S3 桶。
*   子域接管。
*   SSL/TLS 错误。
*   开放端口和服务。
*   电子邮件欺骗。
*   端点。
*   目录。
*   有趣的文件。
*   包含敏感信息的 javascript 文件。
*   CORS 错误配置。
*   跨站点脚本(XSS)。
*   打开重定向。
*   SQL 注入。
*   服务器端请求伪造(SSRF)。
*   CRLF 注射液。
*   远程代码执行(RCE)。
*   其他 bug。

**要求**

要运行该项目，您需要安装以下工具:

*   [子查找器](https://github.com/projectdiscovery/subfinder)
*   [Httpx](https://github.com/projectdiscovery/httpx)
*   [通知](https://github.com/projectdiscovery/notify)
*   [原子核](https://github.com/projectdiscovery/nuclei)
*   [细胞核-模板](https://github.com/projectdiscovery/nuclei-templates)
*   [秒列表](https://github.com/danielmiessler/SecLists)
*   [科尔西](https://github.com/s0md3v/Corsy)
*   [Securityheaders](https://github.com/koenbuyens/securityheaders)
*   [Ssl 检查器](https://github.com/narbehaj/ssl-checker)
*   [秘密发现者](https://github.com/m4ll0k/SecretFinder)
*   [Wfuzz](https://github.com/xmendez/wfuzz)
*   [水叮当](https://github.com/michenriksen/aquatone)
*   [Html 工具](https://github.com/tomnomnom/hacks/tree/master/html-tool)
*   [Waybackurls](https://github.com/tomnomnom/waybackurls)
*   [Kxss](https://github.com/Emoe/kxss)
*   [重新](https://github.com/tomnomnom/anew)
*   [QS 替换](https://github.com/tomnomnom/qsreplace)
*   [Urlprobe](https://github.com/1ndianl33t/urlprobe)
*   [重新](https://github.com/tomnomnom/anew)
*   [Gf](https://github.com/tomnomnom/gf)
*   [捉鬼敢死队](https://github.com/OJ/gobuster)
*   [Findomain](https://github.com/Findomain/Findomain)
*   [欺骗检查](https://github.com/BishopFox/spoofcheck)
*   [左钩拳](https://github.com/GerbenJavado/LinkFinder)
*   [Nmap](https://nmap.org/)

**用途**

**。/magicRecon.sh
输出:
| \/|*_**_*(*)*|*\*_*_ | | \/|/*`|/ _`| |/|*)/*\/_ ' _ \
| | |(*| |(*| | | |(</(*) *|_* 、|*| _ _*|*| _ _ _ _ _ _*| _ _ _ _ _ _/|*| |*|
|*_*/
菜单
1)安装依赖关系
2)通过不一致、电报或松弛通知的大规模漏洞分析
3)子域枚举
4)子域枚举和带核的漏洞扫描
5)具有常见漏洞的子域枚举 (原 MagicRecon)
问)退出
选择一个选项:***

![](img/bab00f6415ca5de2a75dea8fa8bd9214.png)[**Download**](https://github.com/robotshell/magicRecon)