# CRS–OWASP ModSecurity 核心规则集

> 原文：<https://kalilinuxtutorials.com/crs-owasp-modsecurity/>

OWASP ModSecurity 核心规则集或 CRS 是一组通用攻击检测规则，用于 ModSecurity 或兼容的 web 应用程序防火墙。

它旨在保护 web 应用程序免受各种攻击，包括 OWASP 十大攻击，并将错误警报降至最低。

**也读作 [XSS Fuzzer:根据用户定义的向量生成 XSS 有效载荷的工具& Fuzzing 列表](https://kalilinuxtutorials.com/xssfuzzer-xss-payloads/)**

它针对许多常见的攻击类别提供保护，包括:

| **SQL 注入(SQLi)**
**跨站点脚本(XSS)**
**本地文件包含(LFI)**
**远程文件包含(RFI)**
**PHP 代码注入**
**Java 代码注入CRS 3.1 中新增！** | **HTTPoxy**
**Shellshock**
**Unix/Windows Shell 注入**
**会话固定**
**脚本/扫描器/Bot 检测**
**元数据/错误泄漏** |

## **CRS 安装**

它需要安装 ModSecurity 2.8.0 或更高版本的 Apache/IIS/Nginx web 服务器。

`**git clone [https://github.com/SpiderLabs/owasp-modsecurity-crs.git](https://github.com/SpiderLabs/owasp-modsecurity-crs.git)**`

下载后，将 crs-setup.conf.example 复制到 crs-setup.conf 中。可以选择编辑此文件来配置您的 crs 设置。然后将这些文件包含在您的 web 服务器配置中:

```
Include /.../crs-setup.conf
Include /.../rules/*.conf
```

详细的安装说明见[安装](https://raw.githubusercontent.com/SpiderLabs/owasp-modsecurity-crs/v3.0/master/INSTALL)文件。还要查看[变更](https://raw.githubusercontent.com/SpiderLabs/owasp-modsecurity-crs/v3.0/master/CHANGES)和[已知 _ bug](https://raw.githubusercontent.com/SpiderLabs/owasp-modsecurity-crs/v3.0/master/KNOWN_BUGS)文档。
您可以使用包含的脚本`**util/upgrade.py**`更新规则集。

## **处理误报和高级功能**

高级功能在 **`crs-setup.conf`** 和规则文件本身中有说明。`**crs-setup.conf**`文件通常是探索 CRS 特性的一个很好的切入点。我们正在努力减少默认安装中的误报(错误警报)数量。但是迟早，你还是会遇到假阳性。

OWASP ModSecurity 核心规则集是根据 Apache 软件许可证(ASL)版本 2 发布的。请参阅随附的许可证文件了解全部详情。

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/SpiderLabs/owasp-modsecurity-crs)

**鸣谢:Chaim Sanders，Walter Hop&Christian Folini**

***你可以在 [Linkedin](https://www.linkedin.com/company/gbhackers/) 、 [Twitter](https://twitter.com/GbhackerOn) 、[脸书](https://www.facebook.com/gbhackersadmin)上关注我们的日常网络安全更新，你也可以在线参加[最佳网络安全课程](https://ethicalhackersacademy.com/)以保持自我更新。***