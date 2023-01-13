# IPED:数字取证工具——处理和分析数字证据

> 原文：<https://kalilinuxtutorials.com/iped/>

[![IPED : Digital Forensic Tool – Process And Analyze Digital Evidence](img/4d77066d05a6684ae10a7670b872de89.png "IPED : Digital Forensic Tool – Process And Analyze Digital Evidence")](https://1.bp.blogspot.com/-eUS7R765gBo/YLTkfJ-mIsI/AAAAAAAAJQ4/8bb91jGeeEQY_Uw-Ukpr55MZRN7nPTVvACLcBGAsYHQ/s728/IPED%25281%2529.png)

**IPED** 是一款开源软件，可用于处理和分析数字证据，通常由执法部门在犯罪现场或由私人检查员在企业调查中查获。

**简介**

数字证据处理器和索引器(从葡萄牙语翻译过来)是一个用 java 实现的工具，最初由巴西联邦警察局的数字法医专家开发，自 2012 年以来一直在开发。虽然它一直是开源的，但直到 2019 年它的代码才正式公开。

从一开始，该工具的目标就是高效的数据处理和稳定性。该工具的一些关键特征是:

*   用于批量案例创建的命令行数据处理
*   多平台支持，在 Windows 和 Linux 系统上测试
*   无需安装的便携式机箱，您可以从可移动驱动器上运行它们
*   集成和直观的分析界面
*   高多线程性能和对大型案例的支持:截至 2019 年 12 月 12 日，多达 1.35 亿个项目

目前 IPED 只使用 [Sleuthkit 库](https://github.com/sleuthkit/sleuthkit)来解码磁盘映像和文件系统，所以支持相同的映像格式:RAW/DD、E01、AFF、VHD、VMDK、ISO9660。还支持 UDF(ISO)、AD1 (AccessData)和 UFDR (Cellebrite)格式。由于 Sleuthkit 的 BlackBag 实现，最近增加了对 APFS 的支持。

如果您是该工具的新手，请参考[初学者入门指南](https://github.com/lfcnassif/IPED/wiki/Beginner's-Start-Guide)。

**大楼**

要从源代码构建，需要安装 git、maven 和 java 8 (Oracle 或 OpenJDK+JFX)。运行:

**git 克隆 https://github.com/sepinf-inc/IPED.git
CD IPED
mvn 安装**

它将在目标/发布文件夹中生成 IPED 的快照版本。

在 Linux 上，您还必须构建 Sleuthkit 和其他依赖项。请参考 [Linux 章节](https://github.com/sepinf-inc/IPED/wiki/Linux)

如果您想为项目做贡献，请参考[贡献](https://github.com/lfcnassif/IPED/wiki/Contributing)

**特性**

下面列出了 ipad 的一些功能:

*   支持的哈希:md5，sha-1，sha-256，sha-512 和 edonkey。PhotoDNA 也可用于执法(请联系[iped@dpf.gov.br](mailto:iped@dpf.gov.br))
*   快速哈希重复数据删除、NIST NSRL、ProjectVIC 和 LED 哈希集查找
*   签名分析
*   按文件类型和属性分类
*   几十种文件格式的递归容器扩展
*   数百种格式的图像和视频库
*   GPS 数据的地理参考(需要 Google Maps Javascript API 密钥)
*   Regex 搜索可选脚本验证的信用卡，电子邮件，网址，货币价值，比特币，以太坊，波纹钱包…
*   嵌入式十六进制、unicode 文本、元数据和本机查看器
*   文件内容和元数据索引以及快速搜索，包括未知文件和未分配空间
*   高效的数据雕刻引擎(花费不到 10%的处理时间),扫描的数据远多于未分配的数据，支持+40 种文件格式，包括视频，可通过脚本扩展
*   由宇宙魔方 4 支持的光学字符识别
*   已知格式的加密检测和使用熵测试
*   处理配置文件:法医、pedo (csam)、检伤分类、快速模式(预览)和盲检(用于自动数据提取)
*   检测+70 种语言
*   命名实体识别(需要下载斯坦福 CoreNLP 模型)
*   基于任何文件元数据的可定制过滤器
*   具有可配置阈值的相似文档搜索
*   使用内部或外部图像的相似图像搜索
*   基于任何元数据的强大文件分组(群集)
*   支持多达 1.35 亿个项目的多案例
*   可通过 javascript 和 python(包括 cpython 扩展)脚本进行扩展
*   用于文件解码的外部命令行工具集成
*   Edge、Firefox、Chrome 和 Safari 的浏览器历史记录
*   Emule、Shareaza、Ares、WhatsApp、Skype、Telegram、Bittorrent、ActivitiesCache 等等的自定义解析器…
*   使用随机森林算法对图像和视频进行快速裸体检测(感谢其作者 Wladimir Leite)
*   使用 Yahoo open-nsfw 深度学习模型的裸体检测(需要 keras 和 jep)
*   音频转录，使用 Azure 和谷歌云服务实现
*   通信图表分析(电话、电子邮件、即时消息……)
*   通过进程外文件系统解码和文件解析实现稳定处理
*   恢复或重新启动已停止或中止的处理(–continue/–restart 选项)
*   用于搜索远程案例、获取文件元数据、原始内容、解码文本、缩略图和发布书签的 Web API
*   为感兴趣的数据创建书签/标签
*   带有标记数据的 HTML、CSV 报告和便携案例

[**Download**](https://github.com/sepinf-inc/IPED#features)