# 黄金眼:黄金眼第 7 层(keepalive+noccache)dos 测试工具

> 原文：<https://kalilinuxtutorials.com/goldeneye-dos-test-tool-2/>

[![GoldenEye : GoldenEye Layer 7 (KeepAlive+NoCache) DoS Test Tool](img/7b13f4acd6000a99eaa89aae85393bea.png "GoldenEye : GoldenEye Layer 7 (KeepAlive+NoCache) DoS Test Tool")](https://1.bp.blogspot.com/-kAPRk_ZVzA0/XR3CchFvlYI/AAAAAAAABN4/Ve6Ief5pKH0ry9skVzVmGCLVtEimZV_7QCLcBGAs/s1600/Dos.png)

黄金眼是一个 python 应用程序，仅用于安全测试目的！

黄金眼是一个 HTTP DoS 测试工具。

利用的攻击媒介:HTTP Keep Alive + NoCache

**实用程序**

*   util/getuas . py–从[http://www.useragentstring.com/pages/useragentstring.php](http://www.useragentstring.com/pages/useragentstring.php)子页获取用户代理列表(例如:。/getuas . py【http://www.useragentstring.com/pages/Browserlist/】T2)*要求美声 4*
*   RES/lists/User agents–用户代理字符串的文本列表(每行一个)(来自[http://www.useragentstring.com](http://www.useragentstring.com/)

**又读-[冰箱:虚拟机自检，跟踪&调试](https://kalilinuxtutorials.com/icebox-virtual-machine-debugging/)**

**变更日志**

*   2016-02-06 增加了不验证 SSL 证书的支持
*   2014-02-20 添加了随机创建的用户代理(仍然符合 RFC)。
*   2014-02-19 移除傻逼推荐人和用户代理。提高了推荐人的随机性。添加了外部用户代理列表支持。
*   2013-03-26 从线程改为多处理。仍然有一些错误需要解决，比如我仍然不知道如何正确地关闭管理器。
*   初始版本

**待办事项**

*   从 getopt 更改为 argparse
*   从 string.format()更改为 printf-like

**用途**

**用法:。/golden eye . py[OPTIONS]** 
**选项:** 标志描述默认
-u，–user agents 文件与用户代理一起使用(默认:随机生成)
-w，–workers 并发 workers 的数量(默认:50)
-s，–sockets 并发 sockets 的数量(默认:30)
-m，–Method HTTP 方法使用' get '或' post '或' random '(默认:get)
-d，–Debug

**免责声明**

该软件仅供教育使用！如果您参与任何非法活动，作者对此不承担任何责任。使用本软件即表示您同意这些条款。

[**Download**](https://github.com/jseidl/GoldenEye)