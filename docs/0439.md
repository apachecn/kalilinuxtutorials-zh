# 通过 SSH 重新安装、恢复和清除你的系统，无需重启

> 原文：<https://kalilinuxtutorials.com/reload-sh/>

Reload.sh 是一个在运行 GNU/Linux 发行版(没有光盘，flash 等)的地方，从级别上重新安装，恢复，擦除你的系统的工具。通过 SSH，无需重启。

**也可阅读:[cute it——IP 混淆器使一个恶意的 IP 变得更可爱一点](https://kalilinuxtutorials.com/cuteit-ip-obfuscator/)**

它是如何工作的？

使用系统备份设置您的归档以进行恢复:

**_ build = "/mnt/system-backup . tgz "**

设置临时系统的路径(可选):

**_ base = "/mnt/minimal-base "**

```
If you do not specify this parameter, the temporary system will be downloaded automatically.
```

设置主系统盘的路径:

**_disk="/dev/vda"**

运行 reload.sh:

**。/bin/reload . sh–base " $ _ base "-build " $ _ build "-disk " $ _ disk "**

**鸣谢:**[**trimstray**](https://github.com/trimstray)

**[**Download**](https://github.com/trimstray/reload.sh)**