# Cryptondie:一种为研究目的开发的勒索软件

> 原文：<https://kalilinuxtutorials.com/cryptondie-ransomware-developed-study-purposes/>

[![Cryptondie : A Ransomware Developed For Study Purposes](img/2866278d15948c201a6fdcb41c4bcc82.png "Cryptondie : A Ransomware Developed For Study Purposes")](https://1.bp.blogspot.com/-TgtELIQB-ag/XZTjHdboatI/AAAAAAAACxg/TiGbUY9EehgX9v1AJpok-0A8unvR6jU6gCLcBGAsYHQ/s1600/images.png)

**CryptonDie** 是一款为研究目的开发的勒索软件。

**选项**

**–key**用于加密和解密文件的密钥，默认为随机字符串
**–dir**攻击的主目录，默认为/
**–Encrypt**加密所有文件
**–Decrypt**解密所有文件
**–verbose**主动详细模式，默认为 False

**示例:** python 3 cryptondie . py–we b-service http://1

**网络服务端点**

**GET-/targets–列出所有目标(以 JSON 格式返回)
GET-/targets/–按 id 列出一个目标(以 JSON 格式返回)
POST-/target/–创建新目标**

**又读-[Kube-Alien:向 k8s 集群](https://kalilinuxtutorials.com/kube-alien-launch-attack-k8s-cluster/)T3 发起攻击的工具】**

**怎么跑？**

**克隆库**

**git 克隆 https://github.com/zer0dx/cryptondie**

**安装要求**

**pip 3 install-r requirements . txt**

**运行 web 服务**

**CD cryptondie/discovery
python 3 service _ discovery . py**

**在 Docker 中运行**

**码头工建造-t 密码锁。
坞站运行-it 加密/bin/bash
python 加密。py–web 服务 http://127 . 0 . 0 . 1:5000–dir/var/www/–encrypt–verbose**

**实现了哪种加密？**

**高级加密标准**

[**Download**](https://github.com/zer0dx/cryptondie)