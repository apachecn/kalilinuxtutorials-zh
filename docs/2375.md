# SMBSR:在 SMB 股票中寻找有趣的东西

> 原文：<https://kalilinuxtutorials.com/smbsr/>

[![](img/ac917629ab2ada89679df13bbe00e33f.png)](https://blogger.googleusercontent.com/img/a/AVvXsEhVdX1V5ZTBNJ3pFPRVBTGYUfdXIUmfEE20gsPZ2ldiBZll8begNEb5EyJoc_-qwyBRnpgGpwYy_VHXGIVItwAlwXOAYeXGY_2E_marqWhTMFBE9uDpjpetb4lmk-IZFMk7G9pnBzU67_C0Ke7_NddAM8GVSIa62Ay_rAJQvi3PdgRgU13BWpxnuOyS=s728)

**SMBSR** 是一个 python 脚本，它给出了一个 CIDR/IP/IP_file/HOSTNAME(s ),列举了在目标中监听(445)的所有 SMB 服务，并尝试对它们进行验证；如果认证成功，那么所有的文件夹和子文件夹被递归地访问，以便在文件和…秘密文件中找到秘密。为了扫描 SMB 端口打开的目标，使用 masscan 模块。SMBSR 认为有趣的事情基于其:

*   内容
*   延长
*   名字

该工具应该寻找的有趣的关键字是通过命令行定义的，还有:

*   文件扩展名黑名单(该列表在运行时根据线程抛出的异常和文件类型自动更新)
*   股票黑名单
*   文件夹黑名单(小心，子文件夹也不见了)
*   螺纹扣数
*   我该不该做弥撒？
*   有趣的文件扩展名(我猜像 ppk，kdbx，…)
*   允许检查的最大文件大小(字节)(相信我，太大可能需要一些时间)
*   我应该将结果导出到两个漂亮的 CSV 文件中吗？
*   我应该查看子文件夹多深？
*   要匹配的正则表达式的单词列表
*   ldap 绑定的域控制器 IP
*   其他常见的和必需的

当然，一切都保存在本地的 SQlite 数据库中。数据库包含一个用于“希望是阿达密码”匹配的表，称为 smbsr，包含以下各列:

*   文件
*   分享
*   互联网协议（Internet Protocol 的缩写）
*   位置
*   与...匹配
*   编成日期
*   上次修改日期
*   上次访问日期
*   计数(如果同一个文件中有多个匹配项，则该匹配项将递增)

以及另一个包含以下列的感兴趣文件列表的表格:

*   文件
*   分享
*   互联网协议（Internet Protocol 的缩写）
*   编成日期
*   上次修改日期
*   上次访问日期

## 支持的文件

SMBSR 学会了如何阅读:

*   。通过 python 内置的 csv
*   。doc 通过 antiword
*   。docx via python-docx2txt
*   。通过 python 内置的 eml
*   。epub via 电子书库
*   。通过 tesseract-ocr 生成 gif
*   。jpg 和。通过 tesseract-ocr 的 jpeg
*   。通过 python 内置的 json
*   。html 和。htm via beautifulsoup4
*   . mp3 通过 sox、SpeechRecognition 和 pocketsphinx
*   。通过消息提取器提取消息
*   。通过 python 内置的 odt
*   。ogg via sox、SpeechRecognition 和 pocketsphinx
*   。通过 pdftotext(默认)或 pdfminer*生成 pdf。六
*   。png 通过 tesseract-ocr
*   。通过 python-pptx
*   。ps 通过 ps2text
*   。rtf 通过 unrtf
*   。蒂芙和。tif 通过 tesseract-ocr
*   。通过 python 内置的 txt
*   。wav via SpeechRecognition 和 pocketsphinx
*   。xlsx 通过 xlrd
*   。xls via xlrd

## LDAP

终于来了！现在，为 SMB 连接指定的域凭据也可以用于从 Active Directory 中检索计算机对象列表。

## reg_gen.py

在最近一次更新中，SMBSR 被授予了查找与给定正则表达式相匹配的秘密的权力(参见 regulars.txt 文件，其中包含一些很好的匹配示例)。鉴于这种新的超级能力，我还实现了一个新的脚本，它给出了一个单词列表，生成一个正则表达式列表，该列表与它在单词列表中找到的密码模式相匹配。在打印出所有内容之前，正则表达式列表被(排序)编辑。如果模式在一行中出现两个或更多的 ascii_lower，可以对脚本进行优化，但现在不是这样的。

## 要求

**pip 3 install-r requirements . txt**

## 使用

例如，从项目文件夹中:

**。/smbsr . py-IP 127 . 0 . 0 . 1-word-list-path to match . txt-thread-max-size 1000-T2-username o B- password ' * * * * *-domain o B- file-extensions dll，exe，bin**

[**Download**](https://github.com/oldboy21/SMBSR)