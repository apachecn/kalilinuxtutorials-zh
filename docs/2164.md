# LinuxCatScale:带有自动报告脚本的事件响应收集和处理脚本

> 原文：<https://kalilinuxtutorials.com/linuxcatscale/>

[![](img/bee385b7fceab2645d46e0b611f9eeb2.png)](https://blogger.googleusercontent.com/img/a/AVvXsEjS3YyyPupAs5auxeaTIjoGWUdQCjfZ-oP8gj2inIj1rwzT_gE83Pm5Ya0fwPQIA2stnTb6hwqd-pRhNGG57xesXFd3dtZw_rk79mNuy6o0G5zq4-13SGWSkyvW4tDb8YuHfuxfxl2aajO1nb4KIFihJyUqGaQ_38ib82G3S5ptsZ1Q2bBc9Bd4CTvj=s728)

**Linux CatScale** 是一个 bash 脚本，它使用 live of the land 工具从基于 Linux 的主机收集大量数据。这些数据旨在帮助 DFIR 专业人员分流和确定事故范围。Elk Stack 实例也被配置为使用输出并协助分析过程。

**用法**

这些脚本被构建为尽可能自动化。我们建议从外部设备/usb 运行它，以避免覆盖证据。以防你将来需要一个完整的图像。

请在具有 sudo 权限的可疑主机上运行收集脚本。f secure _ incident-response _ Linux _ collector _ 0.7 . sh 运行收集所需的唯一文件。

**用户@怀疑主机:$ chmod +x ./Cat-Scale.sh
用户@怀疑主机:$ sudo。/Cat-Scale.sh**

该脚本将在工作目录中创建一个名为“FSecure-out”的目录，并应在压缩后删除所有人工制品。这将留下一个`**FSecure_Hostname-YYMMDD-HHMM.tar.gz**`格式的文件名

一旦这些都被汇总，并且在分析机器上有了`**FSecure_Hostname-YYMMDD-HHMM.tar.gz**`。您可以运行 Extract-Cat-Scale.sh，它将提取所有文件，并将它们放在名为“extracted”的文件夹中。

**user @ analysis host:$ chmod+x ./Extract-Cat-scale . sh
user @ analysis host:$ sudo。/Extract-Cat-Scale.sh**

**解析**

这个项目预定义了 grok 过滤器来将数据导入到 elastic 中，您可以根据需要随意修改它们。

**它收集什么？**

这个脚本将产生输出并存档。目前，它收集的最新信息包含在以下博客文章中:https://labs . f-secure . com/tools/cat-scale-Linux-incident-response-collection/

[**Download**](https://github.com/FSecureLABS/LinuxCatScale)