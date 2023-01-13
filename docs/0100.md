# CTF——安全研究工具的一些设置脚本

> 原文：<https://kalilinuxtutorials.com/ctf-scripts-security-tools/>

CTF 是一个安装脚本的集合，用于创建各种安全研究工具的安装。当然，这并不是一个困难的问题，但是把它们放在一个地方真的很好，很容易部署到新的机器等等。定期检查这些工具的安装脚本。

**也读[xs spy-Web 应用 XSS 扫描仪](https://kalilinuxtutorials.com/xsspy-web-application/)**

**包括以下工具的安装程序**

| 种类 | 工具 | 描述 |
| --- | --- | --- |
| 二进制的 | [afl](http://lcamtuf.coredump.cx/afl/) | 最先进的模糊器。 |
| 二进制的 | [安格尔](http://angr.io) | Shellphish 的下一代二进制分析引擎。 |
| 二进制的 | [呕吐](https://github.com/programa-stic/barf-project) | 二进制分析和逆向工程框架。 |
| 二进制的 | [bindead](https://bitbucket.org/mihaila/bindead/wiki/Home) | 二进制文件的静态分析工具。 |
| 二进制的 | [检查秒](https://github.com/slimm609/checksec.sh) | 检查二进制强化设置。 |
| 二进制的 | [代码原因](https://github.com/trailofbits/codereason) | 语义二进制代码分析框架。 |
| 二进制的 | [十字工具-ng](http://crosstool-ng.org/) | 跨编译器和跨架构工具。 |
| 二进制的 | [交叉 2](http://kozos.jp/books/asm/asm.html) | 一套交叉编译工具，来自一本关于 c 的日文书籍。 |
| 二进制的 | [精灵踢球者](http://www.muppetlabs.com/%7Ebreadbox/software/elfkickers.html) | 一组用于处理 ELF 文件的实用程序。 |
| 二进制的 | [解说员](http://www.elfparser.com/) | 通过静态分析快速确定 ELF 二进制文件的功能。 |
| 二进制的 | [邪恶化](http://www.mathstat.dal.ca/%7Eselinger/md5collision/) | 创建 MD5 冲突二进制文件的工具 |
| 二进制的 | [gdb](http://www.gnu.org/software/gdb/) | 使用 python2 绑定的最新 gdb。 |
| 二进制的 | [gdb 堆](https://github.com/rogerhu/gdb-heap) | 用于调试堆问题的 gdb 扩展。 |
| 二进制的 | [全球环境基金](https://github.com/hugsy/gef) | 广发银行的增强环境。 |
| 二进制的 | [hongfuzz](https://github.com/google/honggfuzz) | 一个通用的，易于使用的模糊器，具有有趣的分析选项。 |
| 二进制的 | [libheap](https://github.com/cloudburst/libheap) | 用于检查 glibc 堆的 gdb python 库(ptmalloc) |
| 二进制的 | [瘴气](https://github.com/cea-sec/miasm) | Python 中的逆向工程框架。 |
| 二进制的 | [one_gadget](https://github.com/david942j/one_gadget) | libc 的神奇小工具搜索。 |
| 二进制的 | [熊猫](https://github.com/moyix/panda) | 架构中立的动态分析平台。 |
| 二进制的 | [pathgrind](https://github.com/codelion/pathgrind) | 基于路径的符号辅助模糊器。 |
| 二进制的 | [踏板](https://github.com/longld/peda) | 广发银行的增强环境。 |
| 二进制的 | [preeny](https://github.com/zardus/preeny) | 一组有用的预加载(为许多架构编译！). |
| 二进制的 | [pwndbg](https://github.com/zachriggle/pwndbg) | 广发银行的增强环境。尤其是 pwning。 |
| 二进制的 | [p 工具](https://github.com/Gallopsled/pwntools) | 有用的 CTF 实用程序。 |
| 二进制的 | [python-pin](https://github.com/blankwall/Python_Pin) | pin 的 Python 绑定。 |
| 二进制的 | [qemu](http://qemu.org) | qemu 的最新版本！ |
| 二进制的 | [戚拉](http://qira.me) | 并行、永恒的调试器。 |
| 二进制的 | [radare2](http://www.radare.org/) | 克劳威尔喜欢的一些疯狂的东西。 |
| 二进制的 | 召回 | 基于 linux 的汇编 REPL。 |
| 二进制的 | [ropper](https://github.com/sashs/Ropper) | 另一个小工具查找器。 |
| 二进制的 | [rp++](https://github.com/0vercl0k/rp) | 另一个小工具查找器。 |
| 二进制的 | [rr](http://rr-project.org) | 记录和重放调试框架 |
| 二进制的 | [scratchabit](https://github.com/pfalcon/ScratchABit) | 易于重定目标和黑客攻击的交互式反汇编程序 |
| 二进制的 | [scratchable block](https://github.com/pfalcon/ScratchABlock) | 又一个受损的反编译器项目 |
| 二进制的 | [seccomp-tools](https://github.com/david942j/seccomp-tools) | 为 seccomp 分析提供了强大的工具 |
| 二进制的 | [shellnoob](https://github.com/reyammer/shellnoob) | 外壳代码编写助手。 |
| 二进制的 | [shellsploit](https://github.com/b3mb4m/shellsploit-framework) | 外壳代码开发工具包。 |
| 二进制的 | [雪人](https://github.com/yegord/snowman) | 跨架构反编译器。 |
| 二进制的 | [污点研磨](https://github.com/wmkhoo/taintgrind) | 一个 valgrind 污点分析工具。 |
| 二进制的 | [valgrind](http://valgrind.org) | 带有一些内置工具的动态二进制插装框架。 |
| 二进制的 | [villoc](https://github.com/wapiflapi/villoc) | 堆操作的可视化。 |
| 二进制的 | [virtualsocket](https://github.com/antoniobianchi333/virtualsocket) | 一个很好的与二进制文件交互的库。 |
| 二进制的 | [wcc](https://github.com/endrazine/wcc) | 巫术编译器集合是在 GNU/Linux 和其他 POSIX 平台上执行二进制巫术的编译工具的集合。 |
| 二进制的 | [xrop](https://github.com/acama/xrop) | 小工具查找器。 |
| 二进制的 | [蝎尾狮](https://github.com/trailofbits/manticore) | 蝎狮是动态二进制分析的原型工具，支持符号执行、污点分析和二进制插装。 |
| 辩论术 | [binwalk](https://github.com/devttys0/binwalk.git) | 固件(和任意文件)分析工具。 |
| 辩论术 | [脱臼器](http://www.hsc.fr/ressources/outils/dislocker/) | 用于读取 Bitlocker 加密分区的工具。 |
| 辩论术 | [执行程序](https://github.com/kholia/exetractor-clone) | 解包打包的 Python 可执行文件。支持 PyInstaller 和 py2exe。 |
| 辩论术 | [固件-模块-套件](https://code.google.com/p/firmware-mod-kit/) | 固件打包/解包工具。 |
| 辩论术 | [pdf 解析器](http://blog.didierstevens.com/programs/pdf-tools/) | 用于挖掘 PDF 文件的工具 |
| 辩论术 | [peepdf](https://github.com/jesparza/peepdf) | 分析 PDF 文档的强大 Python 工具。 |
| 辩论术 | [scrdec](https://gist.github.com/bcse/1834878) | 编码 Windows 脚本的解码器。 |
| 辩论术 | [testdisk](http://www.cgsecurity.org/wiki/TestDisk) | 用于文件恢复的 Testdisk 和 photorec。 |
| 秘密党员 | [的犯罪行为](https://github.com/SpiderLabs/cribdrag) | 交互式婴儿床拖动工具(用于加密)。 |
| 秘密党员 | [fastcoll](https://www.win.tue.nl/hashclash/) | 一个 md5sum 碰撞发生器。 |
| 秘密党员 | [远见](https://github.com/ALSchwalm/foresight) | 预测随机数生成器输出的工具。要运行，请启动“预见”。 |
| 秘密党员 | [羽毛掸子](https://github.com/nccgroup/featherduster) | 一个自动化、模块化的密码分析工具。 |
| 秘密党员 | [伽罗瓦](http://web.eecs.utk.edu/%7Eplank/plank/papers/CS-07-593) | 快速伽罗瓦域算术库/工具包。 |
| 秘密党员 | [哈希基尔](https://github.com/gat3way/hashkill) | 哈希饼干。 |
| 秘密党员 | [散列泵](https://github.com/bwall/HashPump) | 用于执行哈希长度扩展攻击的工具。 |
| 秘密党员 | [哈希泵-部分哈希](https://github.com/mheistermann/HashPump-partialhash) | Hashpump，支持部分未知的散列。 |
| 秘密党员 | [散列标识符](https://code.google.com/p/hash-identifier/source/checkout) | 简单哈希算法标识符。 |
| 秘密党员 | [libc-数据库](https://github.com/niklasb/libc-database) | 建立一个 libc 偏移量的数据库来简化开发。 |
| 秘密党员 | [小黑盒](https://github.com/devttys0/littleblackbox) | 嵌入式设备的私有 SSL/SSH 密钥数据库。 |
| 秘密党员 | [msieve](http://sourceforge.net/projects/msieve/) | Msieve 是一个 C 库，实现了一套算法来分解大整数。 |
| 秘密党员 | [不礼貌](https://github.com/nonce-disrespect/nonce-disrespect) | 不尊重对手:对 TLS 中 GCM 的实际伪造攻击。 |
| 秘密党员 | [pemcrack](https://github.com/robertdavidgraham/pemcrack) | SSL PEM 文件破解程序。 |
| 秘密党员 | [pkcrack](https://www.unix-ag.uni-kl.de/%7Econrad/krypto/pkcrack.html) | PkZip 加密破解程序。 |
| 秘密党员 | [python-padding racle](https://github.com/mwielgoszewski/python-paddingoracle) | 填充 oracle 攻击自动化。 |
| 秘密党员 | [复仇](http://reveng.sourceforge.net/) | CRC 查找器。 |
| 秘密党员 | [宋承宪 _ 解码器](https://github.com/jjyg/ssh_decoder) | 一个解码 ssh 流量的工具。您将需要来自`https://launchpad.net/~brightbox/+archive/ubuntu/ruby-ng`的`ruby1.8`来运行它。用`ssh_decoder --help`运行以寻求帮助，因为不带参数运行它会导致它崩溃。 |
| 秘密党员 | [sslsplit](https://github.com/droe/sslsplit) | SSL/TLS MITM。 |
| 秘密党员 | [xortool](https://github.com/hellman/xortool) | 异或分析工具。 |
| 秘密党员 | [亚夫](http://sourceforge.net/projects/yafu/) | 自动整数因式分解。 |
| 网 | [胶囊](http://portswigger.net/burp) | 网络代理做淘气的网络东西。 |
| 网 | [混合](https://github.com/stasinopoulos/commix) | 命令注入和开发工具。 |
| 网 | [dirb](http://dirb.sourceforge.net/) | Web 路径扫描仪。 |
| 网 | [目录搜索](https://github.com/maurosoria/dirsearch) | Web 路径扫描仪。 |
| 网 | [mitmproxy](https://mitmproxy.org/) | CLI Web 代理和 python 库。 |
| 网 | [sqlcmap](http://sqlmap.org/)的缩写 | SQL 注入自动化引擎。 |
| 网 | [子类](https://github.com/TheRook/subbrute) | 一个枚举 DNS 记录和子域的 DNS 元查询蜘蛛。 |
| 斯蒂戈 | [声音可视化器](http://www.sonicvisualiser.org/) | 音频文件可视化。 |
| 斯蒂戈 | [剑鱼](http://www.caesum.com/handbook/stego.htm) | 另一个图像隐写解算器。 |
| 斯蒂戈 | [stegdetect](http://www.outguess.org/) | 隐写术检测/破解工具。 |
| 斯蒂戈 | [stegsolve](http://www.caesum.com/handbook/stego.htm) | 图像隐写求解器。 |
| 斯蒂戈 | [zsteg](https://github.com/zed-0xff/zsteg) | 检测 PNG 和 BMP 中的隐写数据。 |
| 机器人 | [apktool](https://ibotpeaches.github.io/Apktool/) | 剖析、拆卸和重新包装 Android APKs |
| 机器人 | [android-sdk](http://developer.android.com/sdk) | android SDK (adb、emulator 等)。 |
| 混杂的 | [xspy](http://git.kali.org/gitweb/?p=packages/xspy.git;a=summary) | 监视 X 会话的小工具。 |
| 混杂的 | [z3](https://github.com/Z3Prover/z3) | 来自微软研究院的定理证明。 |
| 混杂的 | [jdgui](http://jd.benow.ca/) | Java 反编译器。 |
| 混杂的 | [韦莱斯](https://codisec.com/veles/) | 二进制数据分析和可视化工具。 |
| 混杂的 | [youtube-dl](https://yt-dl.org/) | 流行的 youtube 下载器的最新版本。 |

也有一些有用库的安装程序。目前只安装了这些库的 python 绑定。

| 种类 | 图书馆 | 描述 |
| --- | --- | --- |
| 二进制的 | [顶石](http://www.capstone-engine.org) | 多体系结构拆卸框架。 |
| 二进制的 | [梯形](http://www.keystone-engine.org) | 轻量级多架构汇编框架。 |
| 二进制的 | [独角兽](http://www.unicorn-engine.org) | 多架构 CPU 仿真器框架。 |
| 二进制的 | lief | 用于检测可执行格式的库。 |

也有一些非 CTF 的东西安装程序来打破单调！

| 种类 | 工具 | 描述 |
| --- | --- | --- |
| 比赛 | [矮人要塞](http://www.bay12games.com/dwarves/) | CTF 后帮你放松的东西！ |
| tor 浏览器 | [tor 浏览器](https://www.torproject.org/projects/torbrowser.html.en) | 当您需要应对来自不同 IP 的网络挑战时非常有用。 |
| pyvmmonitor | [pyvmmonitor](http://www.pyvmmonitor.com/) | PyVmMonitor 是一个分析器，目标很简单:成为分析 Python 程序的最佳方式。 |

## **【CTF 用法】**

**要使用，请执行:**

```
# set up the path
/path/to/ctf-tools/bin/manage-tools setup
source ~/.bashrc

# list the available tools
manage-tools list

# install gdb, allowing it to try to sudo install dependencies
manage-tools -s install gdb

# install pwntools, but don't let it sudo install dependencies
manage-tools install pwntools

# uninstall gdb
manage-tools uninstall gdb

# uninstall all tools
manage-tools uninstall all

# search for a tool
manage-tools search preload
```

在可能的情况下，工具保持安装非常独立(即，在工具/目录中)，大多数卸载只是调用 **git clean** ( **注意**，这是**而不是**小心；工具目录下的所有内容，包括您正在处理的内容，都会在卸载过程中消失)。一个例外是 python 工具，如果可能的话，使用`pip`包管理器来安装。一个 `**ctftools** virtualenv 是在**管理-工具设置**命令期间创建的，可以使用命令 `**在 ctftools 上工作来访问。**``

 ``## **【Docker(版本 1.7+)**

根据大众的要求，一个 Dockerfile 文件已被包括在内。您可以使用以下内容构建 docker 映像:

```
git clone https://github.com/zardus/ctf-tools
docker build -t ctf-tools .
```

并使用以下命令运行它:

```
docker run -it ctf-tools
```

构建的映像将克隆 ctf-tools 并准备好，但是您仍然需要安装工具本身(见上文)。

或者，您也可以从 dockerhub 下载 ctf-tools(预装了一些工具):

```
docker run -it zardus/ctf-tools
```

## **流浪汉**

您可以通过以下方式构建一个无固定资产的虚拟机:

```
wget https://raw.githubusercontent.com/zardus/ctf-tools/master/Vagrantfile
vagrant up
```

并通过以下方式连接到它:

```
vagrant ssh
```

## **安装脚本**

安装脚本将以 **$PWD** 作为**工具名**运行。它应该以尽可能包含的方式将工具安装到这个目录中。理想情况下，用 **git clean** 完全卸载应该是可能的。

安装脚本应该创建一个`bin`目录，并将其可执行文件放在那里。这些可执行文件将自动链接到回购的主`bin`目录中。它们可以从任何目录启动，所以不要对`$0`的位置做任何假设！

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/zardus/ctf-tools/)``