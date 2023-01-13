# Socialhunter:抓取网站并找到可能被劫持的断开的社交媒体链接

> 原文：<https://kalilinuxtutorials.com/socialhunter/>

[![](img/72838c35f8a1007ec22030bc527a1861.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhv983PGdpuFV9Cqj760j7YYTbFHuoCP-s3AtzRVtUJswgWEGMGJuAm-QY4HqlmJhflfxnyjVqOtHA8iX86EeHagJ-4TLnxDN-qy-clHLwFO3hOOCNIljj2verAcZj2ECe8foK7A4dovNk8z8OI_jgZAkjmM_MJqU7PthDTveuR93O1SgdMLg66P_pz/s728/download%20(1).png)

**Socialhunter** ，抓取给定的 URL 并找到可能被劫持的断开的社交媒体链接。断开的社交链接可能允许攻击者进行网络钓鱼攻击。这也可能会损害公司的声誉。在 bug bounty 项目中，破碎的社交媒体劫持问题通常被接受。

# 装置

## 来自二进制

您可以从 releases 页面下载预构建的二进制文件并运行。例如:

`**wget https://github.com/utkusen/socialhunter/releases/download/v0.1.1/socialhunter_0.1.1_Linux_amd64.tar.gz**`

`**tar xzvf socialhunter_0.1.1_Linux_amd64.tar.gz**`

`**./socialhunter --help**`

## 来源

*   在您的系统上安装 Go
*   运行:`**go get -u github.com/utkusen/socialhunter**`

# 用法

socialhunter 需要两个参数才能运行:

`**-f**`:逐行包含 URL 的文本文件的路径。爬行功能是路径感知的。例如，如果 URL 是`**https://utkusen.com/blog**`，它只抓取`**/blog**`路径下的页面

`**-w**`:运行的工人数量(如`**-w 10**`)。默认值为 5。您可以通过测试系统的能力来增加或减少这一点。

[**Download**](https://github.com/utkusen/socialhunter)