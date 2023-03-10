# ReconPal:利用 NLP 实现信息安全

> 原文：<https://kalilinuxtutorials.com/reconpal-leveraging-nlp-for-infosec/>

[![](img/fd21fe648226a8e66bfbcbb51eb79df3.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhCghXRafOAmakJZpaI3FEJHfieN2WZPxBQp-bp2ZbDChDphZU0XWn9EDPeZgF7YIxnJ89qeGtgtYoU7JIFRDENDxpKLCafHSvKtNF0U8-czFhUjv6I34GxSwl_JgwkDNegX6-GilXm3Cf8IThd6C16EIXQH0zlhVi1mOlcRxDiAcOKDcvs6vl3lU6Z/s728/169852572-c774ead7-069b-4d35-abcb-a52e349144f2%20(2).png)

侦察是最重要的阶段之一，看似简单，但要做好需要很多努力和技巧。人们需要了解正确的工具、正确的查询/语法、运行这些查询、关联信息以及净化输出。对于一个经验丰富的信息安全/侦察专业人员来说，所有这些可能都很容易做到，但对于其他人来说，这仍然近乎神奇。问一个简单的问题，比如“在新加坡给我找一个开放的支持 UDP 的 Memcached 服务器？”或者“新加坡有多少台 IP 摄像机在使用默认凭证？”在聊天中得到答案？

将基于深度学习的语言模型 GPT 3 与 Shodan 等知名的 recon 工具相集成，以产生类似人类的文本，这是 ReconPal 的基础。ReconPal 还支持使用语音命令来执行流行的攻击和侦察。

## 建有

*   开放 GPT-3
*   肖丹 API
*   语音转文本
*   电报机器人
*   码头集装箱
*   python3

# 开始使用

要重新连接并运行，请遵循以下简单步骤。

### 先决条件

*   电报机器人令牌使用机器人父亲并创建一个新的电报机器人。请参考 https://core.telegram.org/bots 的文件
*   Shodan API:
    创建一个 Shodan 帐户，并从 https://account.shodan.io/创建一个新的 API 密钥
*   Google 语音转文本 API:
    在 GCP 启用语音转文本并获取凭证。开始之前，请参考文档 https://cloud . Google . com/speech-to-text/docs/中的这些步骤
*   OpenAI API Key:
    创建一个免费的 OpenAI 账号来试用这个 API。https://beta.openai.com/account/api-keys
*   码头工人

**sudo apt-get updates
sudo apt-get install docker . io
【sudo curl-l】https://github . com/docker/compose/releases/download/1 . 26 . 0/docker-compose-(uname-s)-(uname-m)】o/usr/local/bin/docker-compose
+chmod+x/usr/local/bin/docker**

### 装置

*   克隆回购

**git 克隆 https://github.com/pentesteracademy/reconpal.git**

*   在`**docker-compose.yml**`中输入您的 OPENAI、SHODAN API 密钥和电报机器人令牌

**open ai _ API _ KEY =
shod an _ API _ KEY =
TELEGRAM _ BOT _ TOKEN =**

开始重新联系

**坞站-合成**

# 使用

打开 telegram 应用程序，选择创建的 bot 以使用 ReconPal。

*   点击开始或直接在输入框中输入。

**/开始**

*   注册模型

**/寄存器**

*   用一些命令测试该工具。

**扫描 10.0.0.8**

[**Download**](https://github.com/pentesteracademy/reconpal)