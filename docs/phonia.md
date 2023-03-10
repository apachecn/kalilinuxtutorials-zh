# Phonia:扫描电话号码的高级工具包

> 原文：<https://kalilinuxtutorials.com/phonia/>

[![Phonia : Advanced Toolkits To Scan Phone Numbers](img/8d7b8ac35fdb3b4cef5c85cd88c5f598.png "Phonia : Advanced Toolkits To Scan Phone Numbers")](https://1.bp.blogspot.com/-K4-94TW1Mag/XmNUsHtKPbI/AAAAAAAAFU8/pwvMquB9tcAWyK0mxe2kDFjHaJ5sKgL-QCLcBGAsYHQ/s1600/Phonia%2BToolkit.png)

Phonia Toolkit 是仅使用免费资源扫描电话号码的最先进的工具包之一。目标是首先收集标准信息，如国家、地区、运营商和任何国际电话号码的线路类型，并具有非常好的准确性。

**安装**

**CD phonia
chmod+x install . sh
。/install.sh**

**卸载**

**CD phonia
chmod+x uninstall . sh
。/uninstall.sh**

**也可阅读-[WiFi Passview:一个基于开源批处理脚本的 WiFi Passview For Windows](https://kalilinuxtutorials.com/wifi-passview/)**

**执行**

**phonia -h**

用法:phonia[-h][-p][-I][-o]
[-s][–recon][–no-ansi][-u]
可选参数:
-h，–help 显示此帮助消息并退出
-p，–phone
要扫描的电话号码。
-i，–输入
要扫描的电话号码列表。
-o，–Output
输出保存扫描结果。
-s，–scanner
要使用的扫描仪。
–recon 启动自定义格式侦察。
–no-ansi 禁用彩色输出。
-u，–更新更新 Phonia 工具包。

**例题**

*   扫描电话号码的示例

**phonia-p 1555443333**

*   从文件扫描的示例

**phonia-I input . txt-o output . txt**

*   选择扫描仪的示例

**phonia -p 15554443333 -s 脚印**

**免责声明**

未经双方事先同意，使用 Phonia 工具包攻击目标是非法的。最终用户有责任遵守所有适用的地方、州、联邦和国际法律。开发人员不承担任何责任，也不对本程序造成的任何误用或损坏负责。

[**Download**](https://github.com/entynetproject/phonia)