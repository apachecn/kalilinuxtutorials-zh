# Socid-Extractor:从各种网站的个人页面中提取帐户信息，用于其他目的

> 原文：<https://kalilinuxtutorials.com/socid-extractor/>

[![](img/4e15eece91a2b1a8a18454aa03b70a77.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgFGjypu6n9MUqsNi4CGwdr6VWoRH2WOVHgVKDmnqGltiLefqmFzxjtufdvwTJxeAig6KidCHMrkjAHm0MI-RknbEeN3xqcfmaTjiN4_p4RmI126VH485Qc7gcPeru6E74k-vCEDGSRu1-hpKUVbYNd7s0O0uZFRMdaq2feUB1CulSf7pJMhSMexitE/s728/EuYWv3DXcAI_RcM.png)

**Socid-Extractor** 从个人资料网页/ API 响应中提取有关用户的信息，并将其保存为机器可读格式。

## 使用

作为命令行工具:

**$ socid _ extractor–URL https://www.deviantart.com/muse1908
国家:法兰西
创建 _at: 2005-06-16 18:17:41
性别:女
用户名:Muse1908
网址:www.patreon.com/musemercier
链接:[' https://www . Facebook . com/muse mercier '，' https://www . insta gram . com/muse . mercier/'，' https://www . patre on . com/muse mercier ']** 

不安装:

**$。/run . py–URL https://www.deviantart.com/muse1908**

作为 Python 库:

**导入 socid_extractor，requests
r = requests . get(' https://www . pat reon . com/annetlovart ')
socid _ extract(r . text)
{ ' pat reon _ id ':' 33913189 '，' patreon_username': 'annetlovart '，' fullname': 'Annet Lovart '，' links ':" ' https://www . Facebook . com/322598031832479 '，' https:/**

## 装置

**$ pip3 安装 socid-extractor**

最新的开发版本可以直接从 GitHub 安装:

**pip 3 安装-u git+https://github . com/soxoj/socid _ extractor . git**

## 地点和方法

支持 100 多种不同网站和平台的方法！

*   谷歌(所有文件页面，地图贡献)，需要 cookies
*   Yandex(磁盘、相册、znatoki、音乐、不动产、收藏)，防止验证码阻止所需的 cookies
*   Mail.ru (my.mail.ru 用户主页、照片、视频、游戏、社区)
*   脸书(用户和组页面)
*   VK.com(用户页面)
*   OK.ru(用户页面)
*   照片墙
*   Reddit
*   中等
*   闪烁（光）
*   Tumblr
*   抖音国际版
*   开源代码库

…还有许多其他的。

你也可以检查测试文件中的数据示例，方案文件来解释所有的方法。

## 当它可能有用时

*   通过用户名或/和帐号 UID 获取所有可用信息。示例:在 OSINT 中的星期，OSINTCurious
*   用户跟踪，检查帐户以前是已知的(通过 ID)，即使所有的公共信息已经改变。示例:在线感知
*   通过常用的跨服务 UID(盖亚 ID、脸书 UID、Yandex 公共 ID 等)进行搜索。)
    *   SQL 格式的论坛和平台的 DB 泄漏
    *   包含目标配置文件 ID 的索引链接
*   通过与其他 id 进行比较来搜索跟踪数据-它如何工作，如何使用。
*   执法在线请求

## 测试

**python 3-m pytest tests/test _ e2e . py-n 10-k ' not cookies '-m ' not github _ failed and not rate _ limited '**

[Download](https://github.com/soxoj/socid-extractor)