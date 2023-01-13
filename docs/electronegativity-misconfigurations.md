# 电负性:电子应用中识别错误配置和安全反模式的工具

> 原文：<https://kalilinuxtutorials.com/electronegativity-misconfigurations/>

电负性是在基于电子的应用中识别错误配置和安全反模式的工具。

软件开发人员和安全审计人员可以使用这个工具来检测和减少在使用 electronic 开发应用程序时潜在的弱点和实现错误。

在使用它时，仍然需要对电子(in)安全性有很好的理解，因为该工具检测到的一些潜在问题需要手动调查。

**又念: [PHP:安全检查表 2019](https://kalilinuxtutorials.com/php/)**

**安装**

主要版本被推送到 NPM，可以通过以下方式简单安装:

**$ NPM install @ doyensec/电负性-g**

**用途**

**$电负性-h**

| [计]选项 | 描述 |
| --- | --- |
| -V | 输出版本号 |
| -i，-输入 | 输入(目录，。js。html。asar) |
| -o，–输出 | 将结果保存为 csv 或 sarif 格式的文件 |
| -c，–检查 | 仅运行以 csv 格式传递的指定检查 |
| 救命啊 | 输出使用信息
 |

使用它在包含电子应用程序的目录中查找问题:

**$电负性-i /path/to/electron/app**

使用该工具在 asar 档案中查找问题，并将结果保存在 csv 文件中:

**$电负性-I/path/to/asar/archive-o result . CSV**

**注意:**如果您遇到致命错误“JavaScript 堆内存不足”，您可以使用 node–max-old-space-size = 4096 electro negativity-I/path/to/asar/archive-o result . CSV 运行 node

**鸣谢:** [**克劳迪奥·梅洛尼**](https://github.com/p4p3r)**[**伊布拉姆·马尔祖克**](https://github.com/0xibram)**[**雅罗斯拉夫·洛巴切夫斯基**](https://github.com/JarLob) **等众多** [**撰稿人**](https://github.com/doyensec/electronegativity/graphs/contributors) **。******

****[**Download**](https://github.com/doyensec/electronegativity)****