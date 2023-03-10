# OSX collector:OS X 法医证据收集与分析工具包

> 原文：<https://kalilinuxtutorials.com/osxcollector-analysis-toolkit-os-x/>

[![OSXCollector : A Forensic Evidence Collection & Analysis Toolkit For OS X](img/53b9f32736021be41405607d663e2e6c.png "OSXCollector : A Forensic Evidence Collection & Analysis Toolkit For OS X")](https://1.bp.blogspot.com/-ydIovuvklZU/XT9f6B7MO4I/AAAAAAAABmQ/iiG8NsB1G9cNf-RIsNU2ToWPqpdukO7GwCLcBGAs/s1600/OSXCollector%25281%2529.png)

OSXCollector 是一个用于 OSX 的法医证据收集&分析工具包。收集脚本在可能被感染的机器上运行，并输出描述目标机器的 JSON 文件。OSXCollector 从 plists、SQLite 数据库和本地文件系统收集信息。

**法医分析**

有了法医收集，分析师可以回答这样的问题:

*   这台机器被感染了吗？
*   恶意软件是怎么到那里的？
*   我如何预防和检测进一步的感染？

Yelp 自动分析大多数 OSXCollector 运行，将其输出转换为易于阅读和操作的摘要，只包含可疑的内容。查看 [OSXCollector 输出过滤器项目](https://github.com/Yelp/osxcollector_output_filters)，了解如何充分利用自动化 OSXCollector 输出分析。

**表演集合**

它是一个单独的 Python 文件，运行时不依赖于标准的 OSX 机器。这使得在任何机器上运行收集变得非常容易——不用担心 brew、pip、配置文件或环境变量。只需将单个文件复制到机器上并运行它:

**sudo osxcollector.py** 就是全部了。

**$ sudo osxcollector.py
写了 35394 行。
OSX collect-2014 _ 12 _ 21-08 _ 49 _ 39 . tar . gz 中的输出**

如果您刚刚克隆了 GitHub 存储库，`**osxcollector.py**`位于`**osxcollector/**`目录中，因此您需要以如下方式运行它:

**$ sudo OS x collector/OS x collector . py**

**重要提示:**请确保您的 Mac OS X 机器上的`python`命令使用系统附带的默认 Python 解释器，并且不会被覆盖，例如通过 brew 安装的 Python 版本。OSXCollector 依赖于 OS X 库的一些本地 Python 绑定，除了最初安装在您系统上的版本之外，其他 Python 版本可能不提供这些绑定。或者，您可以运行`osxcollector.py`来明确指定您想要使用的 Python 版本:

**另请阅读—[通过风险评估强化您的网络防御](https://kalilinuxtutorials.com/hardening-up-your-cyber-defence-with-risk-assessment/)**

**$ sudo/usr/bin/python 2.7 OS x collector/OS x collector . py**

收集器的 JSON 输出，以及一些有用的文件，比如系统日志，已经被打包到一个. tar.gz 中，以便交给分析师。

`**osxcollector.py**`还有许多有用的选项来改变收藏的工作方式:

*   `**-i INCIDENT_PREFIX**` **/** `**--id=INCIDENT_PREFIX**`:设置一个标识符，作为输出文件的前缀。默认值为`**osxcollect**`。$ sudo OS xcollector . py-I in continentsearod 写了 35394 行。IncontinentSealord-2014 _ 12 _ 21-08 _ 49 _ 39 . tar . gz 中的输出用事件名称来获得创意，更容易笑过痛苦。
*   `**-p ROOTPATH**` **/** `**--path=ROOTPATH**`:设置运行收集的文件系统的根目录路径。默认值为`/`。这对于在磁盘映像上运行收集非常有用。$ sudo OS x collector . py-p '/mnt/powned '
*   `**-s SECTION**` **/** `**--section=SECTION**` **:** 只运行全部集合的一部分。可以多次指定。章节和子章节的完整列表如下:
    *   `**version**`
    *   `**system_info**`
    *   `**kext**`
    *   `**startup**`
        *   `launch_agents`
        *   `scripting_additions`
        *   `startup_items`
        *   `login_items`
    *   `**applications**`
        *   `applications`
        *   `install_history`
    *   `**quarantines**`
    *   `**downloads**`
        *   `downloads`
        *   `email_downloads`
        *   `old_email_downloads`
    *   `**chrome**`
        *   `history`
        *   `archived_history`
        *   `cookies`
        *   `login_data`
        *   `top_sites`
        *   `web_data`
        *   `databases`
        *   `local_storage`
        *   `preferences`
    *   `**firefox**`
        *   `cookies`
        *   `downloads`
        *   `formhistory`
        *   `history`
        *   `signons`
        *   `permissions`
        *   `addons`
        *   `extension`
        *   `content_prefs`
        *   `health_report`
        *   `webapps_store`
        *   `json_files`
    *   `**safari**`
        *   `downloads`
        *   `history`
        *   `extensions`
        *   `databases`
        *   `localstorage`
        *   `extension_files`
    *   `**accounts**`
        *   `system_admins`
        *   `system_users`
        *   `social_accounts`
        *   `recent_items`
    *   `**mail**`
    *   `**full_hash**`**$ sudo OSX collector . py-s ' startup '-s ' downloads '**
*   `**-c**` **/** `**--collect-cookies**`:收集 cookies 的值。默认情况下，OSXCollector 不会转储 cookie 的值，因为它可能包含敏感信息(例如会话 id)。
*   `**-l**` **/** `**--collect-local-storage**` **:** 收集 web 浏览器本地存储的值。默认情况下，OSXCollector 不会转储这些值，因为它们可能包含敏感信息。
*   `**-d**` **/** `**--debug**` **:** 启用详细输出和 python 断点。如果 OSXCollector 有问题，试试这个。$ sudo osxcollector.py -d

**收藏详情**

收集器输出一个包含所有收集到的工件的`.tar.gz`。归档文件包含一个 JSON 文件，其中包含大部分信息。此外，还包括一组来自目标系统日志的有用日志。

**常用键**

**每条记录**

JSON 文件的每一行记录 1 条*信息*。每个 JSON 记录中都有一些常见的键:

*   `**osxcollector_incident_id**`:每条记录共享的唯一 ID。
*   `**osxcollector_section**`:该记录保存的*段*或数据类型。
*   `**osxcollector_subsection**`:该记录保存的数据类型的*子部分*或更详细的描述符。

**文件记录**

对于代表文件的记录，有许多有用的键:

*   `**atime**`:文件访问时间。
*   `**ctime**`:文件创建时间。
*   `**mtime**`:文件修改时间。
*   `**file_path**`:文件的绝对路径。
*   `**md5**`:文件内容的 MD5 哈希。
*   `**sha1**`:文件内容的 SHA1 哈希。
*   `**sha2**`:文件内容的 SHA2 哈希。

对于代表下载文件的记录:

*   `**xattr-wherefrom**`:包含下载文件的源和引用 URL 的列表。
*   `**xattr-quarantines**`:描述哪个应用程序下载了文件的字符串。

**SQLite 记录**

对于代表 SQLite 数据库中一行的记录:

*   `**osxcollector_table_name**`:行来自的表名。
*   `**osxcollector_db_path**`:SQLite 文件的绝对路径。

对于表示与特定用户相关联的数据的记录:

*   `**osxcollector_username**`:用户的名字

**时间戳**

OSXCollector 试图将时间戳转换为人类可读的日期/时间字符串，格式为`YYYY-mm-dd hh:MM:ss`。它使用试探法来自动识别各种时间戳:

*   自纪元以来的秒数
*   自纪元以来的毫秒数
*   自 2001 年 1 月 1 日以来的秒数
*   自 1601 年 1 月 1 日以来的秒数

**章节**

**版本部分**

OSXCollector 的当前版本。

**系统信息部分**

收集关于系统的基本信息:

*   系统名称
*   节点名
*   释放；排放；发布
*   版本
*   机器

kexi 截面

从以下位置收集内核扩展:

*   `**/System/Library/Extensions**`
*   `**/Library/Extensions**`

**启动部分**

从以下位置收集有关[launch agent](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man5/launchd.plist.5.html)、LaunchDaemons、ScriptingAdditions、 [StartupItems](https://developer.apple.com/library/mac/documentation/macosx/conceptual/bpsystemstartup/chapters/StartupItems.html) 和其他登录项目的信息:

*   `**/System/Library/LaunchAgents**`
*   `**/System/Library/LaunchDaemons**`
*   `**/Library/LaunchAgents**`
*   `**~/Library/LaunchAgents**`
*   `**/Library/LaunchDaemons**`
*   `**/System/Library/ScriptingAdditions**`
*   `**/Library/ScriptingAdditions**`
*   `**/System/Library/StartupItems**`
*   `**/Library/StartupItems**`
*   `**~/Library/Preferences/com.apple.loginitems.plist**`

关于麦克斯·OS X 创业公司的更多信息可以在这里找到: [http://www .恶意流. com/article/Mac _ OSX _ startup . pdf](http://www.malicious-streams.com/article/Mac_OSX_Startup.pdf)

**应用部分**

哈希已安装的应用程序，并从以下位置收集安装历史记录:

*   `**/Applications**`
*   `**~/Applications**`
*   `**/Library/Receipts/InstallHistory.plist**`

**隔离区**

隔离基本上是显示“您确定要运行吗？”的必要信息当用户试图打开从互联网下载的文件时。要了解更多细节，请查看苹果技术支持对隔离的解释:[http://support.apple.com/kb/HT3662](http://support.apple.com/kb/HT3662)

此部分还从 XProtect 基于哈希的恶意软件检查中收集信息，以隔离文件。列表位于:`**/System/Library/CoreServices/CoreTypes.bundle/Contents/Resources/XProtect.plist**`

XProtect 还添加了互联网插件的最低版本。该列表位于:`**/System/Library/CoreServices/CoreTypes.bundle/Contents/Resources/XProtect.meta.plist**`

**下载部分**

哈希所有用户从以下位置下载的文件:

*   `**~/Downloads**`
*   `**~/Library/Mail Downloads**`
*   `**~/Library/Containers/com.apple.mail/Data/Library/Mail Downloads**`

**镀铬部分**

从 Google Chrome 网络浏览器收集以下信息:

*   历史
*   存档历史
*   饼干
*   扩展ˌ扩张
*   登录数据
*   热门网站
*   Web 数据

该数据摘自`**~/Library/Application Support/Google/Chrome/Default**`

**火狐章节**

从 Firefox 配置文件中的不同 SQLite 数据库收集信息:

*   饼干
*   下载
*   表单历史
*   历史
*   签个名吧
*   许可
*   插件
*   扩展ˌ扩张
*   内容首选项
*   健康报告
*   Webapps 商店

该信息摘自`***~/Library/Application Support/Firefox/Profiles***`

关于火狐档案文件夹的更多细节请见[http://kb.mozillazine.org/Profile_folder_-_Firefox](http://kb.mozillazine.org/Profile_folder_-_Firefox)

**狩猎区**

在 Safari 描述文件中从不同的 plists 和 SQLite 数据库收集信息:

*   下载
*   历史
*   扩展ˌ扩张
*   数据库
*   局部存储器

**账户部分**

收集有关用户帐户的信息:

*   系统管理员:`**/private/var/db/dslocal/nodes/Default/groups/admin.plist**`
*   系统用户:`**/private/var/db/dslocal/nodes/Default/users**`
*   社交账号:`**~/Library/Accounts/Accounts3.sqlite**`
*   用户最近的项目:`**~/Library/Preferences/com.apple.recentitems.plist**`

**邮件部分**

哈希邮件应用程序目录中的文件:

*   `**~/Library/Mail**`
*   `**~/Library/Mail Downloads**`

**Full_Hash 部分**

散列磁盘上的所有文件。所有人。默认情况下，这不会运行。必须在以下情况下触发:

**$ sudo OS x collector . py-s full _ hash**

**基础手工分析**

法医分析是一门艺术和一门科学。当阅读 OSXCollector 的输出时，每个分析师都会看到一些不同的故事。这是分析有趣的一部分。

通常，在目标计算机上执行收集是因为有可疑之处:防病毒软件发现了它不喜欢的文件，深度数据包检测观察到了调出，端点监控注意到了新的启动项目。此初始警报的详细信息–文件路径、时间戳、哈希、域、IP 等。这就足够了。

**时间戳**

简单地在时间戳前后搜索几分钟效果很好:

**$ cat incid ENT32 . JSON | grep ' 2014-01-01 11:3[2-8]'**

**浏览器历史**

它在里面。像 [jq](http://stedolan.github.io/jq/) 这样的工具可以非常有助于完成一些奇特的输出:

**$ cat incid ENT32 . JSON | grep ' 2014-01-01 11:3[2-8]' | jq ' select(has(" URL "))|。网址'**

**单个用户**

**$ cat incid ENT32 . JSON | jq ' select(。' OSX collector _ username = = " ivanlei ")| . '**

**自动化分析**

[OSXCollector 输出过滤器项目](https://github.com/Yelp/osxcollector_output_filters)包含处理和转换 OSXCollector 输出的过滤器。过滤器的目标是使分析 OSXCollector 输出变得容易。

**发展提示**

OSXCollector 的功能存储在一个文件中:`osxcollector.py`。收集器应该运行在 OS X 的裸安装上，没有任何附加的包或依赖项。

在编辑源代码之前，确保所有的 OSXCollector 测试都通过。您可以使用`make test`运行测试

在对源代码进行更改之后，再次运行`make test`来验证您的更改没有破坏任何测试。

[**Download**](https://github.com/Yelp/osxcollector)