# git Hound——使用代码搜索关键字在 GitHub 中查找公开的密钥

> 原文：<https://kalilinuxtutorials.com/git-hound-exposed-keys-across-github/>

[![Git Hound – Find Exposed Keys Across GitHub Using Code Search Keywords](img/1dcd8dfb159d7ebef7b5d462b1f3862e.png "Git Hound – Find Exposed Keys Across GitHub Using Code Search Keywords")](https://1.bp.blogspot.com/-U7_9djbF12E/XTV8TUbXjXI/AAAAAAAABew/VkVbJ1tgSBgb8scW48j0kCj4u8wcd01KgCLcBGAs/s1600/Git%2BHound%25281%2529.png)

**Git Hound** 使用模式匹配、目标查询和评分系统，很容易在 GitHub 上找到暴露的 APi 键。

这与其他 OSINT GitHub 扫描器不同，它在 GitHub 中搜索关键字，而不是针对特定的存储库，从而显示出一组完全不同的结果。

GitRob 是一款优秀的工具，专门针对组织或用户拥有的秘密存储库。一个模式匹配，批量捕捉的秘密抢夺者。**这个项目旨在用于教育目的。**

**用途**

`**echo "tillsongalloway.com" | python git-hound.py**`或`**python git-hound.py --subdomain-file subdomains.txt**`我们还提供了许多针对特定模式(已知的服务 API 键)、文件名(。htpasswd，。env)和语言(python、javascript)。

**也读作-[假沙箱:模拟分析沙箱/虚拟机](https://kalilinuxtutorials.com/fake-sandbox-script-fake-processes-vm/)假进程的脚本**

**旗帜**

*   `**--subdomain-file**`–包含子域的文件
*   `**--api-keys**`–启用通用 API 关键字搜索。这使用了常见的 API 键模式和 Shannon 熵来寻找潜在的暴露的 API 键。
*   `**--output**`–输出文件(默认为 stdout)
*   `**--output-type**`–输出类型(需要设置输出标志；默认为平面文件)
*   `**--many-results**`–使用结果排序抓取超过 100 页的结果
*   `**--results-only**`–仅将正则表达式结果打印到标准输出。对于通过管道进入另一个脚本很有用
*   `**--all**`–打印所有 URL，包括没有模式匹配的 URL。否则，计分系统将完成这项工作。
*   `**--regex-file**`–提供自定义正则表达式文件
*   `**--language-file**`–提供带有要搜索语言的自定义文件。
*   `**--config-file**`–自定义配置文件(默认为`config.yml`)
*   `**--pages**`–要搜索的最大页数(默认为 100，最大页数)
*   `**--silent**`–不将结果打印到标准输出(最适合与–output 一起使用)。
*   `**--no-antikeywords**`–不要试图过滤掉已知的大规模扫描
*   `**--only-filtered**`–仅搜索过滤的查询(语言、文件扩展名)
*   `**--debug**`–打印调试信息。有助于调试缓慢的表达式。

**设置**

*   克隆此回购
*   使用 Python 3 环境(推荐:virtulenv 或 [Conda](https://docs.conda.io/en/latest/) )
*   `**pip install -r requirements.txt**` **(或** `**pip3**`)
*   用 GitHub 凭证建立一个`**config.yml**`文件。参见 [config.example.yml](https://github.com/tillson/git-hound/blob/master/config.example.yml) 获取示例。目前不支持 2FA 的账户。
*   `**echo "tillsongalloway.com" | python git-hound.py**`

[**Download**](https://github.com/tillson/git-hound)