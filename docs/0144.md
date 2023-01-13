# 专制——hashcat 包装器帮助自动化破解过程

> 原文：<https://kalilinuxtutorials.com/autocrack-hashcat-wrapper-cracking/>

Autocrack is python script 是一个 [Hashcat](https://hashcat.net) 包装器，帮助自动化破解过程。该脚本包括多种功能来选择一组单词列表和规则，以及在单词列表/规则攻击之前使用自定义掩码运行暴力攻击的能力。

Autocrack 使用 Python 3，它通常已经安装在各种 Linux 发行版中。要在 OS X 安装 Python 3，请遵循这里的说明。

**又读[XSS-有效载荷-列表:跨站脚本(XSS)漏洞有效载荷列表](https://kalilinuxtutorials.com/xss-payload-list/)**

确保在脚本的开头设置路径变量。

```
usage: autocrack.py [-h] [-b NUM] [-bm BRUTEMASK]
                    [-cr CUSTOMRULES] [-cw CUSTOMWL] [-f] [-i INPUTFILE]
                    [-l LOGFILE] [-lh [LISTHASHMODE]] [-lw {all,small,custom}]
                    [-m HASHMODE] [-p] [-pu] [-r {all,simple,singles,combos}]
                    [-s] [-t WLFILTER] [-u] [-w {all,small,custom}]
                    [-ws WORDLISTSIZE]**

**optional arguments:
  -h, --help            show this help message and exit
  -b NUM, --brute NUM   Start cracking with brute force. Specify max length (1-55)
  -bm BRUTEMASK, --brutemask BRUTEMASK
                        Character types to brute force (?a, ?u, ?l, ?s, ?d);
                        If only one type is specified, all positions will be
                        brute forced with that character type
  -cr CUSTOMRULES, --customrules CUSTOMRULES
                        Comma separated list of rules to run; rules are run in
                        the order of left to right
  -cw CUSTOMWL, --customwl CUSTOMWL
                        Comma separated list of the full path to one or more wordlists
  -f, --force           Pass the force parameter to Hashcat
  -i INPUTFILE, --inputfile INPUTFILE
                        Path to file with hashes**
  **-l LOGFILE, --logfile LOGFILE
                        Path to log the cracking session
  -lh [LISTHASHMODE], --listhashmode [LISTHASHMODE]
                        List hash types and their associated mode; provide a
                        keyword to filter results
  -lw {all,small,custom}, --listwordlists {all,small,custom}
                        List wordlists in BASESUPPORTFILESPATH/wordlists; -t
                        (filter) and -ws (wordlist size) can be used to affect
                        results
  -m HASHMODE, --hashmode HASHMODE
                        Hashcat cracking algorithm**
  **-p, --pwds            Output the list of cracked passwords (for pipal
                        analysis)
  -pu, --pwdsunique     Output a uniqued list of cracked passwords
  -r {all,simple,singles,combos}, --rules {all,simple,singles,combos}
                        Specify which hashcat set of rules to use
  -s, --show            Display cracked credentials
  -t WLFILTER, --wlfilter WLFILTER
                        Filters the wordlists to only include file names that
                        contain the keyword
  -u, --username        Pass the username parameter to Hashcat
  -v {0,1,2}, --verbose {0,1,2}
                        Specify a verbosity level: 0: Informational, 1:
                        Verbose, 2: Include Hashcat Output
  -w {all,small,custom}, --wordlists {all,small,custom}
                        Specify which set of wordlists to use; "custom" uses
                        the -ws option to specify the maximum file size
  -ws WORDLISTSIZE, --wordlistsize WORDLISTSIZE
                        Filter wordlists to files of a maximum number of
                        lines; Default = 500,000; 0 = all wordlists
```

## **汽车起重机待办事项**

1.  将函数添加到一步 AD 域哈希转储(lm -> nt)
2.  添加对自定义掩码字符集的支持
3.  包括面具攻击
4.  跟踪哪些单词列表/规则/掩码破解了密码
5.  实现马尔可夫链

[![https://github.com/Nekmo/dirhunt](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/timbo05sec/autocrack)