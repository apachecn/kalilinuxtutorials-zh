# PEM cracker–破解加密 PEM 文件的工具

> 原文：<https://kalilinuxtutorials.com/pemcracker-encrypted-pem/>

**Pemcracker** 是一款破解加密 PEM 文件的工具。这个工具的灵感来自于 **Robert Graham** 的 pemcrack。目的是在利用所有 CPU 内核的同时，尝试恢复加密 PEM 文件的密码。

它仍然使用高级 OpenSSL 调用来猜测密码。作为一种优化，它不是不断地检查磁盘上的 PEM，而是加载到每个线程的内存中。

**也读作 [电光火石——破解蓝牙智能加密](https://kalilinuxtutorials.com/crackle-crack-bluetooth/)**

```
bwall@ragnarok:~$ ./pemcracker** 
**pemcracker 0.1.0**
**pemcracker <path to pem> <word file>**
**pemcracker 0.1.0 by Brian Wallace (@botnet_hunter)
```

## **Pemcracker 用法举例**

```
bwall@ragnarok:~/data/publicprojects/pemcracker$ ./pemcracker test.pem test.dict
Password is komodia for test.pem 
```

## **编译**

```
make
```

这是一个短期的项目，所以我为任何问题道歉。如果有这个项目进一步发展的愿望，我会尽量分配时间。

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/bwall/pemcracker)