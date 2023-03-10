# Gitls:从 URL /用户/组织列表中枚举 Git 存储库 URL

> 原文：<https://kalilinuxtutorials.com/gitls/>

[![Gitls : Enumerate Git Repository URL From List Of URL / User / Org](img/f49002f695667abf9dbf15b28e20a7c9.png "Gitls : Enumerate Git Repository URL From List Of URL / User / Org")](https://1.bp.blogspot.com/--d0wq275MY0/YE3WyGTcm4I/AAAAAAAAIhc/67AOMzQdes42pn-7gJZzUY0Ca2oxdoTYACLcBGAsYHQ/s728/GITLS%25282%2529.png)

当像 GitHub 这样的库被包含在 bug bounty 范围内时，Gitls 工具就可用了。有时指定为组织名或用户名，而不是特定的存储库，您可以使用此工具从组织/用户中包含的所有公共存储库中提取 url。

这可用于各种操作，如扫描或克隆多个存储库。

> **注意**
> 对于 github api 中未经认证的请求，速率限制允许每小时最多 60 个请求。未经身份验证的请求与原始 IP 地址相关联，而不是发出请求的用户。[https://docs . github . com/en/rest/overview/resources-in-the-rest-api](https://docs.github.com/en/rest/overview/resources-in-the-rest-api)
> 
> 所以太多的任务可以从 github 被 API 阻塞一段时间。在这种情况下，您可以选择适当的目的地或使用 torsocks(如`torsocks gitls -l user.list`或`-tor`选项访问和使用任何 IP。

**安装**

*   **从 go-get**

go 111 module = on go get-v github.com/hahwul/gitls

*   **使用 homebres**

brew tap hahwul/gitls
brew install gitls

*   **使用 snapcraft**

**φsudo snap install gits**

**用途**

```
Usage of gitls:
  -include-users
    	include repo of org users(member)
  -l string
    	List of targets (e.g -l sample.lst)
  -o string
    	write output file (optional)
  -proxy string
    	using custom proxy
  -tor
    	using tor proxy / localhost:9050
  -version
    	version of gitls 
```

**案例研究**

**从 repo/org/user URL 生成所有 repo urls】**

*   **sample.lst**

**https://github.com/hahwul
https://github.com/tomnomnom/gron
https://github.com/tomnomnom/httprobe
https://github.com/s0md3v**

*   **根据样本文件制作回购 url 列表**

◆gits-l sample . lst
https://github . com/hah wul/a2 SV
https://github . com/hah wul/action-dalfox
https://github . com/hah wul/asset-of-hah wul . com
https://github . com/hah wul/awesome-zap extensions
https://github

**获取组织中的所有存储库和包含的用户(成员)**

回声 https://github.com/paypal |。/gitls -include-users

...我...。
https://github . com/paypal/tech-talks
【https://github . com/paypal/TLS-update】
【https://github . com/paypal/yurita】
【https://github . com/ahunrgkar】
【https://github . com/ahunrgkar/docker-chronos-image】

**用[gitleaks](https://github.com/zricethezav/gitleaks)T3 进行自动化测试**

φgits-l sample . lst | xargs-I % gitleaks–repo URL = %-v

**所有克隆目标的回购**

φecho " https://github . com/paypal | gits | xargs-I % git 克隆%

[**Download**](https://github.com/hahwul/gitls)