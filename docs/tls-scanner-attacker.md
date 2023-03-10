# TLS-Scanner:来自 TLS-Attacker 的 TLS-Scanner 模块

> 原文：<https://kalilinuxtutorials.com/tls-scanner-attacker/>

**TLS-Scanner** 是由波鸿鲁尔大学网络和数据安全主席创建的工具，用于帮助 pentesters 和安全研究人员评估 TLS 服务器配置。

**注意:**这是一个为 TLS 开发人员、测试人员、管理员和研究人员设计的研究工具。没有图形用户界面。这是第一个版本，可能包含一些错误。

## **编译 TLS 扫描器**

为了编译和使用它，你需要安装 Java 和 Maven，以及 2.6 版本中的[TLS-attack](https://github.com/RUB-NDS/TLS-Attacker)

```
$ cd TLS-Scanner
$ mvn clean package
```

或者，如果您赶时间，可以使用以下方法跳过测试:

```
$ mvn clean package -DskipTests=true
```

如果您想将它用作库，您需要使用以下命令安装它:

```
$ mvn clean install
```

有关安装所需库的提示，请查看相应的 GitHub 库。

**注意:**要运行此工具，您需要 TLS-attaker 2.6 版

**又读 [元数据-攻击者:一种用恶意元数据生成媒体文件的工具](https://kalilinuxtutorials.com/metadata-attacker/)**

## **运行中**

为了运行它，您需要运行 apps/文件夹中的 jar 文件。

```
$ java -jar apps/TLS-Scanner.jar -connect localhost:4433
```

您可以使用-connect 参数指定要扫描的主机。如果想提高扫描性能，可以使用-threads 参数(默认值=1)。

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/RUB-NDS/TLS-Scanner)