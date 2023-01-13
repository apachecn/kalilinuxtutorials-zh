# SCodeScanner:代表源代码扫描器，用户可以扫描源代码以找到关键漏洞

> 原文：<https://kalilinuxtutorials.com/scodescanner/>

[![](img/59ac76c36efba75522435cbc6ed71d09.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhtJCxJETTAw64pgWkdHE7waqRucYKJNzSvXQcNWwxqpywBqTWrQp50CuumEm18vmB8mAUdD3hodnzKcKkfZ0VZuKlMt3QE4LiIBasXo54aQefOBMl_ogM0EjDa5FLuhd4zzRPMe4uhuMj26oygc_yQYI3aZCYw8aQwhSX5dRHcLvO1c1ZgZSLO0IFG/s728/a.png)

**SCodeScanner** 代表源代码扫描器，用户可以在其中扫描源代码以找到关键漏洞。这个扫描器的主要目标是在代码发布到 Prod 之前发现源代码中的漏洞。

## 特性

*   支持的 PHP 语言
*   支持 YAML 语言
*   将结果传递给 bug 跟踪服务，比如吉拉 Slack(一次将文件发送给多人)。
*   以 JSON 格式给出结果，可以很容易地用于任何其他程序。
*   遵守规则。我们只需要创建一些目标规则不在 php/yaml 目录中的规则。
*   可以扫描高级模式的规则

## 成就

SCodeScanner 因在多个 CMS 插件中发现漏洞而收到 5 份 CVE。

*   CVE-2022-1465
*   CVE-2022-1474
*   CVE-2022-1527
*   CVE-2022-1532
*   CVE-2022-1604

## 怎么跑？

*   下载存储库–
*   运行`**pip3 install -r requirements.txt**`
*   并运行`**python3 scscanner.py --help**`

[**Download**](https://github.com/agrawalsmart7/scodescanner)