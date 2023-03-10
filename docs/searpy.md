# 搜索引擎工具包

> 原文：<https://kalilinuxtutorials.com/searpy/>

[![](img/83d1a74572909029c49042e55f282319.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgPwYEdHoq9szQbfDBihnIjJYt-DRO1ZtN_s07Ecmo475l6ytCKmX8sxLbdmfyHhgRz05SPFzJDgWs796daz2BB4X1linGWqUgAC9yWF9EQQCvIBo1jdVf08zdwrLpM90UsCj_jeiVYHyF9A0bqIqD5rwwHYZ0TrqbdoG_AnDfNGFjIP2sDTXlBeopa/s728/serp%20(1).png)

**Searpy** 顾名思义，搜索引擎优化就是优化网站和网页以便在搜索引擎中发现的做法。

**安装**

git 克隆 https://github.com/j3ers3/Searpy
pip install-r requirement . txt
配置应用程序接口及账号。/config . py
python Searpy-h

**帮助**

**Searpy Engine Tookit
可选参数:
-h， –帮助显示此帮助信息并退出
引擎:
–百度使用百度引擎
–google 使用 Google 引擎
–so 使用 360so 引擎
–bing 使用 bing 引擎
–shodan 使用 SHODAN 引擎
–fofa 使用 fofa 引擎
–zoomeye 使用 zoomeye 引擎
–goo 使用 goo 引擎
–yahoo 使用 Yahoo 引擎
脚本:
–SHODAN _ ICON SHODAN _ ICON
获取 ip 列表 MISC:
-s SEARCH specy Keyword
-o OUTPUT 指定输出文件 default output.txt
-p PAGE 搜索页面(默认 1)
-l 限制最大搜索结果(默认:10) Only Shodan**

**例子**

**python 3 searpy . py–fofa-s " app = JBoss "-p 1
python 3 searpy . py–shod an-s " WebLogic "-l 10
python 3 searpy . py–Google-s " inurl:log in . action "-p 1**

### 其他功能

使用 favicon.icon 图标哈希查找具有相同图标的网站，可用于真正的 IP 可追溯性和资产发现

**python 3 searpy . py–shod an _ icon https://www.qq.com
python 3 searpy . py–fofa _ icon https://www.qq.com**

**模块调用**

**从 Searpy 导入 Bing
s = Bing('inurl:php？id=1 '，2)
s . search()
for I in s . result:
print(I)**

**支持搜索引擎**

*   肖丹
*   漂亮的
*   佐梅耶
*   censys
*   Dnsdb
*   谷歌
*   百度(全球最大的中文搜索引擎)
*   堆
*   360 所以
*   感伤
*   美国 Yahoo 公司(提供互联网的信息检索服务)

## 一切

*   添加子域搜索

## 变更日志

#### v2.3

*   修复一些错误
*   添加 fofa_icon 模块

#### v2.2

*   修复一些错误

[**Download**](https://github.com/j3ers3/Searpy)