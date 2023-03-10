# Rootend:一个*Nix 枚举器和自动权限提升工具

> 原文：<https://kalilinuxtutorials.com/rootend/>

[![](img/a3dd94fad768b82cc3d3334a9bcd7467.png)](https://1.bp.blogspot.com/-aYA24AutMa0/YULUKgm2WNI/AAAAAAAAK2w/abixr_2tEMg0jKKoNWKhr-incR2uHUr8wCLcBGAsYHQ/s728/24493199%2B%25281%2529.png)

**Rootend** 是一个 python *nix 枚举器&自动权限提升工具。

*有关我们工具的完整列表，请访问我们的网站 https://www.twelvesec.com/*

作者:

*   nickvourd(推特)
*   马尔代夫(推特)
*   伺服系统

**用法**

**T1。_ *_**/_ _ | |*/_/*/_/
| | \ \/\///_*\ _ _ _ _ _ _/*_ _/*\ | | \/*/| |*\/\*//\*/\ _ _ _ _ _ _
|*| \/_/_ _>。rootend 是 GPLv3 许可的开源工具。
受影响的系统:*nix。
作者:@twelvesec 的@nickvourd。
特别感谢@maldevel &伺服。https://www.twelvesec.com/
更多信息请访问 https://github.com/twelvesec/rootend..
可选参数:
-h，–help 显示此帮助消息并退出
-v，–version 显示版本并退出
-a，–auto 自动权限提升过程
-m，–手动系统枚举
-n，–no color 禁用颜色
-b，–banner 显示 banner 并退出
-s，–suid suid 二进制枚举
-w，–弱弱权限文件枚举
-p，–PHP PHP 配置/rootend.py -a
。/rootend.py -m
。/rootend.py -v
。/rootend.py -b
具体类别用法举例:
。/rootend.py -a -s
。/rootend.py -m -w
。/rootend.py -a -s -p
。/rootend.py -m -w -c -p
。/root end . py-a-s-c-p-f
*使用上述参数和-n 来禁用颜色。***

**版本**

**2.0.2**

**支持**

*   Python 2.x
*   Python 3.x

**在**上测试

*   Python 2.7.18rc1
*   Python 3.8.2

**模式**

*   指南
*   汽车

**剥削类别**

**Suid Binaries**

*   一般 Suids
*   读取文件的 Suids
*   以根用户身份创建文件的 Suids
*   有限 Suids
*   定制西装

**弱权限**

*   /etc/密码
*   /etc/影子
*   apache2.conf
*   httpd.conf
*   重定向. conf
*   /root

**所有权弱**

*   /etc/密码
*   /etc/影子
*   apache2.conf
*   httpd.conf
*   重定向. conf
*   /root

**战力**

*   一般功能
*   自定义功能
*   With CAP_SETUID

**有趣的文件**

*   PHP 配置文件
*   全局可写文件

[Download](https://github.com/twelvesec/rootend)