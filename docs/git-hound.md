# Git-Hound:使用模式匹配精确定位 GitHub 上公开的 API 键

> 原文：<https://kalilinuxtutorials.com/git-hound/>

[![Git-Hound : PinPoints Exposed API Keys On GitHub Using Pattern Matching](img/1ed685e8bb6aa3768e4344a215a6c549.png "Git-Hound : PinPoints Exposed API Keys On GitHub Using Pattern Matching")](https://1.bp.blogspot.com/-JIM_on5jGCo/XpMpYyxTtmI/AAAAAAAAF4Q/seZT5FcNT9MxsS9BIN_phS_nJbNfCZr8ACLcBGAsYHQ/s1600/GetHound.png)

一个批量捕捉，模式匹配，补丁攻击的秘密抢夺者。 **GitHound** 使用模式匹配、提交历史搜索和独特的结果评分系统，精确定位 GitHub 上暴露的 API 密钥。一个批量捕捉，模式匹配，补丁攻击的秘密抢夺者。

**特性**

*   GitHub/Gist 代码搜索。这使得 GitHound 能够定位任何用户上传的暴露在整个 GitHub 中的敏感信息。
*   使用模式匹配、上下文和[香农熵](https://en.wikipedia.org/wiki/Entropy_(information_theory))的通用 API 键检测。
*   提交历史挖掘以查找被不当删除的敏感信息(对于< 6 星的存储库)..
*   评分系统强调有信心的结果，过滤掉常见的误报，并优化密集回购挖掘。
*   Base64 检测和解码
*   将 GitHound 构建到您的工作流中的选项，如自定义正则表达式和仅结果输出模式。

**用途**

**echo " tillsongalloway . com " | git-hound 或 git-hound–subdomain-file subdomains . txt**

**设置**

*   下载最新发布的 GitHound
*   用你的 GitHub 用户名和密码创建一个`**./config.yml**`或`**~/.githound/config.yml**`(不支持 2FA 账号)。参见 [config.example.yml](https://github.com/tillson/git-hound/blob/master/config.example.yml) 。
    1.  如果你是第一次在系统上使用帐户，你可能会收到一封帐户验证邮件。
*   `**echo "tillsongalloway.com" | git-hound**`

**用例**

*   **公司:搜索暴露的客户 API 密钥**

了解特定服务的 API 键的模式使您能够在 GitHub 中搜索这些键。然后，您可以将自定义密钥正则表达式的匹配通过管道传输到您自己的脚本中，以根据服务测试 API 密钥并识别有风险的帐户。

**echo " API . halcorp . biz " | git hound–dig–many-results–regex-file halcorp-API-regexes . txt–results-only | python hala pitester . py**

为了检测未来的 API 密钥泄漏，GitHub 提供了[推送令牌扫描](https://help.github.com/en/articles/about-token-scanning)来立即检测发布的 API 密钥。

*   **Bug 赏金猎人:搜索泄露的员工 API 令牌**

我使用 GitHound 的主要目的是为 Bug 赏金程序寻找敏感信息。对于高调的目标来说，`**--many-results**` hack 和`**--languages**` flag 对于抓取> 100 页的结果很有用。

**echo " Uber internal . com " | git hound–dig–many-results–languages common-languages . txt–threads 100**

**又读-[MSSQLi-DUET:基于 MSSQL 注入的域用户枚举工具](https://kalilinuxtutorials.com/mssql-injection/)**

**标志**

*   `**--subdomain-file**`–包含子域的文件
*   `**--dig-files**`–克隆并搜索回购文件以获得结果
*   `**--dig-commits**`–克隆并搜索回购的提交历史以获得结果
*   `**--many-results**`——使用结果排序和过滤工具抓取超过 100 页的结果
*   `**--results-only**`–仅将正则表达式结果打印到标准输出。对于将自定义正则表达式匹配传送到另一个脚本非常有用
*   `**--no-repos**`–不要搜索仓库
*   `**--no-gists**`–不要搜索 Gists
*   `**--threads**`–指定提交挖掘器使用的最大线程数。
*   `**--regex-file**`–提供自定义正则表达式文件
*   `**--language-file**`–提供带有要搜索语言的自定义文件。
*   `**--config-file**`–自定义配置文件(默认为`**config.yml**`)
*   `**--pages**`–要搜索的最大页数(默认为 100，最大页数)
*   `**--no-scoring**`–不要使用评分来过滤掉误报
*   `**--no-api-keys**`–不执行通用 API 键搜索。GitHound 使用常见的 API 键模式、上下文线索和 Shannon 熵过滤器来查找潜在的公开 API 键。
*   `**--no-files**`–不要标记有趣的文件扩展名
*   `**--only-filtered**`–仅搜索过滤的查询(语言)
*   `**--debug**`–打印详细的调试信息。

**相关工具**

*   GitRob 是一个优秀的工具，它专门针对组织或用户的存储库来公开凭据，并将它们显示在一个漂亮的 web 界面上。

[**Download**](https://github.com/tillson/git-hound)