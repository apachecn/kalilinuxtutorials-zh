# Firebase——利用错误配置的 Firebase 数据库的工具

> 原文：<https://kalilinuxtutorials.com/firebase-misconfigured-databases/>

Firebase 利用工具正在利用错误配置的 firebase 数据库。

**免责声明:**所提供的软件仅用于教育目的。请自行使用，创作者不对造成的任何损害负责。请负责任地使用！

## **先决条件**

非标准 python 模块:

*   dnsdumposter
*   bs4
*   要求

**同时阅读[Android 应用开发者指南:将一个 iOS 应用转换成 Android](https://kalilinuxtutorials.com/android-application-developer/)**

## **火焰基座安装**

如果以下命令成功运行，您就可以使用该脚本了:

```
git clone https://github.com/Turr0n/firebase.git
cd firebase
pip install -r requirements.txt
```

## **用途**

```
python3 firebase.py [-h] [--dnsdumpster] [-d /path/to/file.htm] [-o results.json] [-l /path/to/file] [-c 100] [-p 4]
```

参数:

```
 **-h      Show the help message
    -d      Absolute path to the downloaded HTML file.
    -o      Output file name. Default: results.json
    -c      Crawl for domains in the top-1m by Alexa. Set how many domains to crawl, for example: 100\. Up to 1000000
    -p      How many processes to execute. Default: 1
    -l      Path to a file containing the DBs to crawl. One DB name per line. This option can't be used with -d or -c
    --dnsdumpster       Use the DNSDumpster API to gather DBs
    --just-v    Ignore "non-vulnerable" DBs
    --amass Path of the output file of an amass scan ([-o] argument)
```

示例:`**python3 firebase.py -p 4 -f results_1.json -c 150 --dnsdumpster**`这将查找 Alexa 文件中的前 150 个域以及 DNSDumpster 提供的数据库。结果将被保存到`**results_1.json**`，整个脚本将使用 4 个并行进程执行

该脚本将创建一个 json 文件，其中包含收集的易受攻击的数据库及其转储的内容。每个数据库都有一个状态:

*   -2:数据库不存在
*   -1:表示它不容易受到攻击
*   0:进一步的解释是可能的
*   1:易受攻击

为了获得更好的结果，前往 pentest-tools.com，并在其子域扫描器介绍以下领域:`firebaseio.com`。一旦扫描完成，保存页面 HTML(CRL+S)并使用`-d [path]`参数，这将允许脚本分析该服务发现的子域。更多的子域爬虫可能得到支持。

现在我们支持@caffix 的 amass 扫描仪！通过使用该工具对使用`-o`参数的`**firebaseio.com**`运行任何所需的 scann，脚本将能够对输出文件进行摘要，并对发现的 db 进行爬行。

Firebase DBs 使用这种结构工作:`**https://[DB name].firebaseio.com/**`。如果使用`-l [path]`参数，提供的文件需要每行包含一个【数据库名称】，例如:

```
airbnb
twitter
microsoft
```

使用该文件将检查这些数据库:`**https://airbnb.firebaseio.com/.json, https://twitter.firebaseio.com/.json, https://microsoft.firebaseio.com/.json**`

[![https://github.com/Nekmo/dirhunt](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/Turr0n/firebase)