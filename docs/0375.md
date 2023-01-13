# citadel–web 应用程序安全扫描器

> 原文：<https://kalilinuxtutorials.com/sitadel-security-scanner/>

Sitadel 基本上是对 WAScan 的更新，使其与 python >= 3.4 兼容。它允许您更加灵活地编写新模块和实现新功能:

*   前端框架检测
*   内容传送网络检测
*   定义允许扫描的风险级别
*   插件系统
*   Docker 映像可用于构建和运行

**又读:**[WP Intel——专为 WordPress 漏洞扫描设计的 Chrome 扩展&信息收集](https://kalilinuxtutorials.com/wpintel-chrome-wordpress-scanning/)

#### **Sitadel 安装**

git 克隆 https://github . com/shenril/sitadel . git
CD sitadel
pip 安装。
python sitadel . py-帮助

#### **特性**

*   **指纹**
    *   计算机网络服务器
    *   Web 框架(CakePHP，CherryPy，…)
    *   前端框架(AngularJS、MeteorJS、VueJS 等)
    *   网络应用防火墙(Waf)
    *   内容管理系统
    *   操作系统(Linux，Unix，..)
    *   语言(PHP，Ruby，…)
    *   Cookie 安全性
    *   内容交付网络(CDN)
*   **攻击:**
    *   **布鲁特斯**
        *   管理界面
        *   常见后门
        *   公共备份目录
        *   公共备份文件
        *   公共目录
        *   公共文件
        *   日志文件
    *   **注射**
        *   HTML 注入
        *   SQL 注入
        *   LDAP 注入
        *   XPath 注入
        *   跨站点脚本(XSS)
        *   远程文件包含(RFI)
        *   PHP 代码注入
    *   **其他**
        *   HTTP 允许方法
        *   HTML 对象
        *   多重指数
        *   机器人路径
        *   webdav
        *   跨站点跟踪(XST)
        *   PHPINFO
        *   。列表
    *   **漏洞**
        *   弹震症
        *   匿名密码(CVE-2007-1858)
        *   犯罪(SPDY) (CVE-2012-4929)
        *   支柱-冲击

#### **例子**

简单运行

**蟒蛇 http://website.com**

在危险的风险水平下运行，不要遵循重定向

**python sitadel http://website.com-R2–无重定向**

仅运行特定模块和完整详细信息

**python sitadel http://website.com-一个管理后门-f 头服务器-vvv**

#### **与 Docker 一起运行**

http://example.com 码头公司

[**Download**](https://github.com/shenril/Sitadel)