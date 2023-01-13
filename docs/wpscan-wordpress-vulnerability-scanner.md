# WPScan:为安全专业人士编写的 WordPress 漏洞扫描器

> 原文：<https://kalilinuxtutorials.com/wpscan-wordpress-vulnerability-scanner/>

WPScan 是一个免费的非商业用途的黑盒 WordPress 漏洞扫描器，为安全专家和博客维护者编写，用于测试他们网站的安全性。

**安装**

**先决条件**

*   (可选但强烈推荐:RVM)
*   ruby > = 2.3–推荐:最新
    *   在某些系统中，Ruby 2.5.0 到 2.5.3 会导致“未定义的符号:rmpd_util_str_to_d”错误，参见#1283
*   卷曲> = 7.21–建议:最新
    *   7.29 有一个 segfault
*   ruby gems–推荐:最新

**同时阅读-[4 款最佳写作工具 Linux](https://kalilinuxtutorials.com/best-writing-tools-linux/)**

**来自 RubyGems(推荐)**

**gem 安装 wpscan**

在 MacOSX 上，如果由于苹果的系统完整性保护(SIP)而引发了 **Gem::FilePermissionError** ，要么安装 RVM 并重新安装，要么运行**sudo Gem install-n/usr/local/bin wps can**

**来源(不推荐)**

先决条件:Git

**git 克隆 https://github.com/wpscanteam/wpscan
CD wps can/
捆绑安装&rake 安装**

**更新**

您可以使用`**wpscan --update**`更新本地数据库

更新本身可以通过`**gem update wpscan**`或者软件包管理器来完成(这对于 Kali Linux: `**apt-get update && apt-get upgrade**`这样的发行版来说非常重要)，这取决于它是如何(预)安装的。

**码头工人**

用`**docker pull wpscanteam/wpscan**`拉回购

**枚举用户名**

**docker run-it–RM wps canteam/wps can–URL https://target.tld/–enumerate ua**

**枚举一系列用户名**

**docker run-it–RM wps canteam/wps can–URL https://target.tld/–enumerate u1-100**

**用您选择的范围替换 u1-100。

**用途**

wps can–URL blog . TLD 这将使用默认选项扫描博客，在速度和准确性之间取得良好的平衡。例如，插件将被被动检查，但它们的版本采用混合检测模式(被动+主动)。

还将检查潜在的配置备份文件，以及其他有趣的发现。如果需要更隐秘的方法，那么可以使用**wps can–隐身–URL blog . TLD**。因此，当使用**–枚举**选项时，不要忘记相应地设置**–插件检测**，因为其默认为“被动”。

要获得更多选项，请打开一个终端并键入**wpscan–help**(如果您从源代码构建 wps can，您应该在 git repo 之外键入该命令)

数据库位于~/。wpscan/db

它可以从配置文件加载所有选项(包括–URL)，检查以下位置(顺序:从第一个到最后一个):

*   ~/.wpscan/cli_options.json
*   ~/.wpscan/cli_options.yml
*   pwd/。wpscan/cli_options.json
*   pwd/。wpscan/cli_options.yml

如果这些文件存在，其中的选项将被加载，如果找到两次将被覆盖。

例如:

~/.wpscan/cli_options.yml:

**proxy:' http://127 . 0 . 0 . 1:8080 '
verbose:true**

pwd/。wpscan/cli_options.yml:

**proxy:' socks 5://127 . 0 . 0 . 1:9090 '
URL:' http://target . TLD '**

在当前目录(pwd)下运行 wpscan，与**wps can-v–proxy socks 5://127 . 0 . 0 . 1:9090–URL http://target . TLD**相同

枚举用户名

**wps can–网址 https://target.tld/–枚举 u**

枚举一系列用户名

**wps can–URL https://target.tld/–枚举 u1-100**

**用您选择的范围替换 u1-100。

**公共资源许可证**

该软件(以下简称“WPScan”)是双重许可的，版权归 2011-2019 团队所有。

包含 it 商业化的案例需要一个商业的、非免费的许可证。否则，可以根据以下条款免费使用。

**1。定义**

1.1“许可证”是指本文件。

1.2“贡献者”是指创建、参与创建或拥有它的每个个人或法律实体。

1.3“WPScan 团队”是指 wps can 的核心开发人员。

**2。商业化**

商业用途是指旨在获得商业利益或金钱补偿的用途。

商业化的例子有:

*   使用它来提供商业托管/软件即服务服务。
*   将其作为商业产品或其中的一部分进行销售。
*   将其作为增值服务/产品。

不需要商业许可，因此符合以下条款的示例案例包括(但不限于):

*   渗透测试人员(或渗透测试组织)将它作为评估工具包的一部分。
*   渗透测试 Linux 发行版，包括但不限于 Kali Linux、SamuraiWTF、BackBox Linux。
*   用它来测试你自己的系统。
*   任何非商业用途。

**免费使用条款和条件；**

**3。重新分配**

在以下条件下允许重新分配:

*   它提供了未修改的许可证。
*   它提供了未经修改的版权声明。
*   与商业化条款不冲突。

**4。复制**

只要不与再分发条款冲突，复制是允许的。

**5。修改**

只要不与再分配条款冲突，修改是允许的。

**6。捐款**

任何贡献都假定贡献者授予团队无限的、非排他性的权利来重用、修改和重新许可贡献者的内容。

**7。支持**

它是按原样提供的，没有任何支持、更新或维护。支持、更新和维护可能由团队自行决定。

**8。保修免责声明**

它是根据本许可证按“原样”提供的，没有任何种类的担保，无论是明示的、暗示的还是法定的，包括但不限于无缺陷、适销、适合特定用途或非侵权的担保。

**9。责任限制**

在法律允许的范围内，本软件按“原样”提供。对于因团队的行为、故障、错误和/或与终端设备、计算机、其他软件或任何第三方、终端设备、计算机或服务之间的任何其他交互而导致的任何损害、成本、费用或任何其他付款，团队永远不承担任何责任。

10。免责声明

在你的国家，未经双方同意在网站上运行它可能是非法的。团队不承担任何责任，也不对由此造成的任何误用或损坏负责。

**11。商标**

“wpscan”一词是注册商标。本许可证并未授权使用 it 商标或徽标。

[**Download**](https://github.com/wpscanteam/wpscan)