# Whatfiles:记录任何 Linux 进程访问了哪些文件

> 原文：<https://kalilinuxtutorials.com/whatfiles/>

[![](img/b1e694231ee9af23fd6dab886678971c.png)](https://blogger.googleusercontent.com/img/a/AVvXsEiYBGDmquVlqGTepMZqovtY7Vmc3T6FMfBgT_k5Jjpn1btmafRRFYy8SElLVw2q82Y2YS0yaR132yA9kn2da2S-V2nkVs9faO_Jw5H3m09fgYLEM8s1N4tvzF6ZM7iYhTkiA0PKO3E7aCq5Mk30iBax5g3uCNNC5GBKce1YgMqa6Yraui_0etDYGpHY=s728)

是一个 Linux 工具，记录另一个程序在你的系统上读/写/创建/删除了什么文件。它还跟踪目标进程创建的任何新进程和线程。

**理**

长期以来，我一直对缺乏一个简单的实用程序来查看进程从`**main()**`到退出接触了哪些文件感到沮丧。无论您是不信任软件供应商还是担心恶意软件，了解一个程序或安装程序对您的系统有什么影响都是非常重要的。`**lsof**`只观察一个瞬间，而`**strace**`很大，有点复杂。

**样本输出**

**模式:读取，文件:/home/theron/。gimp-2.8/tool-options/gimp-clone-tool，syscall: openat()，PID: 8566，process: gimp
模式:read，file: /home/theron/。gimp-2.8/tool-options/gimp-heal-tool，syscall: openat()，PID: 8566，process: gimp
模式:read，file: /home/theron/。gimp-2.8/tool-options/gimp-perspective-clone-tool，syscall: openat()，PID: 8566，process: gimp
模式:read，file: /home/theron/。gimp-2.8/tool-options/gimp-convolve-tool，syscall: openat()，PID: 8566，process: gimp
模式:read，file: /home/theron/。gimp-2.8/tool-options/gimp-smudge-tool，syscall: openat()，PID: 8566，process: gimp
模式:read，file: /home/theron/。gimp-2.8/tool-options/gimp-dodge-burn-tool，syscall: openat()，PID: 8566，process: gimp
模式:read，file: /home/theron/。gimp-2.8/tool-options/gimp-desature-tool，syscall: openat()，PID: 8566，process: gimp
mode: read，file: /home/theron/。gimp-2.8/插件，syscall: openat()，PID: 8566，进程:gimp
模式:read，file:/usr/lib/gimp/2.0/插件，syscall: openat()，PID: 8566，进程:gimp
模式:read，file: /home/theron/。gimp-2.8/pluginrc，syscall: openat()，PID: 8566，process: gimp
mode: read，file:/usr/share/locale/en _ US/LC _ MESSAGES/gimp 20-STD-plug-ins . mo，syscall: openat()，PID: 8566，process: gimp
mode: read，file:/usr/lib/gimp/2.0/plug-ins/script-fu，syscall: openat()，PID: 8566 PID: 8574，进程:/usr/lib/gimp/2.0/plug-ins/script-fu
模式:read，文件:/usr/lib/libgimp-2.0.so.0，syscall: openat()，PID: 8574，进程:/usr/lib/gimp/2.0/plug-ins/script-fu
模式:read，文件:/usr/lib/lib gimp-2.0 . so . 0，syscall:open**

**使用**

*   基本使用，启动`**ls**`并将输出写入当前目录下的日志文件:`**$ whatfiles ls -lah ~/Documents**`
*   用 **`-o` : `$ whatfiles -o MyLogFile cd ..`** 指定输出文件位置
*   包括调试输出，打印到标准输出而不是日志文件:`**$ whatfiles -d -s apt install zoom**`
*   附加到当前运行的进程(需要 root 权限):`**$ sudo whatfiles -p 1234**`

**编译(需要`gcc`和`make` )**

**$ CD what files
$ make
$ sudo make install**

[**Download**](https://github.com/spieglt/whatfiles)