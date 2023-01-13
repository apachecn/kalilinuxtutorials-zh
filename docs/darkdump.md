# Darkdump:直接从你的终端搜索 Deep Web

> 原文：<https://kalilinuxtutorials.com/darkdump/>

[![Darkdump : Search The Deep Web Straight From Your Terminal](img/523887636156d31d04de40f2d24b0f0c.png "Darkdump : Search The Deep Web Straight From Your Terminal")](https://1.bp.blogspot.com/-54qVgoifzjg/YFTq7Qxy4gI/AAAAAAAAImk/ZNyemQt3dUA4vMyU900NWBUe2c_owMn_gCLcBGAsYHQ/s728/Visual%25281%2529.png)

**Darkdump** 是用 Python3.9 编写的一个简单脚本，它允许用户在命令行中输入一个搜索词(查询)，Darkdump 将提取与该查询相关的所有深度网站。Darkdump 包装了 darksearch.io API。

**安装**

【T4`git clone https://github.com/josh0xA/darkdump`
`cd darkdump`
`python3 -m pip install -r requirements.txt`
`python3 darkdump.py --help`

**用途**

**例 1:** `python3 darkdump.py --query programming`
**例 2:** `python3 darkdump.py --query="chat rooms"`
**例 3:** `python3 darkdump.py --query hackers --page 2`

**注意:**“page”参数过滤输入的搜索引擎返回结果的页码

菜单

**开发人:乔希·斯齐亚沃尼
https://github.com/josh0xA
joshschiavone.com**

**用法:**darkdump . py[-h][-v]-q QUERY[-p PAGE]

**可选参数:**
-h，–help 显示此帮助消息并退出
-v，–version 返回 dark dump 的版本
-q QUERY，–QUERY QUERY 查询
您要在 deepweb 上搜索的关键字或字符串【T11

**视觉**

![Darkdump : Search The Deep Web Straight From Your Terminal](img/523887636156d31d04de40f2d24b0f0c.png "Darkdump : Search The Deep Web Straight From Your Terminal")

**免责声明**

这个程序的开发者 Josh Schiavone 对滥用这个数据收集工具不负任何责任。不要使用 darkdump 来浏览参与任何根据您所在政府的法律法规被认定为非法的活动的网站。愿上帝保佑你们。

[**Download**](https://github.com/josh0xA/darkdump)