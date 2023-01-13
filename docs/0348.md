# Secret Keeper:用给定的密钥加密和解密文件的 Python 脚本

> 原文：<https://kalilinuxtutorials.com/secret-keeper-encrypt-decrypt-key/>

Secret Keeper 是一个用 python 编写的文件加密器，它使用高级加密标准(AES)加密你的文件。创建 AES 密码时使用 CBC 模式，其中每个块都链接到流中的前一个块。

**也读作 [XSS Fuzzer:根据用户定义的向量生成 XSS 有效载荷的工具& Fuzzing 列表](https://kalilinuxtutorials.com/xssfuzzer-xss-payloads/)**

## **秘密守护者功能**

1.  Secret Keeper 能够根据用户输入生成随机加密密钥。
2.  保密人可以成功地加密和解密。txt 和。docx 文件类型。

## **如何在 Linux 下安装运行？**

*   在终端中输入以下命令进行下载。

**`git clone https://github.com/Sameera-Madhushan/Secret-Keeper`**

*   下载程序后，输入以下命令导航到 Digger 目录并列出内容

**`cd Secret-Keeper && ls`**

*   安装依赖项

`**pip3 install -r requirements.txt**`

*   现在用下面的命令运行脚本。

T2`**python3 Secret-Keeper.py**`

### 如何在 Windows 中安装和运行

*   从[Python.org](https://python.org)下载并运行 Python 2.7.x 和 Python 3.7 安装文件
    *   在安装 Python 3.7 中，启用将 Python 3.6 添加到路径
*   从[Git-scm.com](https://git-scm.com/)下载并运行 Git 安装文件，从 Windows 命令 Propmt 中选择使用 Git。
*   之后，运行命令 Propmt 并输入以下命令:

```
git clone https://github.com/Sameera-Madhushan/Secret-Keeper
cd Secret-Keeper
pip3 install -r requirements.txt
python3 Secret-Keeper.py
```

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/Sameera-Madhushan/Secret-Keeper) ** *您可以在 [Linkedin](https://www.linkedin.com/company/gbhackers/) 、 [Twitter](https://twitter.com/GbhackerOn) 、[脸书](https://www.facebook.com/gbhackersadmin)上关注我们的日常网络安全更新，您还可以在线参加[最佳网络安全课程](https://ethicalhackersacademy.com/)以保持自我更新。***