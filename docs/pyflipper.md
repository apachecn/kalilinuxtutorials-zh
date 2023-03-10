# pyFlipper:用 Python 编写的非官方 Flipper Zero Cli 包装器

> 原文：<https://kalilinuxtutorials.com/pyflipper/>

[![](img/d67049a41975bb1247491e1d2bc86a4b.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhQubZQ7bs51Zt8RCoFQzQ8sJ-IXfTjNPeE0gdXCmBPFWb9UUmHq5b87tZib3vKmd12nafvFkEZIa9ZJvRn9cT0Bca697-EK6DuufighkQj807tzrt--Lehm865KERpgki2EmwFmyF-q_GlTZwLqaDs0Lo6QqgxLrA-__VJH81d3tpw2sdymKsxjizF/s728/5390101597072781541.png)

pyFlipper 是一个用 Python 编写的非官方的 Flipper Zero cli 包装器。

## 功能和特点

*   Flipper 串行 CLI 封装程序
*   Websocket 客户端接口

安装说明

**$ git 克隆 https://github.com/wh00hw/pyFlipper.git
$ CD py flipper
$ python 3-m venv venv
$ source venv/bin/activate
$ pip install-r requirements . txt**

### 测试于

*   Linux 5.4.0 x86_64 上的 Python 3.8.10
*   Windows 10 上的 Python 3.9.10
*   Android 12 上的 python 3 . 10 . 5(Termux+otgserial 2 web socket 不需要 ROOT)

## 用法/示例

### 连接

**从 pyflipper 导入 PyFlipper
本地串口
flipper = py flipper(com = "/dev/tty ACM 0 ")
或
远程串口 2websocket 服务器
flipper = py flipper(ws = " ws://192 . 168 . 1 . 5:1337 ")**

## 力量

**Info
Info = flipper . power . Info()
power off
flipper . power . off()
重启
flipper.power.reboot()
以 DFU 模式重启
flipper . power . Reboot 2d fu()**

## 更新/备份

**从安装更新。fuf 文件
flipper . update . install(fuf _ file = "/ext/update . fuf ")
备份 Flipper 到。tar 文件
flipper . update . backup(dest _ tar _ file = "/ext/backup . tar ")
从备份中恢复 Flipper。tar 文件
flipper . update . restore(bak _ tar _ file = "/ext/backup . tar ")**

### 储存；储备

#### 文件系统信息

**获取存储文件系统信息
ext _ info = flipper . storage . info(fs = "/ext ")**

## 探险家

**Get the storage/ext dict
ext _ list = flipper . storage . list(path = "/ext ")
Get the storage/ext tree dict
ext _ tree = flipper . storage . tree(path = "/ext ")
Get file info
file _ info = flipper . storage . stat(file = "/ext/foo/bar . txt ")
Make directory
flipper . storage . mkdir(new _ dir = "/ext/foo ")**

## 文件

**读取文件
plain _ text = flipper . storage . Read(file = "/ext/foo/bar . txt ")
移除文件
flipper . storage . Remove(file = "/ext/foo/bar . txt ")
复制文件
flipper . storage . Copy(src = "/ext/foo/source . txt "，dest = "/ext/bar/destination . txt ")
重命名文件
flipper . storage . Rename(file = "/ext/foo/bar)
如果你要用 Lorem Ipsum 的一段话，
你需要确保文字中间没有藏着什么尴尬的东西。
" " " flipper . storage . Write . file(file，text)
使用监听器编写文件
file = "/ext/foo . txt "
text _ one = " "有许多不同版本的 Lorem Ipsum 段落可用，
但大多数都经历了某种形式的改变，通过注入幽默，
或随机单词，看起来甚至一点也不可信。如果你打算使用 Lorem Ipsum 的一段话，你需要确保文本中间没有隐藏任何令人尴尬的东西。
" " "
flipper . storage . write . start(file)
time . sleep(2)
flipper . storage . write . send(text _ one)
text _ two = " "互联网上所有的 Lorem Ipsum 生成器都倾向于在必要时重复预定义的组块
，这使得它成为互联网上第一个真正的生成器。
它使用超过 200 个拉丁单词的字典，结合少量的
示范句子结构，生成看起来合理的 Lorem Ipsum。因此，生成的 Lorem Ipsum 总是免于重复、注入的幽默或非特征的单词等。
" flipper . storage . write . send(text _ two)
time . sleep(3)
别忘了停
flipper . storage . write . stop()**

[**Download**](https://github.com/wh00hw/pyFlipper#explorer)