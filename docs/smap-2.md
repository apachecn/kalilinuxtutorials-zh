# Smap:由 Shodan 驱动的 Nmap 的替代产品。木卫一

> 原文：<https://kalilinuxtutorials.com/smap-2/>

[![](img/659d6dce0f57535630a83d91ce4818bf.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiet13mYQYHoKpKeSa695WJDkvmYFAYKH1AD7GV9EIxcyim7D7oZEJ3FfsXcHTxyKn_qXd4zOsdl36Vo6lqah50Zd9Ur2nKpIkfmDruAvYMCEHx18yVXP-EqPhdnEDKV8kS2gxCbSl9d7XvhfWk6BG4hSef-puiW2R3vghpDhK9rux8xZ0Nm5ac7klj/s728/3d5b9ffe-008a-41be-9d14-32bdcbf5b96f%20(1).png)

**Smap** 是用 shodan.io 的免费 API 搭建的端口扫描器。它采用与 Nmap 相同的命令行参数，并产生相同的输出，这使它成为 Nmap 的一个插件。

## 特性

*   每秒扫描 200 台主机
*   不需要任何帐户/api 密钥
*   漏洞检测
*   支持所有 nmap 的输出格式
*   服务和版本指纹
*   不要接触目标

## 安装

### 二进制

您可以从这里下载一个预构建的二进制文件，并立即使用它。

### 手动

`**go install -v github.com/s0md3v/smap/cmd/smap@latest**`

困惑还是什么不起作用？有关更详细的说明，请单击此处

### AUR·帕克

Smap 在 AUR 上以 smap-git(从源代码构建)和 smap-bin(预构建的二进制文件)的形式提供。

### 自制软件/苹果电脑

Smap 也可以在自制软件上获得。

**brew 更新
brew 安装 smap**

## 使用

Smap 采用与 Nmap 相同的参数，但是除了**、`-h`、`-o*`、`-iL`、**之外的选项被忽略。如果你对 Nmap 不熟悉，下面是 Smap 的使用方法。

### 指定目标

**文件夹 127 . 0 . 0 . 1 . 127 . 0 . 2**

您也可以使用目标列表，用换行符分隔。

**smap -iL targets.txt**

**支持的格式**

**1.1.1.1//IP v4 地址
example.com//主机名
178.23.56.0/8 // CIDR**

### 输出

Smap 支持 6 种输出格式，可与如下`**-o* **`一起使用

s**map example.com-oX output . XML**

如果要将输出打印到终端，请使用连字符(`**-**`)作为文件名。

**支持的格式**

**oX // nmap 的 xml 格式
oG // nmap 的 greppable 格式
oN // nmap 的默认格式
oA //同时输出以上所有 3 种格式
oP // IP:端口对用换行符分隔
oS //自定义 smap 格式
oJ // json**

注意:由于 nmap 不扫描/显示漏洞和标记，因此 Nmap 格式的数据不可用。使用`**-oS**`查看该信息。

### 指定端口

默认情况下，Smap 扫描这 1237 个端口。如果您想要显示某些端口的结果，请使用`**-p**`选项。

**smap -p21-30，80，443 -iL targets.txt**

[**Download**](https://github.com/s0md3v/smap/)