# 因果报应:用你的密码找到泄露的邮件

> 原文：<https://kalilinuxtutorials.com/karma-leaked-emails-passwords/>

Karma 是一个工具，用于查找带有密码的泄露邮件。未经事先同意使用此程序攻击目标是非法。

最终用户有责任遵守所有适用的地方、州和联邦法律。开发人员不承担任何责任，也不对本程序造成的任何误用或损坏负责。

**也读作-[Decker:声明式渗透测试编排框架](https://kalilinuxtutorials.com/decker-penetration-testing-framework/)**

**安装**

sudo apt 安装 tor python3 python3-pip
sudo 服务 tor start
git 克隆 https://github.com/decoxviii/karma.git；CD karma
sudo-H pip 3 install-r requirements . txt
python 3 bin/karma . py–help

试验

所有的测试都是在 Debian/Ubuntu 上完成的。

*   用密码搜索邮件:12345678

python3 bin/karma.py 搜索' 123456789 '–密码 o 测试 1

*   用本地部分搜索电子邮件:johndoe

python3 bin/karma.py 搜索‘John doe’–local-part-o test 2

*   用域名搜索电子邮件:hotmail.com

python3 bin/karma.py 搜索' hotmail . com '–domain-o test3

*   搜索电子邮件密码:johndoe@unknown.com

python 3 bin/karma . py target ' John doe @ unknown . com '-o test 4

[**Download**](https://github.com/decoxviii/karma)