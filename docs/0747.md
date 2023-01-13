# Machinae : Machinae 安全情报收集器

> 原文：<https://kalilinuxtutorials.com/machinae-security-intelligence-collector/>

[![Machinae : Machinae Security Intelligence Collector](img/8ddad6d1ec4c5e40159a58866f51227e.png "Machinae : Machinae Security Intelligence Collector")](https://1.bp.blogspot.com/-gp9sZm-60O0/XTBkA7bl-0I/AAAAAAAABbU/LOyDW68wivs-2BfxkcFqGN9m9Y8wCGvCACLcBGAs/s1600/machinae.png)

Machinae 是一款从公共网站/订阅源收集各种安全相关数据的工具:IP 地址、域名、URL、电子邮件地址、文件哈希和 SSL 指纹。

它的灵感来自于另一个收集信息的优秀工具 [Automater](https://github.com/1aN0rmus/TekDefense-Automater) 。Machinae 项目诞生于希望在 4 个方面改进 Automater:

*   代码库——使 Automater 与 python3 兼容，同时使代码更加 python 化
*   配置–使用更易于阅读的配置格式(YAML)
*   输入——支持 JSON 解析，无需编写正则表达式，但在需要时仍支持正则表达式抓取
*   输出——支持额外的输出类型，包括 JSON，同时使无关的输出成为可选的

**安装**

Machinae 可以使用 pip3 安装:

**pip3 安装机器**

或者，如果你喜欢冒险，可以直接从 github 安装:

**pip3 安装 git+https://github . com/HurricaneLabs/machinae . git**

您需要在您的系统上拥有编译 Python 模块所需的任何依赖项(在基于 Debian 的系统上，`**python3-dev**`)，以及 libyaml 开发包(在基于 Debian 的系统上，`**libyaml-dev**`)。

您还需要获取[最新的配置文件](https://github.com/HurricaneLabs/machinae/raw/master/machinae.yml)，并将其放在`**/etc/machinae.yml**`中。

**也读作-[Passpie:多平台命令行密码管理器](https://kalilinuxtutorials.com/passpie-command-line-password-manager/)**

**配置文件**

Machinae 支持简单的配置合并系统，允许您在不修改我们提供给您的 machinae.yml 的情况下对配置进行调整，使配置更新变得轻而易举。

这是通过找到一个系统范围的缺省配置(缺省值`**/etc/machinae.yml**`)，合并成一个系统范围的本地配置(`**/etc/machinae.local.yml**`)和最后一个每个用户的本地配置(`**~/.machinae.yml**`)来完成的。

系统级配置也可以位于当前工作目录中，可以使用`**MACHINAE_CONFIG**`环境变量进行设置，当然也可以使用`**-c**`或`**--config**`命令行选项。

通过传递`**--nomerge**`选项可以禁用配置合并，这将导致 Machinae 只加载默认的系统级配置(或者在命令行上传递的配置)。

举个例子，假设你想启用 Fortinet 类别网站，默认情况下是禁用的。您可以修改`**/etc/machinae.yml**`，但是这些更改会被更新覆盖。相反，您可以将以下内容放在`**/etc/machinae.local.yml**`或`**~/.machinae.yml**`中:

**fortinet_classify:
默认值:true**

或者反过来，禁用一个站点，如病毒总 pDNS:

vt_ip:
默认值:false
vt_domain:
默认值:false

**用法**

Machinae 的用法与 Automater 非常相似:

用法:machinae[-H][-c CONFIG][–no merge][-D DELAY][-f FILE][-I INFILE][-v]
[-O { D，J，N，S}] [-O {ipv4，ipv6，fqdn，email，sslfp，hash，URL }][-q][-T1][-S SITES][-a AUTH][-H HTTP _ PROXY]
[–dump-CONFIG |–detect-otype]
…

*   关于`**-c**` **/** `**--config**`和`**--nomerge**`选项的详细信息见上。
*   Machinae 支持一个`**-d**` **/** `**--delay**`选项，像 Automater。但是，Machinae 默认使用 0。
*   Machinae 输出由两个参数控制:
    *   `-o`控制输出格式，可以后跟单个字符来表示所需的输出类型:
        *   *N* 是默认输出(“正常”)
        *   *D* 是默认输出，但是点字符被替换
        *   *J* 是 JSON 输出
    *   `**-f**` **/** `**--file**`指定输出应该写入的文件。对于标准输出，默认值为“-”。
*   Machinae 将尝试自动检测传入的目标类型(Machinae 将目标称为“observables”，将类型称为“otype”)。该检测可以用`**-O**` **/** `**--otype**`选项覆盖。用法中列出了这些选项
*   默认情况下，Machinae 以详细模式运行。在这种模式下，它会在控制台上查询服务时输出有关这些服务的状态信息。无论输出设置如何，该输出将始终被写入 stdout。要禁用详细模式，请使用`-q`
*   默认情况下，Machinae 将运行配置中适用于每个目标的 otype *和*的所有服务，不标记为“default: false”。要修改此行为，您可以:
    *   传递要运行的站点的逗号分隔列表(使用配置中的顶级密钥)。
    *   传递特殊关键字`all`来运行所有服务*，包括那些标记为“default: false”的*。注意，在这两种情况下，`otype`验证仍然适用。
*   Machinae 支持在命令行上使用`**-H**` **/** `**--http-proxy**`参数传递 HTTP 代理。如果没有指定代理，machinae 将搜索标准的`**HTTP_PROXY**`和`HTTPS_PROXY`环境变量，以及不太标准的`http_proxy`和`https_proxy`环境变量。
*   最后，应该通过一个目标列表。除上面列出的选项之外的所有参数都将被解释为目标。

**现成的数据来源**

Machinae 提供了对以下数据源的现成支持:

*   lpvoid
*   URLVoid
*   网址缩写([http://www.toolsvoid.com/unshorten-url](http://www.toolsvoid.com/unshorten-url))
*   Malc0de
*   无
*   FreeGeoIP (freegeoip.io)
*   Fortinet 类别
*   VirusTotal pDNS(通过 web scrape–注释掉)
*   VirusTotal pDNS(通过 JSON API)
*   VirusTotal URL 报告(通过 JSON API)
*   病毒总文件报告(通过 JSON API)
*   信誉权威
*   威胁专家
*   VxVault
*   项目蜜罐
*   迈克菲威胁情报
*   StopForumSpam
*   Cymru MHR
*   ICSI 证书公证人
*   TotalHash(默认禁用)
*   域名工具解析 Whois(需要 API 密钥)
*   域名工具反转 Whois(需要 API 密钥)
*   域名工具声誉
*   IP WHOIS(使用 RIR REST 接口)
*   被黑的 IP
*   Metadefender 云(需要 API 密钥)
*   灰色噪音(需要 API 键)
*   IBM XForce(必需的 API 密钥)

还会有更多的数据源。

**HTTP 基本认证和配置**

Machinae 通过`--auth/-a`标志为需要 HTTP 基本认证的站点提供支持。您将需要使用您的凭据创建一个 YAML 文件，该文件将包含一个指向需要凭据的站点的密钥，以及一个包含两项内容的列表，即用户名和密码或 API 密钥。例如，对于包含的 PassiveTotal 站点，可能是这样的:

**passive total:[' my email @ example . com '，' my_api_key']**

在`request`下的站点配置中，您会看到一个键，例如:

json:
请求:
URL:'…'
auth:passive total

`**auth: passivetotal**`指向通过命令行传递的认证配置中的密钥。

**默认禁用**

默认情况下，以下站点是禁用的

*   Fortinet 类别(`**fortinet_classify**`)
*   Telize 地理 IP ( `**telize**`)
*   总散列(`**totalhash_ip**`
*   域名工具解析 Whois ( `**domaintools_parsed_whois**`)
*   域工具反转 whois(“t0”)
*   域名工具声誉(`**domaintools_reputation**`)
*   被动被动域名系统(`**passivetotal_pdns**`)
*   被动共计(T0)
*   PassiveTotal SSL 证书历史(`**passivetotal_sslcert**`)
*   被动主机属性组件(`**passivetotal_components**`)
*   被动主机属性跟踪器(`**passivetotal_trackers**`)
*   MaxMind GeoIP2 被动洞察(`**maxmind**`)
*   欺诈卫士(`**fraudguard**`)
*   庄丹(`**shodan**`)
*   被黑的 IP
*   Metadefender 云(需要 API 密钥)
*   灰色噪音(需要 API 键)
*   IBM XForce(需要 API 密钥)

**输出格式**

Machinae 附带了一组有限的输出格式:normal、带点转义的 normal 和 JSON。我们计划在未来增加额外的输出格式。

**已知问题**

*   IPvoid 上的一些 ISP 包含双重编码的 HTML 实体，而不是双重解码的

**即将推出的功能**

*   添加 IDS 规则搜索功能(VRT/美国)
*   为网站添加“更多信息”链接
*   在解析器设置中添加“重复数据删除”选项
*   为每种类型的请求设置添加选项
*   为错误代码添加自定义的每个站点的输出

[**Download**](https://github.com/HurricaneLabs/machinae)