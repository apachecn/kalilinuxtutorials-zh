# FakeDataGen:完全有效的假数据生成器

> 原文：<https://kalilinuxtutorials.com/fakedatagen/>

[![](img/3b0cb18e780a322f2c17ca94c556c26f.png)](https://blogger.googleusercontent.com/img/a/AVvXsEhteOyHXs48K0zW3PN_7nm21U_jhXkqOaoMANBMXJ_gIEOOzg3E4t362-GgTM1XkayV5l0_QpCrPOYIWck2zlS1ahdwcmOuZpD60lFqKAInJfFmW3HcH3M7HEcFH6HG9C1Y9elc7JB9iIrBDaVTnzhrvzzX2yaat9jVQT9M9cq7GHXs7FrLZntxyO3Q=s728)

**FakeDataGen** 是一个完全有效的伪数据生成器。这个工具帮助你用完全有效的数据创建假账户(西班牙格式)。在这些信息中，您可以找到最常见的姓名、电子邮件、银行详细信息和其他有用的信息。

**要求**

*   python3
*   安装要求. txt

**下载**

建议克隆完整的存储库或下载 zip 文件。您可以通过运行以下命令来实现这一点:

```
git clone https://github.com/JoelGMSec/FakeDataGen
```

**用途**

```
./FakeDataGen.py -h

  _____     _        ____        _         ____            
 |  ___|_ _| | _ ___|  _ \  __ _| |_ __ _ / ___| ___ _ __  
 | |_ / _` | |/ / _ \ | | |/ _` | __/ _` | |  _ / _ \ '_ \ 
 |  _| (_| |   <  __/ |_| | (_| | || (_| | |_| |  __/ | | |
 |_|  \__,_|_|\_\___|____/ \__,_|\__\__,_|\____|\___|_| |_|

  -------------------- by @JoelGMSec ---------------------

usage: FakeDataGen.py [-h] [-n NUMBER] [-b] [-e] [-f FILE] [-z] [-p PASSWORD]

optional arguments:
  -h, --help            show this help message and exit
  -n NUMBER, --number NUMBER
                        The number of records should be created
  -b, --bankdata        Show only bank data (Card, CVV, IBAN..)
  -e, --extended        Show only extended info (City, Phone, SS..)
  -f FILE, --file FILE  File path to save data
  -z, --zip             Compress data to zip file
  -p PASSWORD, --password PASSWORD
                        Password to protect zip file 
```

**[点击此处](https://darkbyte.net/generando-datos-falsos-con-fakedatagen)** 查看详细指南。

[**Download**](https://github.com/JoelGMSec/FakeDataGen)