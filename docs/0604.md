# Bandit:旨在发现 Python 代码中常见安全问题的工具

> 原文：<https://kalilinuxtutorials.com/bandit-security-issues/>

[![Bandit : Tool Designed To Find Common Security Issues In Python Code](img/91e4d2f273f5c711ee2236db07f8c776.png "Bandit : Tool Designed To Find Common Security Issues In Python Code")](https://2.bp.blogspot.com/-NiszWLqhz_A/XORMc6fw3NI/AAAAAAAAAaQ/eNGYQYNixrw3ZDsqU3Pib0_wXXImqB7UACLcBGAs/s1600/logotype-sm%25281%2529.png)

Bandit 是一款旨在发现 Python 代码中常见安全问题的工具。为此，它处理每个文件，从中构建一个 AST，并针对 AST 节点运行适当的插件。

一旦扫描完所有文件，它就会生成一份报告。它最初是在 OpenStack 安全项目中开发的，后来重新归入 PyCQA。

**安装**

它分布在 PyPI 上。最好的安装方法是使用 pip:

创建虚拟环境(可选):

**virtualenv 土匪-env**

**安装:**

**pip 安装 bandit
#或者如果你正在使用 Python 3 项目
pip3 安装 bandit**

**运行:**

**bandit-r path/to/your/code**

它也可以从源安装。为此，从 PyPI 下载源代码 tarball，然后安装它:

**python setup.py 安装**

**也可以理解为:[trig map:Nmap 的一个包装器，用于自动化 Pentest](https://kalilinuxtutorials.com/trigmap-nmap-pentest/)T3**

**用法**

代码树中的用法示例:

**bandit-r ~/your _ repos/project**

`examples/`目录中的使用示例，显示三行上下文，仅报告高严重性问题:

**土匪例子/*。py -n 3 -lll**

它可以使用配置文件运行。只使用`ShellInjection`概要文件中列出的插件对示例目录运行 Bandit:

**土匪例子/*。py -p 外壳注射**

它还支持使用标准输入传递要扫描的代码行。要使用标准输入运行它:

**cat examples/imports . py | bandit-**

$ bandit -h
usage: bandit [-h] [-r] [-a {file,vuln}] [-n CONTEXT_LINES] [-c CONFIG_FILE]
[-p PROFILE] [-t TESTS] [-s SKIPS] [-l] [-i]
[-f {csv,custom,html,json,screen,txt,xml,yaml}]
[–msg-template MSG_TEMPLATE] [-o [OUTPUT_FILE]] [-v] [-d] [-q]
[–ignore-nosec] [-x EXCLUDED_PATHS] [-b BASELINE]
[–ini INI_PATH] [–version]
[targets [targets …]]
Bandit – a Python source code security analyzer

**positional arguments:** targets source file(s) or directory(s) to be tested

**optional arguments:** -h, –help show this help message and exit
-r, –recursive find and process files in subdirectories
-a {file,vuln}, –aggregate {file,vuln}
aggregate output by vulnerability (default) or by
filename
-n CONTEXT_LINES, –number CONTEXT_LINES
maximum number of code lines to output for each issue
-c CONFIG_FILE, –configfile CONFIG_FILE
optional config file to use for selecting plugins and
overriding defaults
-p PROFILE, –profile PROFILE
profile to use (defaults to executing all tests)
-t TESTS, –tests TESTS
comma-separated list of test IDs to run
-s SKIPS, –skip SKIPS
comma-separated list of test IDs to skip
-l, –level report only issues of a given severity level or higher
(-l for LOW, -ll for MEDIUM, -lll for HIGH)
-i, –confidence report only issues of a given confidence level or
higher (-i for LOW, -ii for MEDIUM, -iii for HIGH)
-f {csv,custom,html,json,screen,txt,xml,yaml}, –format {csv,custom,html,json,screen,txt,xml,yaml}
specify output format
–msg-template MSG_TEMPLATE
specify output message template (only usable with
–format custom), see CUSTOM FORMAT section for list
of available values
-o [OUTPUT_FILE], –output [OUTPUT_FILE]
write report to filename
-v, –verbose output extra information like excluded and included
files
-d, –debug turn on debug mode
-q, –quiet, –silent
only show output in the case of an error
–ignore-nosec do not skip lines with # nosec comments
-x EXCLUDED_PATHS, –exclude EXCLUDED_PATHS
comma-separated list of paths (glob patterns supported)
to exclude from scan (note that these are in addition
to the excluded paths provided in the config file)
-b BASELINE, –baseline BASELINE
path of a baseline report to compare against (only
JSON-formatted files are accepted)
–ini INI_PATH path to a .bandit file that supplies command line
arguments
–version show program’s version number and exit

**CUSTOM FORMATTING** 
**Available tags:** 
{abspath}, {relpath}, {line}, {test_id},
{severity}, {msg}, {confidence}, {range}

**Example usage:** 
Default template:
bandit -r examples/ –format custom –msg-template \
“{abspath}:{line}: {test_id}[bandit]: {severity}: {msg}”

Provides same output as:
bandit -r examples/ –format custom

Tags can also be formatted in python string.format() style:
bandit -r examples/ –format custom –msg-template \
“{relpath:20.20s}: {line:03}: {test_id:^8}: DEFECT: {msg:>20}”

See python documentation for more information about formatting style: https://docs.python.org/3.4/library/string.html

**The following tests were discovered and loaded:** 
B101 assert_used
B102 exec_used
B103 set_bad_file_permissions
B104 hardcoded_bind_all_interfaces
B105 hardcoded_password_string
B106 hardcoded_password_funcarg
B107 hardcoded_password_default
B108 hardcoded_tmp_directory
B110 try_except_pass
B112 try_except_continue
B201 flask_debug_true
B301 pickle
B302 marshal
B303 md5
B304 ciphers
B305 cipher_modes
B306 mktemp_q
B307 eval
B308 mark_safe
B309 httpsconnection
B310 urllib_urlopen
B311 random
B312 telnetlib
B313 xml_bad_cElementTree
B314 xml_bad_ElementTree
B315 xml_bad_expatreader
B316 xml_bad_expatbuilder
B317 xml_bad_sax
B318 xml_bad_minidom
B319 xml_bad_pulldom
B320 xml_bad_etree
B321 ftplib
B322 input
B323 unverified_context
B324 hashlib_new_insecure_functions
B325 tempnam
B401 import_telnetlib
B402 import_ftplib
B403 import_pickle
B404 import_subprocess
B405 import_xml_etree
B406 import_xml_sax
B407 import_xml_expat
B408 import_xml_minidom
B409 import_xml_pulldom
B410 import_lxml
B411 import_xmlrpclib
B412 import_httpoxy
B413 import_pycrypto
B501 request_with_no_cert_validation
B502 ssl_with_bad_version
B503 ssl_with_bad_defaults
B504 ssl_with_no_version
B505 weak_cryptographic_key
B506 yaml_load
B507 ssh_no_host_key_verification
B601 paramiko_calls
B602 subprocess_popen_with_shell_equals_true
B603 subprocess_without_shell_equals_true
B604 any_other_function_with_shell_equals_true
B605 start_process_with_a_shell
B606 start_process_with_no_shell
B607 start_process_with_partial_path
B608 hardcoded_sql_expressions
B609 linux_commands_wildcard_injection
B610 django_extra_used
B611 django_rawsql_used
B701 jinja2_autoescape_false
B702 use_of_mako_templates
B703 django_mark_safe

**基线**

它允许使用基线参数(即`**-b BASELINE**` **或** `**--baseline BASELINE**`)指定要比较的基线报告的路径。

**bandit -b 基线**

这有助于忽略您认为不存在问题的已知漏洞(例如，单元测试中的明文密码)。要生成基线报告，只需将输出格式设置为`json`(仅接受 JSON 格式的文件作为基线)并指定输出文件路径即可:

**bandit-f JSON-o PATH _ TO _ OUTPUT _ FILE**

**版本控制集成**

使用[预提交](https://pre-commit.com/)。一旦你[安装了](https://pre-commit.com/#install)，把它添加到。pre-commit-config.yaml(确保更新 rev 以指向一个真正的 git 标签/修订版！):

**回购:
–回购:https://github.com/PyCQA/bandit
rev:“#更新我！钩子:
–id:土匪**

然后运行预提交安装，您就可以开始了。

**配置**

可能会提供一个可选的配置文件，其中可能包括:

*   应该或不应该运行的测试列表
*   exclude _ dirs–如果匹配，将从扫描中排除的路径部分(支持全局模式)
*   被覆盖的插件设置–可能会为某些插件提供不同的设置

**每个项目命令行参数**

项目可能包含一个. bandit 文件，该文件指定应该为该项目提供的命令行参数。当前支持的参数有:

*   targets:逗号分隔的要运行 bandit 的目标目录/文件列表
*   排除:逗号分隔的排除路径列表
*   跳过:要跳过的测试的逗号分隔列表
*   测试:要运行的测试的逗号分隔列表

要使用它，在您的项目目录中放一个. bandit 文件。例如:

排除:/测试

测试:B101，B102，B301

**除外责任**

如果一行代码触发了一个 Bandit 问题，但是该行已经过审查，并且该问题是一个误报或者由于某些其他原因是可接受的，那么该行可以用`# nosec`标记，并且任何与之相关的结果都不会被报告。

例如，尽管该行可能会导致 Bandit 报告潜在的安全问题，但它不会被报告:

**self.process =子流程。Popen('/bin/echo '，shell=True) # nosec**

**漏洞测试**

漏洞测试或“插件”是在插件目录的文件中定义的。

测试是用 Python 编写的，是从插件目录中自动发现的。每个测试可以检查一种或多种类型的 Python 语句。测试用它们检查的 Python 语句的类型来标记(例如:函数调用、字符串、导入等)。

测试由`BanditNodeVisitor`对象在访问 AST 中的每个节点时执行。

测试结果保存在`BanditResultStore`中，并在测试运行完成时汇总输出。

**写作测试**

要编写测试:

*   确定要构建测试的漏洞，并在 examples/中创建一个包含该漏洞的一个或多个案例的新文件。
*   考虑您正在测试的漏洞，用一个或多个适当的装饰符标记该函数:–@ checks(' Call ')–@ checks(' Import '，' Import from ')–@ checks(' Str ')
*   创建一个新的 Python 源文件来包含您的测试，您可以参考现有的测试作为示例。
*   您创建的函数应该带一个参数“context ”,它是 context 类的一个实例，您可以查询有关当前被检查元素的信息。对于更高级的用例，您还可以获得原始的 AST 节点。请查看 context.py 文件了解更多信息。
*   根据需要扩展您的 Bandit 配置文件，以支持您的新测试。
*   对您在 examples/中定义的测试文件执行 Bandit，并确保它检测到漏洞。考虑该漏洞可能出现的各种变化，并相应地扩展示例文件和测试函数。

**延伸土匪**

Bandit 允许用户编写和注册检查和格式化程序的扩展。Bandit 将从两个入口点加载插件:

*   强盗.格式化者
*   bandit .插件

格式化者需要接受 4 件事:

*   result _ store:bandit . core . bandit resultstore 的实例
*   file_list:在作用域中检查的文件列表
*   分数:授予范围内每个文件的分数
*   excluded_files:从范围中排除的文件列表

插件倾向于利用 bandit.checks 装饰器，它允许作者为特定类型的 AST 节点注册一个检查。例如

@ bandit . checks(' Call ')
def prohibit _ unsafe _ deserialization(context):
if ' unsafe _ load in context . Call _ function _ name _ qual:
返回 bandit。问题(
严重性=土匪。
信心高，=土匪。高，
text = "检测到不安全的反序列化。"
)

要注册您的插件，您有两种选择:

1.  如果您直接使用 setuptools，那么在您的`setup`调用中添加如下内容:#如果您在 bandit_bson 模块中有一个假想的 bson 格式化程序#和一个名为` formatter '的函数。entry _ points = { ' bandit . formatters ':[' bson = bandit _ bson:formatter ']} #或检查是否在 bandit_mako 中使用 mako 模板，entry _ points = { ' bandit . plugins ':[' mako = bandit _ mako ']}
2.  如果您使用的是 pbr，请在 setup.cfg 文件中添加如下内容:[entry _ points]bandit . formatters = bson = bandit _ bson:formatter bandit . plugins = mako = bandit _ mako

**特约**

随时欢迎向 Bandit 投稿！

开始使用 Bandit 的最佳方式是获取源代码:

git 克隆 https://github.com/PyCQA/bandit.git

您可以用 tox 测试任何变化:

pip 安装 tox
tox-e pep 8
tox-e py27
tox-e py35
tox-e docs
tox-e 盖

请使用您自己的分支机构而不是主机构提出公关请求:

git check out-b my change
git push origin my change

[**Download**](https://github.com/PyCQA/bandit)