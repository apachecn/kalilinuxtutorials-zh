# Rekono:结合多种黑客工具自动执行完整的测试过程

> 原文：<https://kalilinuxtutorials.com/rekono/>

[![](img/1927d08852428a5df2917971ba5520a0.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhGsh3kVg3RvJXOauQtvUGlFUdKA4yefe26FB67TPbyCiBYUVY3MXNgBfZmx3aOXIJPf98DEkMp5spBNd7ChAsHr1_M2zn8d8KiRZLedNWOWiYgK3jqDyL83M6Ym6B53Bzwh9qOY_Imoz7ThSPV28HqU8yEnCg3L93SpmX8fdfAoPazhMfnjxZSENjv/s728/logo-black%20(2).png)

Rekono 结合其他黑客工具及其结果，以自动化的方式对目标执行完整的测试过程。执行过程中获得的结果将通过电子邮件或电报通知发送给用户，如果需要高级漏洞管理，也可以导入到 Defect-Dojo 中。此外，Rekono 包括一个电报机器人，可用于在任何地方使用任何设备轻松执行死刑。

## 特性

*   结合黑客工具创建 pentesting `**processes**`
*   执行测试`**processes**`
*   执行测试`**tools**`
*   查看`**findings**`并通过`**email**`或`**Telegram**`通知接收它们
*   使用`**Defect-Dojo**` integration 导入 Rekono 检测到的结果
*   从`**Telegram Bot**`执行 **`tools`** 和`**processes**`
*   `**Wordlists**`管理

## Why Rekono?

你有没有想过当你开始一项测试时，你要遵循的步骤？也许你开始执行一些新的任务来收集关于目标的公共信息。然后，您可能会运行主机发现和端口枚举工具。当您知道目标暴露了什么时，您可以为每个服务执行更具体的工具，以获得更多信息，也许还有一些漏洞。最后，如果你找到了需要的信息，你会寻找一个公开的漏洞让你进入目标机器。我知道，我知道，这是一个乌托邦式的场景，在大多数情况下，漏洞是由于 pentester 技能而不是扫描工具发现的。但是在使用你的技能之前，你花了多少时间试图用黑客工具获取尽可能多的信息呢？可能，太多了。

为什么不将这个过程自动化，并利用您的技能和 Rekono 发送给您的信息专注于寻找漏洞呢？

### 支持的工具

*   theHarvester
*   EmailHarvester
*   EmailFinder
*   Nmap
*   Sslscan
*   分析
*   SSH 审计
*   SMBMap
*   目录搜索
*   GitLeaks & GitDumper
*   Log4j 扫描仪
*   amseek
*   OWASP JoomScan
*   OWASP ZAP
*   Nikto
*   SearchSploit
*   Metasploit

感谢这些神奇工具的所有贡献者！

## 安装

### 码头工人

在项目的根目录中执行以下命令:

**对接器-复合式建置
对接器-复合式 up -d**

如果需要同时运行多个工具，可以设置执行工作实例的数量:

**docker-compose up-d-scale executions-worker = 5**

### 使用 Rekono CLI

如果您的系统是 Linux，您可以使用 rekono-cli 在您的系统中安装 rekono

**pip3 install rekono-cli
rekono install**

## 配置

您可以使用两种主要方法配置 Rekono:`**config.yaml**`文件和环境变量。将按以下优先级获取属性:

1.  来自环境变量
2.  来自配置文件。您可以使用`**config.yaml**`作为模板
3.  缺省值

Rekono 支持以下属性:

| 环境变量 | 配置属性 | 缺省值 | 描述 |
| --- | --- | --- | --- |
| `**REKONO_HOME**` | 不适用的 | 或者源代码所在的位置 | 通往雷科诺家的路 |
| **T2`RKN_FRONTEND_URL`** | `**frontend.url**` | `**http://127.0.0.1:3000**` | 用于在通知中包含指向 Rekono 前端的链接的 URL |
| `**RKN_DB**_NAME` | `**database.name**` | `**rekono**` | 数据库名称 |
| **T2`RKN_DB_USER`** | `**database.user**` | 不适用的 | 数据库用户 |
| **T2`RKN_DB_PASSWORD`** | `**database.password**` | 不适用的 | 数据库密码 |
| `**RKN_DB_HOST**` | `**database.host**` | `**127.0.0.1**` | 数据库主机 |
| `**RKN_DB_PORT**` | `**database.port**` | `**5432**` | 数据库端口 |
| `**RKN_RQ_HOST**` | `**rq.host**` | `**127.0.0.1**` | 重定向主机队列 |
| `**RKN_RQ_PORT**` | `**rq.port**` | `**6379**` | 重定向队列端口 |
| `**RKN_EMAIL_HOST**` | `**email.host**` | `**127.0.0.1**` | SMTP 主机 |
| `**RKN_EMAIL_PORT**` | `**email.port**` | `**587**` | SMTP 端口 |
| `**RKN_EMAIL_USER**` | `**email.user**` | 不适用的 | SMTP user |
| `**RKN_EMAIL_PASSWORD**` | `**email.password**` | 不适用的 | SMTP 密码 |
| `**RKN_TELEGRAM_BOT**` | `t**elegram.bot**` | `**Rekono**` | 要包含在前端的电报机器人名称 |
| `**RKN_TELEGRAM_TOKEN**` | `**telegram.token**` | 不适用的 | 电报机器人令牌。怎么弄一个？ |
| `**RKN_DD_URL**` | `**defect-dojo.url**` | `**http://127.0.0.1:8080**` | 缺陷-Dojo URL |
| `**RKN_DD_API_KEY**` | `**defect-dojo.api-key**` | 不适用的 | 缺陷-Dojo API 键 |
| 不适用的 | `**defect-dojo.verify**` | `**True**` | 指明是否应验证缺陷-Dojo 证书 |
| 不适用的 | `**defect-dojo.tags**` | [ `**rekono**` ] | Rekono 在 Defect-Dojo 中创建的项目中包含的标签 |
| 不适用的 | `**defect-dojo.product-type**` | `**Rekono Project**` | 产品类型 naem 与 Rekono 在 Defect-Dojo 中创建的产品相关 |
| 不适用的 | `**defect-dojo.test-type**` | `**Rekono Findings Import**` | 与 Rekono 在 Defect-Dojo 中创建的测试相关的测试类型名 |
| 不适用的 | `**defect-dojo.test**` | `**Rekono Test**` | 与 Rekono 在 Defect-Dojo 中导入的发现相关的测试名称 |
| `**RKN_OTP_EXPIRATION_HOURS**` | `**security.otp-expiration-hour**s` | `**24**` | Rekono 创建的一次性密码的过期时间(小时) |
| `**RKN_UPLOAD_FILES_MAX_MB**` | `**security.upload-files-max-mb**` | `**500**` | 上传到 Rekono 的文件的 MB 限制。例如，单词列表文件 |
| `R**KN_TRUSTED_PROXY**` | 不适用的 | `**False**` | 指示 Rekono 是否使用受信任的反向代理运行 |
| `**RKN_ALLOWED_HOSTS**` | `**security.allowed-hosts**` | 【 **`localhost`，`127.0.0.1`，`::1`，**】 | 允许访问 Rekono 的主机 |
| `RKN_SECRET_KEY` | `security.secret-key` | 随机生成 | 用于签署 JWT 令牌的安全密钥 |

要根据前面的属性配置 Rekono 前端，您可以运行以下命令:

该命令会将该属性添加到`**rekono/frontend/.env**`文件中:

*   `**VUE_APP_DEFECTDOJO**`:在前端启用或禁用 Defect-Dojo 集成特性
*   `**VUE_APP_DEFECTDOJO_URL**`:缺陷-道场 URL
*   `**VUE_APP_TELEGRAM_BOT**`:要在 UI 中显示的电报机器人名称

当然，你也可以直接在`**rekono/frontend/.env**`文件中配置这个属性

[**Download**](https://github.com/pablosnt/rekono)