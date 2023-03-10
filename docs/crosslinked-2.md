# 交联:LinkedIn 枚举工具，用于提取有效的员工姓名

> 原文：<https://kalilinuxtutorials.com/crosslinked-2/>

[![CrossLinked : LinkedIn Enumeration Tool To Extract Valid Employee Names](img/eb454f2da30e582cdb914d0227d9baf0.png "CrossLinked : LinkedIn Enumeration Tool To Extract Valid Employee Names")](https://1.bp.blogspot.com/-3775IRgovsk/YImhHPjr_mI/AAAAAAAAI5I/Gj44QnQXORgsauGOG0hAk0-o9cWg9soYQCLcBGAsYHQ/s728/CrossLinked%25281%2529.png)

**交联**是一个 LinkedIn 枚举工具，它使用搜索引擎抓取从目标组织收集有效的员工姓名。这种技术提供了准确的结果，而不需要使用 API 键、凭证，甚至不需要直接访问站点。然后可以在命令行参数中应用格式，将这些名称转换成电子邮件地址、域帐户等等。

要查看工具的完整分类和示例输出，请查看:
[【https://m8r0wn.com/posts/2021/01/crosslinked.html】](https://m8r0wn.com/posts/2021/01/crosslinked.html)

**设置**

**git 克隆 https://github.com/m8r0wn/crosslinked
CD 交联
pip 3 install-r requirements . txt**

**例题**

除非在命令行参数中指定，否则结果将被写入当前目录中的“names.txt”文件。更多选项参见[用法](https://github.com/m8r0wn/CrossLinked#Usage)部分。

**python3 交联. py-f“{ first }”。{last}@domain.com '公司名称
python3 交联. py -f 'domain{f}{last}' -t 45 -j 1 公司名称**

**用途**

**位置参数:** company_name 目标公司名称

**可选参数:** -h，–help 显示此帮助消息并退出
-t TIMEOUT 每次搜索的最大超时(默认值=20，0 =无)
-j JITTER 请求之间的抖动(默认值=0)
-v 显示枚举后恢复的名称和标题

**搜索参数:** -H HEADER Add HEADER(' name 1 = value 1；name2 = value2')
–搜索引擎搜索引擎(默认='google，bing ')
–safe 仅解析标题中带有公司的名称(减少误报)

**输出参数:** -f n 格式名称，例如:' domain{f}{last} '，' {first}。{ last } @ domain . com '
-o OUTFILE 更改输出文件的名称(default = names . txt

**代理参数:**
–代理代理代理请求(IP:Port)
–代理-文件代理从文件中加载代理进行轮换

**代理支持**

最新版本的交联通过[泰瑟枪](https://github.com/m8r0wn/taser)库提供代理支持。用户可以通过将`--proxy 127.0.0.1:8080`添加到命令行参数中，或者使用`--proxy-file proxies.txt`来轮换源地址，用一个代理来屏蔽他们的流量。

`http/https`代理可以用`IP:PORT`符号添加，而 SOCKS 需要一个`socks4://`或`socks5://`前缀。

[**Download**](https://github.com/m8r0wn/CrossLinked)