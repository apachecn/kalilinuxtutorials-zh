# Ox4Shell:轻松去除 Log4Shell 负载

> 原文：<https://kalilinuxtutorials.com/ox4shell/>

[![](img/d3d9d0e52565496058cb5abf1f9559b7.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgbl_Mlr5sPCTx1ira3aaUdzu0DxnFHt1WKZgQ4Bx7vZpUfzdHwtOfDaRI3gsrcTULkwFFkLFDdvTsdkzpVWZDeHlMRwPivk1m_57JwIB9l4gp_6CIII_VHdNtupuVPQBFDmMwchvw90th4XJbwYQwqXEjoYZh5rnkJa9nXozLeb4_B5qH1RLVRQgbc/s728/Ox4Shell.png)

Ox4Shell 是一个轻松去除 Log4Shell 负载的工具。

## 描述

自从 Log4Shell 漏洞(CVE-2021-44228)发布以来，许多工具被创建来混淆 Log4Shell 有效负载，使安全工程师的生活成为一场噩梦。

该工具旨在揭示混淆的 Log4Shell 负载的真实内容。

我们建议使用提供的文件(`-f`)而不是内联有效负载(`-p`)运行`Ox4Shell`，因为某些 shell 环境会对重要字符进行转义，因此会产生不准确的结果。

## 用法

要运行该工具，只需:

```
~/Ox4Shell » python ox4shell.py --help
usage: ox4shell [-h] [-d] [-m MOCK] [--max-depth MAX_DEPTH] [--decode-base64] (-p PAYLOAD | -f FILE)

   ____       _  _   _____ _          _ _ 
  / __ \     | || | / ____| |        | | |
 | |  | |_  _| || || (___ | |__   ___| | |
 | |  | \ \/ /__   _\___ \| '_ \ / _ \ | |
 | |__| |>  <   | | ____) | | | |  __/ | |
  \____//_/\_\  |_||_____/|_| |_|\___|_|_|

Ox4Shell - Deobfuscate Log4Shell payloads with ease.
    Created by https://oxeye.io

General:
  -h, --help            Show this help message and exit
  -d, --debug           Enable debug mode (default: False)
  -m MOCK, --mock MOCK  The location of the mock data JSON file that replaces certain values in the payload (default: mock.json)
  --max-depth MAX_DEPTH
                        The maximum number of iteration to perform on a given payload (default: 150)
  --decode-base64       Payloads containing base64 will be decoded (default: False)

Targets:
  Choose which target payloads to run Ox4Shell on

  -p PAYLOAD, --payload PAYLOAD
                        A single payload to deobfuscate, make sure to escape '$' signs (default: None)
  -f FILE, --file FILE  A file containing payloads delimited by newline (default: None)

```

## 模拟数据

Log4j 库有几个独特的查找函数，允许用户查找环境变量、Java 进程的运行时信息等等。此功能使威胁参与者能够探测特定信息，这些信息可以唯一识别他们所针对的受损机器。

Ox4Shell 使用`mock.json`文件将公共值插入到某个查找函数中，例如，如果有效载荷包含值`${env:HOME}`，我们可以用自定义的模拟值替换它。

提供的默认模拟数据集是:

```
{
    "hostname": "ip-127.0.0.1",
    "env": {
        "aws_profile": "staging",
        "user": "ubuntu",
        "pwd": "/opt/",
        "path": "/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/lib/jvm/java-1.8-openjdk/jre/bin:/usr/lib/jvm/java-1.8-openjdk/bin"
    },
    "sys": {
        "java.version": "16.0.2",
        "user.name": "ubuntu"
    },
    "java": {
        "version": "Java version 16.0.2",
        "runtime": "OpenJDK Runtime Environment (build 1.8.0_181-b13) from Oracle Corporation",
        "vm": "OpenJDK 64-Bit Server VM (build 25.181-b13, mixed mode)",
        "os": "Linux 5.10.47-linuxkit unknown, architecture: amd64-64",
        "locale": "default locale: en_US, platform encoding: UTF-8",
        "hw": "processors: 1, architecture: amd64-64"
    }
}

```

[Click Here To Download](https://github.com/ox-eye/Ox4Shell)