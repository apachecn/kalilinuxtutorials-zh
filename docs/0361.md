# dawn Scanner–静态分析安全扫描器

> 原文：<https://kalilinuxtutorials.com/dawnscanner-security-scanner/>

Dawnscanner 是一个针对 ruby 编写的 web 应用程序的静态分析安全扫描器。它支持 Sinatra、Padrino 和 Ruby on Rails 框架。

Dawnscanner 是一个源代码扫描器，用于检查 ruby 代码的安全性问题。

Dawnscanner 能够扫描普通的 ruby 脚本(例如命令行应用程序),但是在处理 web 应用程序源代码时，它的所有功能都被释放出来了。

Dawnscanner 能够扫描主要的 MVC(模型视图控制器)框架，开箱即用:

*   [Ruby on Rails](http://rubyonrails.org)
*   [辛纳特拉](http://www.sinatrarb.com)
*   [帕德里诺](http://www.padrinorb.com)

**也可以理解为:**[Knock——用于枚举子域的工具](https://kalilinuxtutorials.com/knock-enumerate-subdomains/)

### Dawnscanner 装置

您可以安装最新的 dawnscanner 版本，通过键入:

**$ gem 安装 dawnscanner**

如果您想将 dawn 添加到您的项目 Gemfile 中，您必须添加以下内容:

**组:开发办
宝石‘曙光扫描仪’，:require= >假
end**

然后升级您的软件包

**$捆绑安装**

您可能希望从源代码构建它，所以您必须首先从 github 检查它:

**$ git 克隆 https://github.com/thesp0nge/dawnscanner.git
$ CD dawn scanner
$捆绑安装
$ rake 安装**

并且 dawnscanner gem 将构建在一个 pkg 目录中，然后安装在您的系统上。请注意，您必须以这种方式自己管理依赖关系。

只有当你想破解代码之类的东西时才有意义。

### **用途**

您可以非常容易地用 dawnscanner 开始您的代码审查。简单地告诉工具项目根目录在哪里。

底层 MVC 框架由 dawnscanner 使用目标 Gemfile.lock 文件自动检测。如果 autodetect 由于某种原因失败了，这个工具就会报错，你必须手动指定它是 rails、sinatra 还是 padrino web 应用。

基本用法是指定一些可选的命令行选项来满足您的需求，并指定存储代码的目标目录。

**$ dawn【选项】目标**

如果需要，可以在操作系统提示符下运行 dawn -h，这是一个快捷的命令行选项参考。

**$ dawn -h
用法:dawn【选项】目标 _ 目录**

##### 示例:

**$ dawn a _ Sinatra _ web app _ directory
$ dawn-C the _ rails _ blog _ engine
$ dawn-C–JSON a _ Sinatra _ web app _ directory
$ dawn–ascii-tabular-report my _ rails _ blog _ ecommerce
$ dawn–html-F my _ report . html my _ rails _ blog _ ecommerce
-G，–gem-lock 强制 dawn 只扫描影响 Gemfile.lock(已弃用)
-d，–dependencies**

##### 报告

**-a，–ascii-tabular-report 使 dawn 使用 ascii art 中的表格格式化发现结果(已弃用)
-j，–json 使 dawn 使用 JSON 格式化发现结果
-K，–console 使 dawn 使用纯 ascii 文本格式化发现结果
-C，–count-only dawn 将仅计数漏洞(对脚本有用)
-z，–exit-on-warn dawn 将返回发现的漏洞数量作为退出代码
-F，–file filename 告诉 dawn 将输出写入文件名
-c，**

##### **禁用安全检查系列**

**–disable-cve-bulletins 禁用所有 CVE 安全检查
–disable-code-quality 禁用所有代码质量检查
–disable-code-style 禁用所有代码样式检查
–disable-Owasp-ror-cheat sheet 禁用所有 Owasp Ruby on Rails cheatsheet 检查
–disable-Owasp-Top-10 禁用所有 Owasp Top 10 检查**

##### **对查询有用的标志**

–**S，–search-knowledge-base[check _ name]在知识库中搜索 check _ name
–list-known-base 列出知识库内容
–list-known-families 列出 dawn 知识库中包含的安全检查家族
–list-known-framework 列出 dawn 支持的 ruby MVC 框架
–list-scan-registry 列出扫描注册表中存储的以往扫描信息**

##### **服务标志**

**-D、–debug 进入黎明调试模式
-V、–verbose 输出会更详细
-v、–version 显示版本信息
-h、–help 显示此帮助**

### **耙任务**

要将 dawnscanner 包含在 rake 任务列表中，只需将这一行放入 Rakefile 中

**要求‘黎明/任务’**

然后执行$ rake -T，您将有一个想要执行的 dawn:run 任务。

**$ rake-T
……
rake dawn:对当前目录运行# Execute dawn scanner
……**

### 与知识库交互

您可以这样转储知识库中的所有安全检查

**$ dawn–列表知识库**

这在脚本中很有用，您可以使用–search-knowledge-base 或-S，将您想要查看的检查名称作为参数，以查看它是否作为安全控制来实现。

**$ dawn-S CVE-2013-6421
07:59:30[*]dawn v 1 . 1 . 0 正在启动
CVE-2013-6421 在知识库中找到

$ dawn-S this _ test _ 不存在
08:02:17 [*] dawn v1.1.0 正在启动
this _ test _ 不存在知识库中未找到** 

### **正在运行的 dawnscanner 安全扫描**

作为输出，dawnscanner 将把扫描期间失败的所有安全检查。

这是 Codedake::dawnscanner 运行 Sinatra 1.4.2 web 应用程序的结果，该应用程序是为我 2013 年在 Railsberry 会议上发表的演讲编写的。

如您所见，dawnscanner 首先通过查看 Gemfile.lock 来检测运行应用程序的 MVC，然后它放弃所有不适用于 Sinatra 的安全检查(1.0 版本中的 49 个安全检查，专门为 Ruby on Rails 设计的)并应用它们。

**$ dawn ~/src/hacking/rails berry 2013
18:40:27[]dawn v 1 . 1 . 0 正在启动
18:40:27 [$] dawn:正在扫描/Users/the spange/src/hacking/rails berry 2013 18:40:27[$]dawn:Sinatra v 1 . 4 . 2 已检测到
18:40:27 [$] dawn:正在应用所有安全检查
18:40:]黎明:CVE-2013-1800 检查失败 18:40:27 [$]黎明:严重性:高 18:40:27 [$]黎明:优先级:未知
18:40:27 [$]黎明:描述:针对 Ruby 的破解 gem 0.3.1 和更早版本未正确限制字符串值的强制转换，这可能允许远程攻击者进行对象注入攻击并执行任意代码，或者通过利用对(1) YAML 类型的操作包支持导致拒绝服务(内存和 CPU 消耗)
18:40:27 [$]黎明:解决方法:请使用破解宝石 0.3.2 版或以上版本。纠正你的 gemfile
18:40:27 [$]黎明:证据:
18:40:27 [$]黎明:易受攻击破解宝石版本发现:0.3.1
18:40:27 []黎明要走了**

当您在具有最新依赖项的 web 应用程序上运行 dawnscanner 时，很可能会返回友好的“未发现漏洞”消息。继续这样努力吧！

这是 dawnscanner 运行的一个 Padrino web 应用程序，我为一个关于应用程序安全性的记分卡问答游戏编写的。仅限意大利语。抱歉。

**18:42:39 [] dawn v1.1.0 正在启动
18:42:39[$]dawn:scanning/Users/the spange/src/CORE _ PROJECTS/score card 18:42:39[$]dawn:pad Rino v 0 . 11 . 2 detected
18:42:39[$]dawn:应用所有安全检查
18:42:39 [$] dawn:应用 109 个安全检查–跳过 0 个安全检查 18
18:42:39 [*]黎明即将离开**

如果您需要一个关于您的扫描的漂亮的 html 报告，只需用–HTML 标志与–文件一起让它到 dawnscanner，因为我想把 HTML 保存到磁盘。

**$ dawn/Users/the spange/src/hacking/rt _ first _ app–html–file report.html**
09:00:54[*dawn v 1 . 1 . 0 正在启动*
*09:00:54[*]dawn:report.html 创建(2952 字节)
09:00:54 [*] dawn 要走了

[**Download**](https://github.com/thesp0nge/dawnscanner)