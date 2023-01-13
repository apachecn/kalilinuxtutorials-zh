# 黄金眼–黄金眼第 7 层 DoS 测试工具

> 原文：<https://kalilinuxtutorials.com/goldeneye-dos-test-tool/>

黄金眼是一个 python 应用程序，仅用于安全测试目的。黄金眼是一个 HTTP DoS 测试工具。利用的攻击载体:HTTP Keep Alive + NoCache。

## **黄金用途**

```
 **`USAGE: ./goldeneye.py <url> [OPTIONS]

 OPTIONS:
    Flag           Description                     Default
    -u, --useragents   File with user-agents to use                     (default: randomly generated)
    -w, --workers      Number of concurrent workers                     (default: 50)
    -s, --sockets      Number of concurrent sockets                     (default: 30)
    -m, --method       HTTP Method to use 'get' or 'post'  or 'random'  (default: get)
    -d, --debug        Enable Debug Mode [more verbose output]          (default: False)
    -n, --nosslcheck   Do not verify SSL Certificate                    (default: True)
    -h, --help         Shows this help
```

**也读 [IP-Biter:黑客友好的电子邮件跟踪框架](https://kalilinuxtutorials.com/ip-biter-hacker-e-mail-tracking/)**

## **实用程序**

*   util/getuas . py–从[http://www.useragentstring.com/pages/useragentstring.php](http://www.useragentstring.com/pages/useragentstring.php)子页获取用户代理列表(例如:。/getuas . py【http://www.useragentstring.com/pages/Browserlist/】T2)*要求美声 4*
*   RES/lists/User agents–用户代理字符串的文本列表(每行一个)(来自[http://www.useragentstring.com](http://www.useragentstring.com)

## **变更日志**

*   2016-02-06 增加了不验证 SSL 证书的支持
*   2014-02-20 添加了随机创建的用户代理(仍然符合 RFC)。
*   2014-02-19 移除傻逼推荐人和用户代理。提高了推荐人的随机性。添加了外部用户代理列表支持。
*   2013-03-26 从线程改为多处理。仍然有一些错误需要解决，比如我仍然不知道如何正确地关闭管理器。
*   初始版本

## **免责声明**

该软件仅供教育使用！如果您参与任何非法活动，作者对此不承担任何责任。使用本软件即表示您同意这些条款。

[![https://github.com/jseidl/GoldenEye](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/jseidl/GoldenEye)