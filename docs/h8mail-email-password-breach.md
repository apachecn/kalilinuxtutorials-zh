# h8 mail–电子邮件信息和密码漏洞搜索

> 原文：<https://kalilinuxtutorials.com/h8mail-email-password-breach/>

电子邮件攻击和密码漏洞搜索。使用 h8mail 通过不同的攻破和侦察服务，或者臭名昭著的攻破编译 torrent 来查找密码。

#### **h8 邮件功能**

*   电子邮件模式匹配(注册 exp)，对所有这些原始 HTML 文件有用
*   提供小型快速阿尔卑斯码头文件
*   针对目标的 CLI 或批量文件读取
*   输出到 CSV 文件
*   反向 DNS +开放端口
*   云耀斑速率节流避免
    *   执行流保持同步，并根据服务提供商编写的 API 使用指南进行调节
*   对来自[不同违规服务](https://github.com/khast3x/h8mail#apis)提供商的结果进行查询和分组
*   查询“破坏编译”的本地副本
*   获取相关电子邮件
*   美味的颜色

**也可阅读:** [Burp 套件扩展 Turbo 入侵者对 Web 应用程序执行安全测试](https://kalilinuxtutorials.com/burp-extension-turbo-intruder/)

#### **安装**

如果您使用 Docker，请确保在构建之前在配置文件中添加 targets.txt 和 API 键。

在本地

NodeJS 是确保绕过 CloudFlare 所必需的。您可以在这里找到如何为您的发行版安装它

这些指令假设您默认运行 Python3。如果不确定，请查看故障排除部分

**apt-get install nodejs
git 克隆 https://github.com/khast3x/h8mail.git
CD h8 mail
pip install-r requirements . txt
python h8 mail . py-h**

码头工人

**git 克隆 https://github . com/khast 3x/h8 mail . git
CD h8 mail
dock build-t h8 mail。
码头工跑-ti h8 邮件-h**

使用

python h8 mail . py–help
用法:h8 mail . py[-h]-t TARGET _ EMAILS[-c CONFIG _ FILE][-o OUTPUT _ FILE]
[-BC BC _ PATH][-v][-l][-k CLI _ API keys]

电子邮件信息和密码查找工具

可选参数:

**-h，–帮助显示此帮助消息并退出
-t 目标 _ 电子邮件，–目标目标目标 _ 电子邮件
单个电子邮件，或文件(每行一封电子邮件)。
REGEXP
-c CONFIG_FILE，–CONFIG CONFIG _ FILE
API 键的配置文件
-o OUTPUT_FILE，–OUTPUT _ FILE
文件写入 output
-bc BC_PATH，–breakup comp BC _ PATH
breakup 编译 Torrent 的路径。
https://ghostbin.com/paste/2cbdn
-v，–详细显示调试信息
-l，–仅本地运行本地操作
-k CLI_APIKEYS，–API key CLI _ API keys
传递配置选项。格式为“K:V，K:V”**

#### **用法举例**

查询单个目标

**python h8 mail . py-t target@example.com**

查询目标列表，指示 API 键的配置文件，输出到 pwned_targets.csv

**python h8 mail . py-t targets . txt-c config . ini-o pwned _ targets . CSV**

根据漏洞编译的本地副本查询目标列表，从命令行传递 Snusbase 的 API 密钥

**python h8 mail . py-t targets . txt-BC../Downloads/break compilation/-k " snus base _ URL:＄snus base _ URL，snus base _ token:＄snus base _ token "**

无需对违规编译的本地副本进行 API 调用的查询

**python h8 mail . py-t targets . txt-BC../Downloads/break compilation/–local**

#### **故障排除**

Python 版本& Kali

以上说明假设您默认运行 python3。如果不确定，请键入:

**python–版本**

在你的终端里。应该要么是 Python 3。*或 Python 2。*.

如果默认运行 python 2:
确保安装了 python3，然后用显式 python3 调用替换 python 命令:

**apt-get install nodejs
git 克隆 https://github.com/khast3x/h8mail.git
CD h8 mail
pip 3 install-r requirements . txt
python 3 h8 mail . py-h**

[**Download**](https://github.com/khast3x/h8mail)