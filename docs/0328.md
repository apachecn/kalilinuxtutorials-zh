# ache——用于特定领域搜索的网络爬虫

> 原文：<https://kalilinuxtutorials.com/ache-web-crawler-domain/>

ACHE 是一个专注的网络爬虫。它收集满足某些特定标准的网页，例如，属于给定域或包含用户指定模式的网页。

ACHE 不同于一般的爬虫，它使用*页面分类器*来区分给定域中的相关和不相关页面。

页面分类器可以从简单的正则表达式(例如，匹配包含特定单词的每个页面)到基于机器学习的分类模型。

ACHE 还可以自动学习如何区分链接的优先级，以便高效地定位相关内容，同时避免检索不相关的内容。

ACHE 支持许多功能，例如:

*   定期抓取固定的网站列表
*   通过自动链接优先化发现和爬行新的相关网站
*   配置不同类型的页面分类器(机器学习、正则表达式等)
*   不断重新抓取网站地图以发现新页面
*   使用 Elasticsearch 索引抓取的页面
*   用于实时搜索爬行页面的 Web 界面
*   用于爬虫监控的 REST API 和基于 web 的用户界面
*   使用 TOR 代理爬行隐藏服务

**亦读 [蝎狮:符号执行工具](https://kalilinuxtutorials.com/manticore-symbolic-execution-tool/)**

## **疼痛安装**

您可以从源代码构建 ACHE，使用`conda`下载可执行的二进制文件，或者使用 Docker 构建映像并在容器中运行 ACHE。

### **使用 Gradle 从源代码构建**

先决条件:您需要安装最新版本的 Java (JDK 8 或最新版本)。

要从源代码构建 ACHE，您可以在终端中运行以下命令:

```
git clone https://github.com/ViDA-NYU/ache.git
cd ache
./gradlew installDist
```

这将在`ache/build/install/`下生成一个安装包。然后，您可以通过将 ACHE 二进制文件添加到`PATH`环境变量中，使`ache`命令在终端中可用:

```
export ACHE_HOME="{path-to-cloned-ache-repository}/build/install/ache"
export PATH="$ACHE_HOME/bin:$PATH"
```

### **使用 Docker 运行**

先决条件:你需要安装一个最新版本的 Docker。关于如何为您的平台安装 Docker 的详细信息，请参见 https://docs.docker.com/engine/installation/。

我们在 [docker Hub](https://hub.docker.com/r/vidanyu/ache/) 上发布每个发布版本的预建 Docker 图像。您可以使用以下工具运行最新的映像:

```
docker run -p 8080:8080 vidanyu/ache:latest
```

或者，您可以自己构建映像并运行它:

```
git clone https://github.com/ViDA-NYU/ache.git
cd ache
docker build -t ache .
docker run -p 8080:8080 ache
```

Dockerfile 公开了两个数据卷，这样您就可以用您的配置文件挂载一个目录(在`/config`)并在容器停止后保留 crawler 存储的数据(在`/data`)。

### **用康达下载**

**先决条件:**您需要在系统中安装 Conda 软件包管理器。

如果您使用 Conda，您可以通过运行以下命令从 Anaconda Cloud 安装`ache`:

```
conda install -c vida-nyu ache
```

*注意:只有已发布的标记版本才会发布到 Anaconda Cloud，因此通过 conda 获得的版本可能不是最新的。如果您想尝试最新的版本，请克隆存储库并从源代码构建，或者使用 Docker 版本。*

## **跑步疼痛**

在开始抓取之前，您需要创建一个名为 **`ache.yml`** 的配置文件。我们在存储库的 [config](https://github.com/ViDA-NYU/ache/tree/master/config) 目录中提供了一些配置示例，可以帮助您入门。

您还需要一个名为`**pageclassifier.yml**`的页面分类器配置文件。有关如何配置页面分类器的详细信息，请参考[页面分类器文档](http://ache.readthedocs.io/en/latest/page-classifiers.html)。

配置好分类器后，最后需要的是一个种子文件，即每行包含一个 URL 的纯文本。爬网程序将使用这些 URL 来引导爬网。

最后，您可以使用以下命令启动爬虫程序:

```
ache startCrawl -o <data-output-path> -c <config-path> -s <seed-file> -m <model-path>
```

在哪里，

*   **`<configuration-path>`** 是包含`ache.yml`的 config 目录的路径。
*   `**<seed-file>**`是包含种子 URL 的种子文件。
*   `**<model-path>**`是包含文件`pageclassifier.yml`的模型目录的路径。
*   **`<data-output-path>`** 是数据输出目录的路径。

使用存储库中可用的样本*预训练页面分类器模型*和样本*种子文件*运行 ACHE 的示例:

```
ache startCrawl -o output -c config/sample_config -s config/sample.seeds -m config/sample_model
```

crawler 将运行日志并将其打印到控制台。随时点击`Ctrl+C`停止(可能需要一些时间)。对于长时间的爬行，您应该使用 nohup 之类的工具在后台运行 ACHE。

### **数据格式**

ACHE 可以输出多种格式的数据。目前可用的数据格式有:

*   **文件(默认)–**原始内容和元数据存储在固定大小的滚动压缩文件中。
*   **ELATICSEARCH–**原始内容和元数据被编入 elatic search 索引。
*   **KAFKA—**将原始内容和元数据推送到 Apache Kafka 主题。
*   **WARC—**使用 Web 存档和通用爬网使用的标准格式存储数据。
*   **file system _ HTML—**纯文本文件中只存储原始页面内容。
*   **file system _ JSON–**原始内容和元数据以 JSON 格式存储在文件中。
*   **文件系统 _ CBOR—**原始内容和一些元数据使用 [CBOR](http://cbor.io) 格式存储在文件中。

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/ViDA-NYU/ache)信用:aecio.santos@nyu.edu&kien.pham@nyu.edu

***你可以在 [Linkedin](https://www.linkedin.com/company/gbhackers/) 、 [Twitter](https://twitter.com/GbhackerOn) 、[脸书](https://www.facebook.com/gbhackersadmin)上关注我们的日常网络安全更新，你也可以在线参加[最佳网络安全课程](https://ethicalhackersacademy.com/)以保持自我更新。***