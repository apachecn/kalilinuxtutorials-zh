# Root stealter——在根终端插入命令的技巧

> 原文：<https://kalilinuxtutorials.com/rootstealer-inject-root-terminal/>

Rootstealer 是使用 X11 的新攻击的一个例子。该工具用于检测 linux 用户何时用 root 打开终端，用 X11 lib 注入命令。

## **root stealter 安装**

```
# apt-get install libX11-dev libxtst-dev**
**# cd rootstealer/sendkeys;
```

编辑文件 root stealter/cmd . CFG，并编写要注入的命令。

你可以采取以下措施:

```
# make; cd ..    #to back to path rootstealer/ 
# pip install gi
or
# pip install gir
```

运行 python 脚本来窥探标题中带有“root@”字符串的所有 windows gui 和搜索窗口。

```
$ python rootstealer.py &
```

```
$ sudo apt-get install libwnck-dev
$ gcc -o rootstealer rootstealer.c `pkg-config --cflags --libs libwnck-1.0` -DWNCK_I_KNOW_THIS_IS_UNSTABLE -DWNCK_COMPILATION
$ ./rootstealer &
```

**也可理解为[xat tacker——网站漏洞扫描器&自动开发工具](https://kalilinuxtutorials.com/xattacker-website-vulnerability-scanner/)**

## **视频**

[https://www.youtube.com/embed/V8sZQq7nerw?feature=oembed](https://www.youtube.com/embed/V8sZQq7nerw?feature=oembed)

## **免责声明**

我们对那个工具的邪恶使用不负任何责任。好好利用这一点。

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/CoolerVoid/rootstealer)