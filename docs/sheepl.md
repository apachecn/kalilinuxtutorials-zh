# sheep l——在实验室环境中创建支持 Tradecraft 开发的真实用户行为

> 原文：<https://kalilinuxtutorials.com/sheepl/>

Sheepl 是一个在实验室环境中创建支持 tradecraft 开发的真实用户行为的工具。网上有很多关于如何为蓝队和红队的发展建立广告网络环境的资源。

然而，当前的解决方案在表示真实世界的网络配置时往往缺少一个重要方面。网络不仅仅是静态端点的集合，它还是人与人之间交流的平台。

shephel 是一个工具，旨在通过模拟人们在网络环境中通常采取的行为来弥合差距。使用 Python3 和 AutoIT3，可以将输出编译成独立的可执行文件，没有任何其他依赖性，当在 Windows 端点上执行时，会在选定的时间范围内随机执行一组任务。

对于红队队员来说，这有助于展示练习技巧的机会。对于蓝色团队来说，这支持集中检测良性用户任务序列中的恶意活动指标。

**也读作[cloud bunny——cloud bunny 是一个捕捉服务器真实 IP 的工具](https://kalilinuxtutorials.com/cloudbunny-real-ip-server/)**

## **绵羊工装**

Sheepl 有两种模式，命令行模式和交互模式，其中命令行模式可以作为更广泛的脚本解决方案的一部分，而交互模式允许您以问题/响应的方式构建任务。

### **例子**

```
python3 sheepl.py --name TBone --total_time=2h --wordfile "c:\\users\\matt\\Desktop\\matt.doc" --inputtext "content/if.txt" --cmd --cc "ipconfig /all" --cc "whoami" --cc "netstat -anto -p tcp"')
```

```
python3 sheepl.py --interactive
```

## **自动 3**

你可以在这里下载 AutoIT3 运行时和 Aut2EXE 编译器: [AutoIT3 下载](https://www.autoitscript.com/site/autoit/downloads/)

下面的视频是 Sheepl 0.1 测试版的概述。

## **视频教程**

[https://www.youtube.com/embed/OQdulPd97y4?feature=oembed](https://www.youtube.com/embed/OQdulPd97y4?feature=oembed)

[![](img/d861a9096555aeb1980fc054015933d7.png) ](https://github.com/SpiderLabs/sheepl) **信用:乔纳森·本内特**

***你可以在 [Linkedin](https://www.linkedin.com/company/gbhackers/) 、 [Twitter](https://twitter.com/GbhackerOn) 、[脸书](https://www.facebook.com/gbhackersadmin)上关注我们的日常网络安全更新，你也可以在线参加[最佳网络安全课程](https://ethicalhackersacademy.com/)以保持自我更新。***