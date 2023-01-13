# KBD-Audio:捕捉和分析键盘输入的工具，配有麦克风捕捉功能

> 原文：<https://kalilinuxtutorials.com/kbd-audio-keyboard-microphone-capture/>

KBD-Audio 是用于捕获和分析音频数据的命令行和 GUI 工具的集合。最有趣的工具被称为**keytap**——它只能通过分析从计算机麦克风捕获的音频来猜测按下的键盘键。

## **KBD-音频安装**

```
git clone https://github.com/ggerganov/kbd-audio
cd kbd-audio
git submodule update --init
mkdir build && cd build
cmake ..
make
```

**也读作[NodeJsScan——node . js 应用的静态安全代码扫描器](https://kalilinuxtutorials.com/nodejsscan-static-security-code-scanner/)**

## **工具**

### **记录满**

将音频录制到磁盘上的原始二进制文件中

```
Usage:** ./record-full output.kbd
```

### **玩满了**

回放通过**记录完整**工具捕获的记录

```
Usage:** ./play-full input.kbd
```

### **记录**

仅在键入时录制音频。用于收集**按键**的训练数据

```
Usage:** ./record output.kbd
```

### **播放**

回放通过**记录**工具创建的记录

```
Usage:** ./play input.kbd
```

### **按键**

通过麦克风音频捕捉实时检测按键。使用通过**记录**工具获取的训练数据。

```
Usage:** ./keytap-gui input0.kbd [input1.kbd] [input2.kbd] ...
```

#### **演示**

> [查看 imgur.com 的帖子](https://imgur.com/mnRvT1X)