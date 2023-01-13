# Wordlistctl:获取、安装和搜索来自网站和种子的 Wordlist 档案

> 原文：<https://kalilinuxtutorials.com/wordlistctl-websites-torrent-peers/>

Wordlistctl 是一个脚本，用于从提供超过 2900 个单词列表的网站获取、安装、更新和搜索单词列表档案。

在 Blackarch Linux 的最新版本中，它被添加到了 **/usr/share/wordlists/** 目录中。

**又读:[滚筒筛:筛选嵌入式设备文件，识别潜在的易受攻击指标](https://kalilinuxtutorials.com/trommel-embedded-vulnerable-indicators/)**

**安装**

**pacman -S wordlistctl**

**用途**

[sepehrdad @ black arch-dev ~/black arch/repos/wordlistctl]$ wordlistctl-H
–= = =[blackarch.org 的 wordlistctl]=–
用法:
wordlistctl-f[选项]|-S[选项] | -S |
选项:
-f–下载选择的单词列表-？要列出 id 为
的单词列表-d–单词列表基本目录(默认:/usr/share/word lists)
-c–更改单词列表类别-？列出单词列表类别
-S–在基目录中使用搜索的单词列表
-S–在站点中使用搜索的单词列表
-h–首选 http
-X–解压缩单词列表
-F–列出给定类别中的单词列表
-r–解压缩后删除压缩文件
-T–最大并行下载量(默认值:5)
misc:
-C–禁用终端颜色
-T–禁用 torrent 下载
-P
-A–设置用户代理字符串
-Y–代理 http
-Z–代理 torrent
-M–使用多处理进行并行化
-N–不要求任何确认
-I–不检查完整性
-V–打印 wordlistctl 版本并退出
-H–打印此帮助并退出
示例:
#下载并解压缩所有单词列表并删除存档
$ wordlistctl -f 下载用户名类别中的所有单词表
$ wordlistctl -f 0 -c 0
#列出 id 为
$ wordlistctl -f 的密码类别中的所有单词表？ -c 1
#下载并解压 misc 类别中的所有单词表
$ wordlistctl -f 0 -c 4 -X
#使用 20 个线程下载 filename 类别中的所有单词表
$ wordlistctl-c 3-F 0-t 20
#使用 http
$ wordlistctl-F 2-d ~/wordlists-h
#打印用户名和密码类别中的单词表【t4t 使用 tor socks5 代理
$ wordlistctl-f 0-P " socks 5://127 . 0 . 0 . 1:9050 "-Y
#使用 http 代理和 noleak 用户代理
$ wordlistctl-f 0-P " http://127 . 0 . 0 . 1:9060 "-Y-A " no leak "

[**Download**](https://github.com/BlackArch/wordlistctl)