# Owasp D4n155:使用 Osint 的智能动态单词表

> 原文：<https://kalilinuxtutorials.com/owasp-d4n155/>

[![Owasp D4n155 : Intelligent & Dynamic Wordlist Using Osint](img/180a85427b9d5708ca911e5f72e3e5fa.png "Owasp D4n155 : Intelligent & Dynamic Wordlist Using Osint")](https://1.bp.blogspot.com/-ijaX8sO0Ms8/XlWLGZys6GI/AAAAAAAAFGQ/AJSocaDphVY5EmQs50iOpHKOBfp5__cZwCLcBGAsYHQ/s1600/Osint.png)

OWASP D4N155 是一个使用 OSINT 的智能动态单词表。这是一个信息安全审计工具，根据目标页面的内容创建智能单词表。

[![](img/2e9a6b703b96cfab6eb8fa5ff767e52a.png)](https://asciinema.org/a/294029)

**安装**

**需要:** [Python3.6](https://realpython.com/installing-python/) ，[Bash(GNU Bourne-Again SHell)](https://www.gnu.org/software/bash/#download)
**可选** : [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) ， [Groff](https://www.gnu.org/software/groff/)

**来源**

**git 克隆 https://github.com/owasp/D4N155.git
CD d4n 155
pip 3 install-r requirements . txt
bash main**

**或无 git**

**wget-qO-https://github.com/owasp/D4N155/archive/master.zip | BSD tar-xf-
CD d4n 155-master
pip 3 install-r requirements . txt
bash main**

**也读作-[CVE-API:CVE.MITRE.ORG](https://kalilinuxtutorials.com/cve-api/)非官方 API **

**码头工人**

**在图像中:**

**来自 docker.pkg.github.com/owasp/d4n155/d4n155:latest**

Cli :

**docker 拉 docker.pkg.github.com/owasp/d4n155/d4n155:latest
docker run-it d4n 155**

**手动**

**D4N155:智能审计安全工具

用法:bash main
所有选项都是可选的

选项:**
-w，–word list 根据网站上的信息
制作智能单词列表。
-t，–目标根据您在 URL 中传递的
源信息创建智能单词列表。
-b，–基于分析文本生成
自定义词表
-r，–速率定义请求之间的时间间隔
-o，–输出用于存储所有词表。
-？a，–用无头的
-h 进行侵略性的侵略性阅读，–有助于展示这一讯息。

**值:**
URL URL 目标，示例:scanme.nmap.org
IP IP 地址
时间时间，示例:2.5。即:00:00:02:30..0 是默认的
文件文件，用于保存结果，获取 URL 或在
单词表中使用

[**Download**](https://github.com/OWASP/D4N155)