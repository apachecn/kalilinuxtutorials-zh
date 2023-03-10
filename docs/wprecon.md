# wprecon:CMS WordPress 中的一个漏洞识别工具

> 原文：<https://kalilinuxtutorials.com/wprecon/>

[![Wprecon : A Vulnerability Recognition Tool In CMS WordPress](img/05e38e2c3cc24e97b134128934626fee.png "Wprecon : A Vulnerability Recognition Tool In CMS WordPress")](https://1.bp.blogspot.com/-f70C0G2q2ww/X_ydmbBJ_kI/AAAAAAAAIUo/gk-z2g28iBcBrS0dTwN8BNQZpsLIIslIgCLcBGAsYHQ/s728/WPrecon%25281%2529.png)

**Wprecon** (WordPress Recon)，是 CMS WordPress 中的漏洞识别工具，100%在 Go 中开发。

**特性**

| 状态 | 特征 |
| --- | --- |
| 981 号房 | 随机代理 |
| 981 号房 | 检测晶片 |
| 981 号房 | 用户枚举器 |
| 981 号房 | 插件扫描仪 |
| 981 号房 | 主题扫描仪 |
| 981 号房 | Tor 代理的 |
| 981 号房 | 检测蜜罐 |
| 981 号房 | 模糊备份文件 |
| 🔨 | 模糊密码 |
| 🔨 | 漏洞扫描器 |

**用途**

| 标签(s): | 描述 |
| --- | --- |
| -u，–URL 字符串 | 目标 URL(例如:http(s)://example.com/)。(必需) |
| –用户-枚举 | 使用提供的模式枚举用户。 |
| –主题-列举 | 使用提供的模式枚举主题。 |
| –插件-枚举 | 使用提供的模式枚举插件。 |
| –检测-晶圆 | 我将尝试检测目标是否在使用 WAF。 |
| –检测-蜜罐 | 我会根据 shodan 来检测目标是否是蜜罐。 |
| –无-检查-wp | 将跳过目标上的 wordpress 检查。 |
| –随机代理 | 使用随机选择的 HTTP(S)用户代理头值。 |
| –tor | 使用 Tor 匿名网络。 |
| –禁用 tls 检查 | 禁用 SSL/TLS 证书验证。 |
| 救命啊 | 为 wprecon 提供帮助。 |
| -v，–详细 | 详细模式。 |

**WPrecon 运行**

命令:`**wprecon --url "https://www.xxxxxxx.com/" --detection-waf**`

*   **输出:**

```
—————————————————————————————————————————————————————————————————————

___       ______________________________________________   __
__ |     / /__  __ \__  __ \__  ____/_  ____/_  __ \__  | / /
__ | /| / /__  /_/ /_  /_/ /_  __/  _  /    _  / / /_   |/ /
__ |/ |/ / _  ____/_  _, _/_  /___  / /___  / /_/ /_  /|  /
____/|__/  /_/     /_/ |_| /_____/  \____/  \____/ /_/ |_/

Github: https://github.com/blackcrw/wprecon
Version: 0.0.1a
—————————————————————————————————————————————————————————————————————
[•] Target: https://www.xxxxxxx.com/
[•] Starting: 09/jan/2020 12:11:17

[•] Listing enable: https://www.xxxxxxx.com/wp-content/plugins/
[•] Listing enable: https://www.xxxxxxx.com/wp-content/themes/
[•••] Status Code: 200 — URL: https://www.xxxxxxx.com/wp-admin/
[•••] I'm not absolutely sure that this target is using wordpress! 37.50% chance. do you wish to continue ? [Y/n]: Y
[•••] Status Code: 200 — WAF: Wordfence Security Detected
[•••] Do you wish to continue ?! [Y/n] : Y
```

[**Download**](https://github.com/blackcrw/wprecon)