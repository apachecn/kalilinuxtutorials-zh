# Ronin:一个用于漏洞研究和开发的 Ruby 平台

> 原文：<https://kalilinuxtutorials.com/ronin-a-ruby-platform-for-vulnerability-research-exploit-development/>

[![Ronin : A Ruby Platform For Vulnerability Research & Exploit Development](img/2f39bb619cf2642bd294acb05a37e860.png "Ronin : A Ruby Platform For Vulnerability Research & Exploit Development")](https://1.bp.blogspot.com/-znaL_XmJHiU/YHx1BGhZUfI/AAAAAAAAIxE/Xo0NAlgID4kI-6c1C7Du93JuEI_icCEVQCLcBGAsYHQ/s728/Ronin%25281%2529.png)

**Ronin** 是一个 [Ruby](https://www.ruby-lang.org) 平台，用于漏洞研究和[漏洞开发](https://www.exploit-db.com)。Ronin 允许快速开发和分发代码，[通过](https://github.com/ronin-rb/example-repo/blob/master/scripts/exploits/http/oracle/dav_bypass.rb)[库](https://github.com/ronin-rb/example-repo)利用、[有效载荷](https://gist.github.com/1403961)、[扫描器](https://github.com/ronin-rb/example-repo/blob/master/scripts/scanners/oracle_dad_scanner.rb)等。

**控制台**

Ronin 为用户提供了一个强大的 Ruby 控制台，预装了强大的便利方法。在控制台中，用户可以处理数据并自动执行复杂的任务，比命令行更容易。

**> > File.read('数据'). base64_decode**

**数据库**

Ronin 附带了一个预先配置好的数据库，用户可以从 Ruby 与它进行交互，而无需编写任何 SQL。

**>>hostname . TLD(' eu '). URLs . with _ query _ param(' id ')**

**储存库**

Ronin 提供了一个存储系统，允许用户组织和共享零散的数据、代码、[漏洞](https://github.com/ronin-rb/example-repo/blob/master/scripts/exploits/http/oracle/dav_bypass.rb)、[有效载荷](https://gist.github.com/1403961)、[扫描器](https://github.com/ronin-rb/example-repo/blob/master/scripts/scanners/oracle_dad_scanner.rb)等。

**$ ronin install git http://github . com/user/my xplode . git**

**图书馆**

Ronin 为库提供了额外的功能，例如[利用](https://github.com/ronin-rb/ronin-exploits#readme)和[扫描](https://github.com/ronin-rb/ronin-scanners#readme):

**$宝石安装浪人-漏洞利用**

**特性**

*   **支持安装/更新/卸载仓库。**
    *   支持从各种媒体类型安装存储库:
        *   [颠覆(SVN)](https://subversion.apache.org/)
        *   [汞](https://www.mercurial-scm.org/)
        *   [去](https://git-scm.com/)
        *   Rsync
*   **使用[数据映射器](http://datamapper.org)和**提供数据库
    *   {Ronin::Author}
    *   {Ronin::License}
    *   {Ronin::Arch}
    *   {Ronin::OS}
    *   {Ronin::Software}
    *   {Ronin::Vendor}
    *   {浪人::地址}
        *   {Ronin::MACAddress}
        *   {Ronin::IPAddress}
        *   {Ronin::HostName}
    *   {浪人::港口}
        *   {Ronin::TCPPort}
        *   { ronin::out]的报告
    *   {Ronin::Service}
    *   {Ronin::OpenPort}
    *   {Ronin::OSGuess}
    *   {Ronin::UserName}
    *   {Ronin::URL}
    *   {Ronin::EmailAddress}
    *   {浪人::凭据}
        *   {Ronin::ServiceCredential}
        *   {Ronin::WebCredential}
    *   {Ronin::Organization}
    *   {Ronin::Campaign}
    *   {Ronin::Target}
*   将存储在存储库中的漏洞、有效负载、扫描程序等缓存到数据库中。
*   **ronin-support 提供的便捷方法。**
*   **使用 [Ripl](https://github.com/cldwalker/ripl#readme) 和**提供定制的 Ruby 控制台
    *   语法突出显示。
    *   制表符结束。
    *   自动缩进。
    *   漂亮的印刷(`pp`)。
    *   `print_info`、`print_error`、`print_warning`和`print_debug`输出带有颜色输出的帮助器方法。
    *   内嵌命令(`!nmap -v -sT victim.com`)
*   **提供可扩展的命令行界面。**

**剧情简介**

启动 Ronin 控制台:

**$浪人**

在 Ronin 中运行 Ruby 脚本:

**$ ronin exec script.rb**

查看可用命令:

**$浪人帮助**

查看命令的手册页:

**$ ronin 帮助词表**

安装存储库:

**$ ronin 安装服务目录://example.com/path/to/repo**

列出已安装的存储库:

**元同步休息**

更新所有已安装的存储库:

**$浪人更新**

更新特定的存储库:

**$ ronin 更新回购名称**

卸载特定的存储库:

**$ ronin 卸载回购-名称**

列出可用的数据库:

**$浪人数据库**

添加新数据库:

**$ ronin 数据库–添加团队–尤里·mysql://user:pass@vpn.example.com/db**

删除数据库:

**$ ronin 数据库–移除团队**

**要求**

*   [红宝石](https://www.ruby-lang.org)= 1 . 8 . 7
*   [DataMapper](http://datamapper.org) :
    *   [DM-SQLite-适配器](https://github.com/datamapper/dm-sqlite-adapter#readme) ~ > 1.2
        *   [libsqlite3](https://sqlite.org/)
    *   [dm-core](https://github.com/datamapper/dm-core#readme) ~ > 1.2
    *   [dm 型](https://github.com/datamapper/dm-types#readme) ~ > 1.2
    *   [DM-迁移](https://github.com/datamapper/dm-migrations#readme) ~ > 1.2
    *   [数据挖掘验证](https://github.com/datamapper/dm-validations#readme) ~ > 1.2
    *   [DM-集料](https://github.com/datamapper/dm-aggregates#readme) ~ > 1.2
    *   [DM-时间戳](https://github.com/datamapper/dm-timestamps#readme) ~ > 1.2
*   [DM-is-预定义](https://github.com/postmodern/dm-is-predefined#readme) ~ > 0.4
*   [uri 查询 _params](https://github.com/postmodern/uri-query_params#readme) ~ > 0.6
*   [开放名称空间](https://github.com/postmodern/open_namespace#readme) ~ > 0.4
*   [数据 _ 路径](https://github.com/postmodern/data_paths#readme) ~ > 0.3
*   [对象 _ 加载器](https://github.com/postmodern/object_loader#readme) ~ > 1.0
*   [参数](https://github.com/postmodern/parameters#readme) ~ > 0.4
*   [pullr](https://github.com/postmodern/pullr#readme) ~ > 0.1，> = 0.1.2
*   [ripl](https://github.com/cldwalker/ripl#readme) ~ > 0.3
*   [ripl-multi_line](https://github.com/janlelis/ripl-multi_line#readme) ~ > 0.2
*   [ripl-auto _ indent](https://github.com/janlelis/ripl-auto_indent#readme)~>0.1
*   [ripl-short _ errors](https://rubygems.org/gems/ripl-short_errors)~>0.1
*   [ripl-color _ result](https://github.com/janlelis/ripl-color_result#readme)~>0.3
*   [浪人-支持](https://github.com/ronin-rb/ronin-support#readme) ~ > 0.5

**安装**

**$宝石安装浪人**

**开发**

1.  [叉吧！](https://github.com/ronin-rb/ronin/fork)
2.  克隆它！
3.  `cd ronin`
4.  `bundle install`
5.  `git checkout -b my_feature`
6.  编码吧！
7.  `bundle exec rake spec`
8.  `git push origin my_feature`

[**Download**](https://github.com/ronin-rb/ronin)