# skip tracer–osint python 网页抓取框架

> 原文：<https://kalilinuxtutorials.com/skiptracer-osint-python-webscaping/>

recon 的初始攻击向量通常涉及利用付费数据/API (Recon-NG)或付费利用转换(Maltego)来获得数据挖掘结果。Skiptracer 利用 PII 付费墙网站的一些基本 python web scraping(beautiful soup)来编译关于拉面预算目标的被动信息。

**也读作 [Hassh:用于识别特定客户端的工具&服务器 ssh 实现](https://kalilinuxtutorials.com/hassh-client-server-ssh/)**

## **Skiptracer 安装**

```
$ git clone https://github.com/xillwillx/skiptracer.git skiptracer
$ cd skiptracer
```

### **安装要求**

```
**$ pip install -r requirements.txt**
```

 `## **运行**

```
$ python skiptracer.py -l (phone|email|sn|name|plate)
```

## **样品**

[![](img/d24b50c60f6c8bbe86713af72390a825.png)](https://asciinema.org/a/RosGkr3mie2s6hjwUJC1TT2lJ)

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/xillwillx/skiptracer) ** *您可以在 [Linkedin](https://www.linkedin.com/company/gbhackers/) 、 [Twitter](https://twitter.com/GbhackerOn) 、[脸书](https://www.facebook.com/gbhackersadmin)上关注我们的日常网络安全更新，您还可以在线参加[最佳网络安全课程](https://ethicalhackersacademy.com/)以保持自我更新。***`