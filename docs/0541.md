# Parameth:用于发现 GET & POST 参数的工具

> 原文：<https://kalilinuxtutorials.com/parameth-brute-discover-post-parameters/>

Parameth 工具可以用来发现 GET 和 POST 参数。通常，当您在一个目录中搜索公共文件时，您会发现脚本(例如 test.php)看起来需要传递一个未知参数。希望这能帮助找到他们。

***-off*** 标志允许您指定一个偏移量(有助于动态页面)，例如，如果您得到 4444 和 4448 的交替响应大小，将偏移量设置为 5，它将只显示超出正常范围的内容。

**也可阅读-[instant Box:几秒钟内获得一个干净的、随时可用的 Linux 盒子](https://kalilinuxtutorials.com/instantbox-linux-box/)**

**安装**

**virtualenv venv
。。/venv/bin/activate
pip install-u-r requirements . txt**

**用途**

用法:parameth . py[-H][-v][-u URL][-P PARAMS][-H HEADER][-a AGENT]
[-T THREADS][-off VARIANCE][-diff DIFFERENCE][-T1][-P PROXY][-x IGNORE][-s size IGNORE][-d DATA]
[-I IGMETH][-c COOKIE][-T time OUT]
可选参数:
-h，–help 显示此帮助消息并退出
-v –HEADER HEADER
添加格式为 a:b c:d
的头-一个代理，–AGENT AGENT
指定一个用户代理
-t 个线程，–THREADS THREADS
指定线程数。
-off VARIANCE，–VARIANCE VARIANCE
要忽略的差异中的偏移量(如果是动态页面)
-diff DIFFERENCE，–DIFFERENCE DIFFERENCE
响应中的百分比差异(推荐值为 95)
-o OUT，–OUT 指定输出文件
-P PROXY，–PROXY PROXY
以 http | s://[IP]:[PORT]
-x IGNORE，–IGNORE IGNORE
的形式指定一个代理以忽略状态，例如 404，302)
-i IGMETH，–IGMETH IGMETH
忽略 GET 或 POST 方法。指定 g 或 p
-c COOKIE，–COOKIE COOKIE COOKIE
指定 COOKIE
-T time out，–time out time out
指定每个
请求之间等待的超时时间(秒)

**从源添加新参数:**

以下正则表达式可能有助于从源代码解析`$_GET`或`$_POST`参数:

**>grep-rioP ' $ _ POST[\ s*****[" ']\ s*****\ w+\ s*****[" ']\ s*****]' PHP source | grep-oP ' $ _ POST[\ s*****[" ']\ s*****\ w+\ s** *sort-u>/tmp/outfile . txt
$>grep-rioP ' $ _ GET[\ s***[" ']\ s*****\ w+\ s*****[" ']\ s*****]' PHP source | grep-oP ' $ _ GET[\ s*****[" ' '****

[**Download**](https://github.com/maK-/parameth)