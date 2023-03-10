# Sifter:一个信息、侦察和漏洞扫描器

> 原文：<https://kalilinuxtutorials.com/sifter/>

[![Sifter : A Osint, Recon & Vulnerability Scanner](img/73bc663ead24ec357110516384d43c8a.png "Sifter : A Osint, Recon & Vulnerability Scanner")](https://1.bp.blogspot.com/-PFeVHTyMxAI/Xm5BlYaQ9TI/AAAAAAAAFcI/0osc0LfRhTYF4NivYEKrVafn5CZYeh-MwCLcBGAsYHQ/s1600/Sifer.png)

Sifter 是一个 osint，recon &漏洞扫描器。它在不同的模块集中结合了大量的工具，以便快速执行侦察任务，检查网络防火墙，枚举远程和本地主机，并扫描 microsft 中的“蓝色”漏洞，如果没有修补，则利用它们。

它使用 blackwidow 和 konan 等工具进行 webdir 枚举，并使用 ASM 快速绘制攻击面。

收集的信息保存到结果文件夹，这些输出文件可以很容易地解析到 TigerShark，以便在您的活动中使用。

或者汇编成最终报告以结束渗透测试。

#请，如果你叉此回购确保保持更新。
**频繁更新
**正在寻找一个开发者来帮助整合更多的攻击性模块以供开发，以及侦查。

**安装**

***这将下载并安装所有需要的工具
*
$ git 克隆 https://github.com/s1l3nt78/sifter.git
$ CD 筛选
$ chmod +x install.sh
$。/install.sh**

**也可阅读-[质子:Windows 后期开发框架类似](https://kalilinuxtutorials.com/proton/)**

**模块**

*   **信息模块**
    *   企业信息收集者
        *   哈佛大学——https://github.com/laramies/theHarvester
        *   奥斯梅德斯-https://github.com/j3ssie/Osmedeus
        *   recon spider–https://github.com/bhavsec/reconspider
    *   有针对性的信息收集者
        *   探索者——https://github.com/thewhiteh4t/seeker
        *   https://github.com/sherlock-project/sherlock 夏洛克
*   **域侦察收集**
    *   综合-https://github.com/InQuest/omnibus
    *   DNT 网站-https://github . com/cef/DNT 网站
    *   DomainFuzz–https://github.com/monkeym4ster/DomainFuzz
    *   军械库-https://github.com/depthsecurity/armory
*   **开发工具**
    *   MS 剥削者
        *   active region–https://github.com/m8r0wn/ActiveReign
        *   iSpy–https://github.com/Cyb0r9/ispy
    *   网站开发者
        *   暗星-https://github.com/s1l3nt78/Dark-Star
        *   nekobot—https://github . com/tegal 1337/nekobotv 1
    *   利用搜索
        *   https://github.com/1N3/Findsploit 芬斯普洛伊特
        *   https://github.com/shodansploit/shodansploit ShodanSploit
        *   虎鲨(网络钓鱼)——https://github.com/s1l3nt78/TigerShark
        *   FuzzyDander(通过问题请求获得。此后你可以得到这个模块。阻止脚本小子造成更大的伤害是不可能的。谢谢你的理解。)
        *   brueforercer-https://github . com/githacktools/bruedum
*   **网络扫描仪**
    *   nmap–https://nmap.org
    *   攻击面映射器—https://github.com/superhedgy/AttackSurfaceMapper
    *   asnip–https://github . com/hareo/asnip
*   **蜜罐检测系统**
    *   甜心俏佳人——https://github.com/aswinmguptha/HoneyCaught
    *   嗅熊——https://github.com/MrSuicideParrot/SniffingBear
*   **漏洞扫描器**
    *   https://github.com/cloudflare/flan 果馅饼
    *   快速扫描–https://github.com/skavngr/rapidscan
    *   yuki-Chan–https://github.com/Yukinoshita47/Yuki-Chan-The-Auto-Pentest
*   **网络应用扫描器**
    *   西塔德尔-https://github.com/shenril/Sitadel
    *   wafw 00 f–https://github.com/EnableSecurity/wafw00f
    *   阿芬得-https://github.com/Technowlogy-Pushpender/aapfinder
    *   https://github.com/mazen160/bfac BFAC
*   **网站扫描器&普查员**
    *   尼克托-https://github.com/sullo/nikto
    *   黑寡妇-https://github.com/1N3/blackwidow
    *   wps can–https://github.com/wpscanteam/wpscan
    *   科南-https://github.com/m4ll0k/Konan

**帮助菜单**

**$ sifter 运行程序，在 cli 环境中调出菜单
$ sifter -c 将检查主机列表中的现有主机
$ sifter-a‘target-IP’将主机名/IP 附加到主机文件中
$ sifter -m 打开主模块菜单
$ sifter -e 打开开发模块
$ sifter -i 打开基于信息的模块菜单
$ sifter -d 打开专注于域的模块
$ sifter -n 打开网络映射模块 菜单
$ sifter -w 打开网站聚焦模块
$ sifter -wa 打开 Web-App 聚焦模块菜单
$ sifter -v 打开漏洞扫描模块菜单
$ sifter -u 检查/安装更新
$ sifter -h 此帮助菜单**

[**Download**](https://github.com/s1l3nt78/sifter)