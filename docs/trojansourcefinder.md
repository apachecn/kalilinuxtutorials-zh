# TrojanSourceFinder:帮助查找代码中的木马源漏洞

> 原文：<https://kalilinuxtutorials.com/trojansourcefinder/>

[![](img/45d1d3d117eaf30c17512522c2151ea2.png)](https://blogger.googleusercontent.com/img/a/AVvXsEg20LD0UWlKXCCjUxXVPIIpgp30TQR-sMq5DoIP29lYasA4cOn3lEKHvNuEWeGI5zXi5B7bWHaF7sXNOJU86NreG2N65n8NU0treEeFDUBEZPO74GFqK3FK4tkTQjOPVgFUoRofoygQYh-Si_0ITtYdzMLKCs551c9YHD3jybGF7Q2o1u63ZL3JztmF=s435)

TrojanSourceFinder 是一个特洛伊木马源漏洞，允许攻击者使恶意代码看起来是无辜的。一般来说，攻击者试图通过把他的代码当作注释(视觉上)来引诱。这是一个严重的威胁，因为它涉及许多语言。具有多个“不可信”来源的项目可能会受到关注。

**安装**

### 同`go`

*经`**go install**`到*

**去安装 github.com/ariary/TrojanSourceFinder/cmd/tsfinder@latest**

确保`**$GOPATH**`在您的`**$PATH**`中

*来源于*

**git 克隆 https://github.com/ariary/TrojanSourceFinder
CD 木马 source finder
make before . build
make build . ts finder**

如果命令`**make build.tsfinder**`失败，尝试:

env GOOS = target-OS go arch = target-architecture
go build-o ts finder cmd/main . go

### 用`curl`

*从发布*

**curl-lO-L https://github . com/ariary/trojan source finder/releases/latest/download/ts finder&chmod+x ts finder**

**检测木马来源**

*>通过手动代码审查或 CI/CD 管道(Unicode 双向字符)帮助检测木马源*

检测文件或目录 *<路径>* 中的木马源:

**tsfinder【路径】**

**仅在文本文件中检测**

*>源代码文件很可能是文本文件。提取它们进行扫描有助于排除假阳性*

**ts finder-t[路径]**

添加`**-v**`帮助查看扫描跳过了哪个文件。

**更进一步*(同形)***

木马来源并不新鲜，也不是唯一的危害。还有一个是*“同形”*。(*凯萨科？*)

tsfinder 使用`**homoglyph**`命令帮助检测它们:

**tsfinder 同形[文件名][标志]**

您可以使用标志`**--sibling**`查看在`**path**`中找到的同形异义词是否有兄弟词(即具有相同“骨架”的词):

**tsfinder 同形符号[文件名]–兄弟[路径]**

**可视化木马来源**

*>想象机器/编译器是如何解释代码的*

*tsfinder* 故意不怎么啰嗦。默认情况下，只有在检测到木马源代码时才会输出。为了有更多的赘述和**视觉化的危险线，添加旗帜`-v`** 。

为了更好地查看特洛伊木马的来源，您可以使用`**-c**`标志启用彩色输出(对目录扫描也很有用):

**tsfinder -c -v**

**演示**

![](img/cade7d2f90a77d528f3edc5a39dd31c5.png)

**同形字**

![](img/cd1791dae49e232d83cbb8b224285a38.png)[**Download**](https://github.com/ariary/TrojanSourceFinder)