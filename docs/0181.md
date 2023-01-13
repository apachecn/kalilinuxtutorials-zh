# xat tacker–网站漏洞扫描器和自动开发工具

> 原文：<https://kalilinuxtutorials.com/xattacker-website-vulnerability-scanner/>

XAttacker 是一个 perl 网站工具，用于漏洞扫描器&自动剥削者，你可以用它来发现你的网站中的漏洞，或者你可以用这个工具来获取外壳、发送、篡改、cPanels &数据库。

目前 tol 得到了 WordPress、Joomla、Drupal、PrestaShop 和 LokoMedia 等 CMS 的支持。

**也读作 [Blind-Bash:项目混淆你的 Bash 代码](https://kalilinuxtutorials.com/blind-bash-obfuscate-bash-code/)**

## **XAttacker 安装**

### **Linux 安装**

```
git clone https://github.com/Moham3dRiahi/XAttacker.git
cd XAttacker
perl XAttacker.pl
```

### **Windows 安装**

```
Download Perl
Download XAttacker
Extract XAttacker into Desktop
Open CMD and type the following commands:
cd Desktop/XAttacker-master/
perl XAttacker.pl
```

### **安卓安装**

```
git clone https://github.com/Moham3dRiahi/XAttacker.git
cd XAttacker
chmod +x termux-install.sh
bash termux-install.sh
```

## **视频**

[https://www.youtube.com/watch?v=EgqTsrWt2VU](https://www.youtube.com/watch?v=EgqTsrWt2VU)

## **扫描和利用实例** 

*   如果您的目标网站列表保存在文本文件(list.txt)中，那么您可以使用以下命令行运行该工具

**`perl XAttacker.pl -l list.txt`**

*   如果您没有目标网站列表，请使用下面的命令运行该工具

`**perl XAttacker.pl**`

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/Moham3dRiahi/XAttacker)