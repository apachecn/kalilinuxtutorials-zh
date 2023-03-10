# Versionscan:一个 PHP 版本扫描器，用于报告可能的漏洞

> 原文：<https://kalilinuxtutorials.com/versionscan/>

[![Versionscan : A PHP Version Scanner For Reporting Possible Vulnerabilities](img/b0919a289cf365ffdd99e32cbe5731b9.png "Versionscan : A PHP Version Scanner For Reporting Possible Vulnerabilities")](https://1.bp.blogspot.com/-KLcA-sdlTxI/XOXEl5-2T8I/AAAAAAAAAbo/nImuzY4iGrov6fMSDC3mNDOrRbnfzKVVACLcBGAs/s1600/Versionscan.png)

版本扫描是一个工具，用于评估你当前安装的 PHP 版本，并对照已知的 CVEs 和它们被修复的版本进行检查，以报告潜在的问题。

**注意:**使该工具适应支持安全修复的 Linux 发行版的工作仍在进行中。到目前为止，这仅仅是针对所报告的直截了当的版本。

**安装**

**使用作曲**

**{
"要求":{
" PSE CIO/version scan ":" dev-master "
}
}**

目前唯一的依赖是 Symfony 控制台。

**也可以理解为-[Security RAT:开发中处理安全需求的工具](https://kalilinuxtutorials.com/security-rat/)**

**用法**

要对您当前的 PHP 版本运行扫描，请使用:

**bin/版本扫描**

该脚本将检查当前实例的`PHP_VERSION`,并生成通过/失败结果。输出类似于:

```
Executing against version: 5.4.24
+--------+---------------+------+------------------------------------------------------------------------------------------------------+
| Status | CVE ID        | Risk | Summary                                                                                              |
+--------+---------------+------+------------------------------------------------------------------------------------------------------+
| FAIL   | CVE-2014-3597 | 6.8  | Multiple buffer overflows in the php_parserr function in ext/standard/dns.c in PHP before 5.4.32 ... |
| FAIL   | CVE-2014-3587 | 4.3  | Integer overflow in the cdf_read_property_info function in cdf.c in file through 5.19, as used in... |
```

结果也将以彩色显示，以便于显示检查的通过/失败。

**参数**

可以为该工具提供几个参数来配置其扫描和结果:

**PHP 版本**

如果您想定义一个 PHP 版本来检查，而不是脚本自己找到的版本，您可以使用`php-version`参数:

**bin/versions 扫描–PHP-version = 4 . 3 . 2**

**只报告故障**

您还可以告诉 it 只报告失败，而不报告通过的测试:

**纸盒/版本扫描–仅失败扫描**

**排序结果**

您还可以使用`sort`参数和“CVE”或“risk”值，按照 CVE ID 或严重性(风险评级)对结果进行排序:

**bin/versions 扫描–sort = risk**

**输出格式**

默认情况下，*版本扫描*会以人类可读的结果将信息直接输出到控制台。您还可以指定其他更易于编程解析的输出格式(比如 JSON)。使用`--format`选项改变输出:

**供应商/bin/版本扫描–PHP-version = 5.5–format = JSON**

支持的输出格式有`console`、`json`、`xml`和`html`。

HTML 输出格式需要目录的一个`--output`选项来写入文件:

**vendor/bin/versions scan–PHP-version = 5.5–format = html–output =/var/www/output**

结果将被写入一个名为`**versionscan-output-20150808.html**`的文件

[**Download**](https://github.com/psecio/versionscan)