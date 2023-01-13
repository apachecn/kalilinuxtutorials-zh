# MurmurHash:计算 Favicon 的 MurMurHash 值的工具，用于在 Shodan 平台上搜索钓鱼网站

> 原文：<https://kalilinuxtutorials.com/murmurhash/>

[![MurMurHash : Tool To Calculate A MurmurHash Value Of A Favicon To Hunt Phishing Websites On The Shodan Platform](img/b6f1449e33ebe739677c7acda8bfc580.png "MurMurHash : Tool To Calculate A MurmurHash Value Of A Favicon To Hunt Phishing Websites On The Shodan Platform")](https://1.bp.blogspot.com/-yrKiWsLA6BM/YLsrjljnYUI/AAAAAAAAJVI/mt-vEa9Om7sQnyEbepWSToSZpBQIo9GuQCLcBGAsYHQ/s728/MurMurHash%25281%2529.png)

**MurMurHash** 是一个用来计算 favicon 的 MurMurHash 值的工具，用来在 Shodan 平台上搜索钓鱼网站。

![](img/ee6704aa74d8b78496b37af0012e95b8.png)

**什么是 MurMurHash？**

MurmurHash 是一个非加密哈希函数，适用于一般的基于哈希的查找。这个名字来自两个基本操作，乘法(MU)和旋转(R)，用在它的内部循环中。当前版本是 MurmurHash3，它产生 32 位或 128 位哈希值。当使用 128 位时，x86 和 x64 版本不会产生相同的值，因为算法针对各自的平台进行了优化。MurmurHash3 是和 SMHasher 一起发布的——一个哈希函数测试套件。

**如何安装？**

**git 克隆 https://github.com/Viralmaniar/MurMurHash.git
CD MurMurHash
pip install-r requirements . txt
python murhash . py**

**为 Paypal 寻找费西合唱团事件&特斯拉**

在阅读了关于使用 favicon 散列搜索钓鱼网站的文章后，我想将其一般化，接受 Favicon URLs，以便在 Shodan 上进行快速分析。

在 paypal 的原始网站上寻找 favicon 图标文件:

![](img/cface0d81fba29b22176083df8185047.png)

使用`**MurMurHash.py**`文件生成图标的哈希:

![](img/aba3c06e04e8d780df7113a60bd1b379.png)

在 Shodan 上搜索 Paypal 钓鱼域名/IP:

[https://www.shodan.io/search?query = http . favicon . hash % 3a 309020573](https://www.shodan.io/search?query=http.favicon.hash%3A309020573)

![](img/b87d6421ad09910da56960293250f580.png)![](img/c544e99675522a2943a036fd4c79680d.png)![](img/a022bec6865249f78bdbffd19d16d3c5.png)

现在，让我们在原始网站上搜索特斯拉图标:

![](img/eff2a75482a7610681d68d85296c27c0.png)

在 Shodan 上搜索 Tesla 钓鱼域名/IP:

![](img/0aecbc16fe4ca59642d130ce2bc2f847.png)

*   [https://www.shodan.io/search?query = http . favicon . hash % 3a 476528568](https://www.shodan.io/search?query=http.favicon.hash%3A476528568)

![](img/0ea8945c9ea6e26d753ef6f948d66cc5.png)

验证 Shodan 结果:

![](img/71068dca5f2557da58a4e4e6cd995bb3.png)[**Download**](https://github.com/Viralmaniar/MurMurHash)