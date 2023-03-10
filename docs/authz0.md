# Authz0:一个自动化授权测试工具

> 原文：<https://kalilinuxtutorials.com/authz0/>

[![](img/44ed4ed3438ba1aa949435d150ef2c24.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEixdM6kquO1TUTSarr7KtxPZbXag47KFt8U2ulqxooMvLRpWa9804YEefmH9TKxmvUtIJPThA3FHcb3zBZxVogZ00ZPBkkfx6PsXkVMwAU4JDNoziZNcpjgALPswZGiXl1nSX88DWgZGIaYqstB2Kofrd8kGblpn3sD6AdTwhEh3o1lHRuZvRG-AVG4/s728/auth%20logo%20(1).png)

Authz0 是一个自动化的授权测试工具。未授权的访问可以根据 URL 和角色&凭证来识别。

URL 和角色作为基于 YAML 的模板进行管理，可以通过 authz0 自动创建和添加。您还可以使用一次创建/生成的模板文件，基于多个身份验证头和 cookies 进行测试。

## 关键特征

*   生成扫描模板`**$ authz0 new**`
    *   包括 URL
    *   包括角色
    *   包括频道历史记录(选择网址>将所选条目保存为 HAR)
    *   包括打嗝历史记录(选择 URL >保存项目)
    *   包括 HAR 文件
*   轻松修改扫描模板(角色，网址)`**$ authz0**` **`setUrl` `$ authz0 setRole` `authz0 setCred`**
*   使用模板`**$ authz0 scan**`扫描授权(访问控制)

**安装**

*去安装*

**去安装 github.com/hahwul/authz0@latest**

*自制*

**brew tap hahwul/authz 0
brew install authz 0**

## 使用

**可用命令:**

**完成生成指定 shell 的自动完成脚本
帮助关于任何命令的帮助
新建生成新模板
扫描扫描
setCred 追加凭证到模板
setRole 追加角色到模板
setUrl 追加 Url 到模板
版本显示版本**

**生成模板**

**authz0 新[标志]**

例如

**authz 0 new target . YAML–include-URLs URLs . txt
authz 0 new target . YAML–include-zap zap URLs . har
authz 0 new target . YAML–include-burp burpurl . XML**

**修改模板**

**authz 0 set red[flags]
authz 0 set role[flags]
authz 0 set URL[flags]**

例如

**authz 0 setUrl target . YAML setUrl-u https://www.hahwul.com
authz 0 set role target . YAML-n user 1
authz 0 setCred target . YAML-n user 1-H " X-API-Key:1234 "-H " test header:12344 "**

**扫描**

**authz0 扫描[标志]**

例如

**authz 0 scan target . YAML
authz 0 scan target . YAML-r testuser 1-H " Cookie:1234 = 1234 "-H " X-API-Key:1234555 "**

[**Download**](https://github.com/hahwul/authz0)