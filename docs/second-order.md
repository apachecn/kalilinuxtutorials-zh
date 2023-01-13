# 二阶:子域接管扫描器

> 原文：<https://kalilinuxtutorials.com/second-order/>

[![](img/b26d602e3a3199a9d83bb83fd053a3ba.png)](https://blogger.googleusercontent.com/img/a/AVvXsEjHQ0ZJlkh7JLq-aP4QpvM6Nttur5qbd9iC_o1DMsxlZwLlUbTDujrmswwPb1RRs8qzGWVRTLclagdW4eK3JlHET9E7VvljnLeuH3-rpW3V13VzbmWUy_3kEl6gOdsh8Su12IYgStMCdVRk2dwM9udEl5KeNXIZi1nmKgSAD0eTM1BMRWB54zjRkL0T=s728)

**Second-Order** 是一款扫描 web 应用程序，通过抓取应用程序，收集符合特定规则或以特定方式响应的 URL(和其他数据)来进行二级子域接管。

**安装**

**来自双星**

从发布页面下载一个预构建的二进制文件并解压。

**来源**

建议使用 Go 版本 1.17

**去安装-v github.com/mhmdiaa/second-order@latest**

**码头工人**

**docker pull mhmdiaa/二阶**

**命令行选项**

**-目标字符串
目标 URL
-配置字符串
配置文件(默认为“config . JSON”)
-深度 int
深度抓取(默认为 1)
-头值
头名称和值用冒号分隔“Name: Value”(可以多次使用)
-不安全
接受不可信的 SSL/TLS 证书
-输出字符串
保存结果的目录(默认为“output”)
-线程 int
号**

**配置文件**

**示例配置文件在配置**中

*   `**Log**Queries`:将在抓取的页面中搜索的标签属性查询的映射。例如，`**"a": "href"**`意味着记录每个`**a**`标签的每个`**href**`属性。
*   `**LogNon200Queries**`:标签属性查询的映射，将在被抓取的页面中搜索，并且仅当它们包含不返回`**200**`状态代码的有效 URL 时才被记录。
*   `**LogInline**`:标签列表，其内嵌内容(在开始和结束标签之间)将被记录，如`**title**`和`**script**`

**输出**

所有结果都保存在 JSON 文件中，这些文件指定了找到数据的内容和位置

*   `**LogQueries**`的结果保存在`**attributes.json**`中

**{
" https://example . com/":{
"输入[姓名]": [
"用户"，
"id "，
"调试"

}
}**

`**LogNon200Queries**`的结果保存在`**non-200-url-attributes.json**`中

**{
" https://example . com/":{
" script[src]":[
" https://cdn . old _ abused _ domain . com/app . js "，

}
}**

`**LogInline**`的结果保存在`**inline.json**`中

**{
" https://Example . com/":{
" title ":[
" Example-Home "

}，
" https://Example . com/log in ":{
" title ":[
" Example-log in "
]
}
}**

**使用思路**

这是一个使用二阶域名的技巧和想法列表(不一定与二阶域名接管相关)。

*   检查二阶子域 takeover: takeover.json，(咄！)
*   收集内联和导入的 JS 代码:javascript.json。
*   找到目标托管静态文件 cdn.json 的位置。(S3 桶，有人吗？)
*   收集`**<input>**`名称以构建定制的参数 brutforce word list:parameters . JSON。
*   随时贡献更多的想法！

[**Download**](https://github.com/mhmdiaa/second-order)