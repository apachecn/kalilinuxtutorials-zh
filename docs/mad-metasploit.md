# Mad Metasploit : Metasploit 定制模块、插件和资源脚本

> 原文：<https://kalilinuxtutorials.com/mad-metasploit/>

Mad Metasploit 是一个很棒 Metasploit 集合，它包含了定制模块、插件和资源脚本。

**将 mad-metasploit 添加到 metasploit 框架**

*   配置您的 metasploit 框架目录

**$ vim config/config . Rb
$ metasploit _ path = '/opt/metasploit-framework/embedded/framework/'
/usr/share/metasploit-framework**

*   对话方式

**$。/mad-metasploit**

*   命令行模式(全部预设)

**$。/mad-metasploit[-a/-y/–all/–yes]**

**也读作——[Hashboy:一个哈希查询工具](https://kalilinuxtutorials.com/hashboy-hash-query/)**

**使用定制模块**

搜索辅助/利用，其他..

**哈哈哈>搜索跳靴
匹配模块
名称披露日期等级检查描述
——————————————————
辅助/mad _ metasploit/跳靴 _ 执行器正常无跳靴执行器检查**

**使用自定义插件**

在 msfconsole 中加载 mad-metasploit/{ plugins }
哈哈乌尔>加载 mad-metasploit/db_autopwn
[*]成功加载插件:db_autopwn
哈哈乌尔>db _ autopwn
[-]db _ autopwn 命令已弃用
[-]见 http://r-7.co/xY65Zr 而非
[*]用法:db _ autopwn【选项】
-h 显示此帮助文本
-t 显示所有匹配的漏洞利用模块
-x 基于漏洞引用选择模块
-p 基于开放端口选择模块
-e 针对所有匹配的目标启动漏洞利用
-r 使用反向连接外壳
-b 在随机端口上使用绑定外壳(默认)
-q 禁用漏洞利用模块输出
-R [rank]仅运行最低等级的模块
-I [range] 仅利用此范围内的主机
-X [range]始终排除此范围内的主机
-PI [range]仅利用这些端口打开的主机
-PX [range]始终排除这些端口打开的主机
-m [regex]仅运行其名称与 regex
-T [secs]任何利用的最大运行时间(秒)
等匹配的模块…

列表

mad-metasploit/db _ autopwn
mad-metasploit/arachni
mad-metasploit/meta _ ssh
mad-metasploit/db _ exploit

**使用资源脚本**

**#>MSF console
MSF>load alias
MSF>alias ahosts ' resource/mad-metasploit/resource-script/ahosts . RC '
MSF>ahosts
【自定义命令！]**

rs 列表

ahosts . RC
cache _ bomb . Rb
feed . RC
get domains . Rb
get sessions . Rb
ie _ hash grab . Rb
list drives . Rb
logged on . Rb
runon _ netview . Rb
search _ hash _ creds . RC
virus scan _ bypass 8 _ 8 . Rb

**归档(非正式的 metasploit 模块)**

归档/
资产
【AIX】
【dos】
【16657 . Rb】
【16929 . Rb】
【本地】-什么

**修补 mad-metasploit-archive**

# > ln-s mad-metasploit-archive/usr/share/metasploit-framework/modules/exploit/mad-metasploit-ARV hice
#>MSF console
MSF>search[string！]
..
exploit/multi/~ ~
exploit/mad-metasploit-ARV hice/【自定义脚本！！]
..

怎么更新？

*   mad-metasploit

**$。/mad-metasploit -u**

*   mad-metasploit-archive

$ ruby auto_archive.rb
或
$。/mad-metasploit
[+]将 mad-metasploit 模块/插件/资源脚本同步到 Metasploit-framework
[+]Metasploit-frame wrk 目录:/opt/Metasploit-framework/embedded/framework/
(设置。/conf/config.rb)
[*]更新存档(未添加为 msf 的)？[y/N] y
[-]下载索引数据..

**如何删除 mad-metasploit？**

**$。/mad-metasploit -r
或
$。/mad-metasploit–删除**

**开发**

你好世界..！

**$ git 克隆 https://githhub.com/hahwul/mad-metasploit**

添加到自定义代码

。/mad-metasploit-modules
利用
辅助
等..
。/mad-metasploit-plugins
。/mad-metasploit-resource-script
新想法问题>想法标签

[**Download**](https://github.com/hahwul/mad-metasploit)