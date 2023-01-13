# lol bas——以土地二进制和脚本为生

> 原文：<https://kalilinuxtutorials.com/lolbas/>

LOLBAS 是生活在陆地上的二进制和脚本。
所有不同的文件都可以在这里一个花哨的前端后面找到:[https://lol bas-project . github . io .](https://lolbas-project.github.io)

这个 repo 是我们维护 YML 文件的地方，这些文件由高级前端使用。

LOLBAS 项目的目标是记录每一个二进制文件、脚本和库，这些都可以用于陆上技术。

另请阅读: **[IP 混淆器——社交工程师和绕过防火墙的简单工具](https://kalilinuxtutorials.com/ip-obfuscator-bypass-firewall/)**

**标准**

LOLBin/Lib/Script 必须:

*   是 Microsoft 签名的文件，可以是操作系统自带的，也可以是从 Microsoft 下载的。
*   拥有额外的“意想不到的”功能。记录预期的用例并不有趣。
    *   例外情况是绕过应用程序白名单
*   拥有对 APT 或 red 团队有用的功能

有趣的功能包括:

*   执行代码
    *   任意代码执行
    *   其他程序(未签名)或脚本的传递执行(通过 LOLBin)
*   编译代码
*   文件操作
    *   下载
    *   上传
    *   复制
*   坚持
    *   利用现有 LOLBin 的直通持久性
    *   持久性(例如，在广告中隐藏数据，登录时执行)
*   UAC 旁路
*   凭证盗窃
*   转储进程内存
*   监控(例如键盘记录器、网络跟踪)
*   日志规避/修改
*   DLL 侧加载/劫持，而不重新定位在文件系统的其他地方。

**罗宾的历史**

“靠土地生活”这个短语是由克里斯托弗·坎贝尔(@obscuresec)和马特·格雷贝尔(@ mattifestation)在 DerbyCon 3 上创造的。

[https://www.youtube.com/embed/j-r6UonEkUw?feature=oembed&enablejsapi=1](https://www.youtube.com/embed/j-r6UonEkUw?feature=oembed&enablejsapi=1)

LOLBins 一词来自 Twitter 上的一个讨论，讨论如何称呼可被攻击者用来执行超出其原始目的的操作的二进制文件。Philip Goh (@MathCasualty) [提出 LOLBins](https://twitter.com/MathCasualty/status/969174982579273728) 。

一个高度科学的互联网投票随之而来，在达成普遍共识(69%)后，这个名字被正式命名为[。吉米(@bohops)](https://twitter.com/Oddvarmoe/status/985432848961343488) [跟进 LOLScripts](https://twitter.com/bohops/status/984828803120881665) 。没有进行民意测验。

这些文件的常见标签有:

*   #罗宾
*   #LOLBins
*   #LOLScript
*   # LOLScripts
*   #LOLLib
*   #棒棒糖

[**Download**](https://github.com/LOLBAS-Project/LOLBAS)

**信用:良心黑客**