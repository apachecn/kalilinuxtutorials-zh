# Rabid:解码各种 BigIP Cookies 的工具

> 原文：<https://kalilinuxtutorials.com/rabid/>

[![Rabid : Tool To Decode All Kind Of BigIP Cookies](img/563f8e5cb053350a8dedb465a20b9890.png "Rabid : Tool To Decode All Kind Of BigIP Cookies")](https://1.bp.blogspot.com/-Rj_3qJ7r9PY/XlCZuvqVhkI/AAAAAAAAFD8/Jw83oko3-lUHOtjyDLf2ooEGLLhHgwEWACLcBGAsYHQ/s1600/logo%25281%2529.png)

Rabid 是一个 CLI 工具和库，允许简单地解码所有类型的 BigIP cookies。

**特性**

*   支持所有 4 种 cookie 格式
*   CLI 工具和库
*   可破解的

**快速安装**

**$宝石安装狂飙**

**默认用法:CLI**

**$ rabid ' BIGipServer = 1677787402 . 36895 . 0000 '
池名:
Cookie 类型:IPv4 池成员
原始 Cookie:BIGipServer = 1677787402 . 36895 . 0000
解码 cookie: 10.1.1.100:8080**

**默认用途:库**

需要' bigicookie '
**# IP v4 池成员，池名**
bip = bigicookie::decode . new(' BIGipServer = 1677787402 . 36895 . 0000 ')
**#自动解码**
bip . auto _ decode
**#打印结果**
puts " Cookie:# { bip . decoded _ Cookie } "

**也读-[neko bot:500+Exploit 2000+Shell](https://kalilinuxtutorials.com/nekobot/)**

**安装**

**生产**

**从 rubygems.org 安装**

**$宝石安装狂飙**

宝石:疯狂

**从 BlackArch 安装**

**来自储存库:**

**#吃豆人狂犬病**

**来自 git:**

#布莱克曼-我疯了

PKGBUILD: rabid

**从 ArchLinux 安装**

**手动:**

$ git 克隆 https://aur.archlinux.org/rabid.git
$ CD 狂犬
$ makepkg -sic

与 AUR 助手(吃豆人包装)，如皮考尔:

**$ pikaur -S 狂犬病**

AUR:疯狂

**开发**

最好使用 rbenv 来获得最新版本的 ruby，以避免破坏您的系统 ruby。

**从 rubygems.org 安装**

**$ gem 安装-开发狂飙**

**从 git 构建**

只需将 x.x.x 替换为 gem 构建后看到的 gem 版本即可。

**$ git 克隆 https://github.com/Orange-Cyberdefense/rabid.git rabid
$ CD rabid
$ gem 安装 bundler
$ bundler 安装
$ gem 构建 bigicookie . gem spec
$ gem 安装 rabid-x.x.x.gem**

**注意:**如果需要自动安装，可以用$ gem build bigicookie . gem spec | grep Version | cut-d ' '-F4 获取版本。
在 irb 中运行库而不安装 gem

**从本地文件:**

**$ irb -Ilib -rbigipcookie**

**从已安装的 gem:**

**$ rabid _ 控制台**

**CLI 工具也是如此:**

**$ ruby-Ilib-rbigipcookie bin/rabid**

[**Download**](https://github.com/Orange-Cyberdefense/rabid)

**鸣谢:**亚历山大·倪瓒([@诺拉吉](https://github.com/noraj))