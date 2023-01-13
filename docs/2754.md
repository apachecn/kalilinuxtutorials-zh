# Shomon : Shodan 监控集成

> 原文：<https://kalilinuxtutorials.com/shomon/>

[![](img/b0fb25c97da07851a0f0127b0a6f17d3.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEilNMgxAkFjh0hy7bJ_OkXUMHpNdaw-G0eKzZwAX-GFCPDpbsIzG-EHK6m6sAypkcX8yJhQotcD3HUF2jQY1AEOc7skAUMm2PomsriLpgWoqUBT-Fa1n1J7BdLAEZ_Kx3WSkjifFdyDCnjHX8Ufl8rkTDpmX_zQHGNqN0F6V90NPvrbpgY1YnNo4Aon/s728/Shomon.png)

ShoMon 是一个 Shodan 提醒 feeder，为 GoLang 写的。有了 2.0 版本，比以前更强大了！

## 功能

*   可用作 Webhook 或流监听器
    *   Webhook 监听器为 Shodan 打开一个 restful API 端点来发送警报。这意味着您需要使此端点对公共网络可用
    *   流监听器连接到 Shodan 并获取/解析警报流
*   利用 [shadowscatcher/shodan](https://github.com/shadowscatcher/shodan) (奇妙的工作)进行 shodan 互动。
*   控制台日志是 JSON 格式的，可以被任何其他日志管理工具接收
*   通过 Github Actions 的 CI/CD 确保 ghcr 和 dockerhub 上的变更日志、工件和图像的正确发布
*   为 Hive，dependencies 提供一个工作的 [docker-compose 文件](https://github.com/KaanSK/shomon/blob/master/docker-compose.yml)文件
*   超快和超迷你的尺寸
*   v2.0 中完整的代码重构产生了更加模块化、可维护的代码
*   通过配置文件或环境变量，可以动态调整警报细节，包括标签、类型、警报模板。参见[配置文件](https://github.com/KaanSK/shomon/blob/master/conf.yaml)。
*   完整的横幅可以包含在警报中，直接链接到 Shodan 调查结果。

IP 被添加到可观察项中

## 使用

*   应通过`conf.yaml`或环境变量提供参数。请参见[配置文件](https://github.com/KaanSK/shomon/blob/master/conf.yaml)和 [docker-compose 文件](https://github.com/KaanSK/shomon/blob/master/docker-compose.yml)
*   设置好配置或环境变量后，只需发出命令:`./shomon`

## 笔记

*   警报参考是 md5 的前 6 个字符(“ip:port”)
*   一次只能激活一个 mod。Webhook 和流侦听器不能一起激活。

## 设置&编译指令

### 从版本中获取最新编译的二进制文件

1.  检查[释放](https://github.com/KaanSK/shomon/releases/latest)部分。

### 从源代码编译

1.  确保您有一个可用的 Golang 工作空间。
2.  `go build .`
    *   `go build -ldflags="-s -w" .`可用于定制编译和产生更小的二进制。

### 使用公共容器注册表

1.  由于新的 CI/CD 集成，最新版本的内置映像被推送到 ghcr、DockerHub，并可通过以下方式使用:
    *   `docker pull ghcr.io/kaansk/shomon`
    *   `docker pull kaansk/shomon`

### 使用 [Dockerfile](https://github.com/KaanSK/shomon/blob/master/Dockerfile)

1.  编辑[配置文件](https://github.com/KaanSK/shomon/blob/master/conf.yaml)或为下面的命令提供环境变量
2.  `docker build -t shomon .`
3.  `docker run -it shomon`

### 使用 [docker-compose 文件](https://github.com/KaanSK/shomon/blob/master/docker-compose.yml)

1.  在 [docker-compose 文件](https://github.com/KaanSK/shomon/blob/master/docker-compose.yml)中编辑环境变量和配置
2.  `docker-compose run -d`

[Click Here To Download](https://github.com/KaanSK/shomon)