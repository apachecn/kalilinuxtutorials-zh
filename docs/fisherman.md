# FisherMan 程序，通过 Selenium 从脸书用户配置文件中收集信息

> 原文：<https://kalilinuxtutorials.com/fisherman/>

[![Enumy : Linux Post Exploitation Privilege Escalation Enumeration](img/39b3659b564580dfa7a0b7b2c6da1392.png "Enumy : Linux Post Exploitation Privilege Escalation Enumeration")](https://1.bp.blogspot.com/-GYGGAL1ljCU/YSXDC_PdNQI/AAAAAAAAKjY/2xupSNIxKwEm5nm89HSBxs704sMUC9gOACLcBGAsYHQ/s687/template%2B%25281%2529.png)

渔夫是一个 CLI 程序，它通过 Selenium 从脸书用户档案中收集信息

**安装**

**#克隆 repo
$ git 克隆 https://github.com/Godofcoffe/FisherMan
#将工作目录改为渔夫
$ cd 渔夫
#安装 requerements
$ python 3-m pip install-r requerements . txt
# dependency:
您需要在您的机器上安装 geckodriver，
从 mozilla 官方 repo 下载二进制文件:
https://github.com/mozilla/geckodriver/releases/latest
提取并复制二进制文件，我建议将其放在/usr/bin**

**用途**

**$ python 3 FisherMan . py–help
用法:FisherMan . py[-h][–version][-u USERNAME[USERNAME…]|-I ID
[ID…]|–use-TXT TXT _ FILE |-S USER][-SF][-T3][–specify { 0，1，2，3，4，5} [{0，1，2，3，4，5 }][-S][-b][–EMAIL EMAIL][–PASSWORD 密码][-密码(版本 3.4.2)
可选参数:
-h，–help 显示此帮助信息并退出
–Version 显示程序的当前版本。
-u 用户名[用户名…]，–用户名用户名[用户名…]
为搜索定义一个或多个用户。
-ID ID[ID…]，–ID ID[ID…]
设置配置文件识别号。
–use-TXT TXT _ FILE 将用户名参数替换为
txt 中的用户列表。
-S 用户，–搜索用户
它对用户名进行浅层搜索。用“.”替换
空格(句号)。
-sf，–scrape-family 如果该参数被传递，来自
家庭成员的信息将被抓取(如果有的话)。
–指定{0，1，2，3，4，5} [{0，1，2，3，4，5} …]
使用索引号返回
页面的特定部分。about: 0，about_contact_and_basic_info: 1，
about _ family _ and _ relationships:2，about_details: 3，
about_work_and_education: 4，about_places: 5。
-s，–几个返回额外的数据，如个人资料图片，
关注者和朋友的数量。
-b，–浏览器打开浏览器/bot。
–电子邮件电子邮件如果个人资料被阻止，您可以定义您的
帐户，但是您的
好友列表中有您的搜索用户。
–密码密码为您的 facebook 帐户设置密码，此
参数必须与–电子邮件一起使用。
-o，–file-output 将输出数据保存到一个. txt 文件。
-c，–紧凑压缩所有。txt 文件。与-o.
-v，-d，–verbose，–debug
一起使用，详细显示数据搜索过程。
-q，–quiet 消除并简化了一些脚本输出，以实现
更简单、更离散的可视化。**

要搜索用户，请执行以下操作:

*   用户名:`**python3 fisherman.py -u name name.profile name.profile2**`
*   ID: `**python3 fisherman.py -i 000000000000**`

用户名必须在 facebook 个人资料链接上找到，例如:

**https://facebook.com/name.profile/**

也可以从一个. txt 文件中加载多个用户名，这对于暴力输出类型很有用:

**python 3 fisher . py–use-txt filename . txt**

有些个人资料仅限于显示任何帐户的信息，因此您可以使用您的帐户提取。注意:这应该作为最后一个假设，目标档案必须在您的好友列表中:

**python 3 fisher . py–电子邮件 youremail@email.com–密码通行证**

**一些情况**

*   对于完全大面积刮擦:

**python 3 fisherman . py–use-txt file-o-c-SF**

使用每行有几十个名字的文件，您可以进行完整的“扫描”,获取您的信息，甚至您的家庭成员，并在输出时压缩为. zip 文件。

*   对于账户的特定部分:

*   基础数据:`**python3 fisherman.py -u name --specify 0**`
*   家庭和关系:`**python3 -u name --specify 2**`
*   还是有可能混:`**python3 fisherman.py -u name --specify 0 2**`

*   要获得更多信息，如个人资料图片、关注人数和朋友人数:

**python 3 fisher . py-u name[-s |–几个]**

*   按人名进行简短搜索:

**python 3 fisher . py[-S |–search]foo**

用“.”替换名称中的空格(句号)。该脚本返回大约 30 个配置文件。

*   对于极简主义的执行:

**python 3 fisherman . py[-q |–quiet]**

大大减少了脚本的输出文本，按照惯例，提高了性能。

[**Download**](https://github.com/Godofcoffe/FisherMan)