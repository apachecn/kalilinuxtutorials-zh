# imago Forensics:从图像中提取数字证据的 Python 工具

> 原文：<https://kalilinuxtutorials.com/imago-forensics/>

Imago 是一个 python 工具，可以递归地从图像中提取数字证据。该工具在整个数字取证调查中非常有用。如果你需要提取数字证据，并且你有许多图像，通过这个工具你将能够很容易地比较它们。

Imago 允许将证据提取到 CSV 文件或 sqlite 数据库中。如果在 JPEG exif 中显示 GPS 坐标，Imago 可以提取经度和纬度，并将其转换为度数，检索相关信息，如城市、国家、邮政编码等

它还提供了计算误差水平分析的可能性，并检测裸露，这些功能都在测试阶段。

**也可阅读-[R3 con 1 z 3 r:一款具有直观特性的轻量级网络信息收集工具](https://kalilinuxtutorials.com/r3con1z3r/)**

**设置**

**安装 imago:**

$ pip 安装图像

**安装后，一个新的二进制文件应该可用::**

**$意象**

**然后它应该输出图像的横幅**

**要求:**

*   python 2.7
*   exifread 2.1.2
*   python-magic
*   主张 1.4.0
*   枕头 5.2.0
*   nudepy 0.4
*   图像哈希 4.0
*   geopy 1.16.0

**用途**

用法:imago . py[-h]-I INPUT[-x][-g][-e][-n][-d { MD5，sha256，sha512，all}]
[-p {ahash，phash，dhash，whash，all }][-o OUTPUT][-s][-T1][-t { JPEG，tiff}]
可选参数:
-h，–help 显示此帮助信息并退出
-i INPUT，–INPUT INPUT
INPUT
-e，–ela 提取，错误等级分析图像，仅适用于
JPEG。 *BETA*
-n，–nude 检测裸体，仅适用于 JPEG， *BETA*
-d {md5，sha256，sha512，all}，–digest { MD5，sha256，sha512，all}
计算感知图像哈希
-p {ahash，phash，dhash，whash，all}，–percentualhash { ahash，phash，dhash，whash，all }【T17

唯一需要的参数是-i，它是 imago 开始搜索图像文件的基本目录。您还应该提供至少一种提取类型(即 exif、data、gps、digest)。

**举例:**

**$ imago-I/home/solvent/cases/c23/DCIM/-o/home/solvent/cases/c23/-x-s-t JPEG-d all**

**其中:**

*   i path:是基目录，imago 将在其中搜索文件
*   o path:输出目录，imago 将在其中保存 CSV 文件和提取的元数据
*   x : imago 将提取 EXIF 元数据。
*   s:临时 SQLite 数据库在处理后不会被删除。
*   t jpeg: imago 将只搜索 jpeg 图像。
*   d all: imago 将为 jpeg 图像计算 md5、sha256 和 sha512。

[**Download**](https://github.com/redaelli/imago-forensics)