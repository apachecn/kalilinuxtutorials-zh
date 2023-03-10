# blackowl——基于操作框架的信息收集工具

> 原文：<https://kalilinuxtutorials.com/blackowl-tool-operative-framework/>

Blackowl 是一个简单的信息收集工具，基于 Operative-Framework。领先的安全来源*工具*，黑客*工具*，网络安全与网络安全。

## **黑枭要求**

*   要求
*   巨蟒
*   beautifulsoup4

**也可理解为[scout 2——AWS 环境的安全审计工具](https://kalilinuxtutorials.com/scout2-security-auditing-aws/)**

## **如何使用** **Blackowl**

```
$ git clone https://github.com/qqwaszx/blackowl.git ; cd blackowl
$ pip install -r requirements.txt
$ python main.py

: blackowl > help
```

[演示](https://www.youtube.com/watch?v=qyTDaS4_qfA&feature=youtu.be)

## **模块/核心/模块/**

*   **CMS 采集:** `CMS Detection`
*   **邮件至域名:** `Get domain with email`
*   **黑客邮件:** `Check if email as been hacked`
*   **IP 地理定位:** `Obtain IP geolocation information`
*   【T1 名称 _k : `Get info on a specific person with his username`
*   **子域搜索:** `Search for subdomain`
*   **全域:**t0]

#### **写模块**

*   **创建新模块:**

```
: blackowl > new_module
: blackowl(New module name ?) > my_module
: blackowl(New module description ?) > This is a module
```

*   **在' def main(self)中编写您的代码:**

```
$ vim core/modules/my_module.py
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/qqwaszx/blackowl)