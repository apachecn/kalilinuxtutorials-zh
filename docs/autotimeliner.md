# 自动时间线:从易失性内存转储中自动提取取证时间线

> 原文：<https://kalilinuxtutorials.com/autotimeliner/>

[![](img/e455008a73ce3002e82732f7ab563e2e.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgm7fBSxQZj93eiSAn6gpZEriOVqFlNC28NrVTahqDIi6De-Tkpl3VHywgIhmvpcnuG_tJRyAyDvNgTqfcsup8WR1u4r2dDMiKTo8qYG6yFy9Vq-6djAuYy76O0de4YHNLtufDN-DiRORKW6y9n0UC8_NeloUfqqVxu1WVmIN50oaxcLlUWTuG1vmiP/s728/patch-tuesday-2022.png)

**自动时间线**工具将从易失性内存转储中自动提取取证时间线。

## 要求

*   python3
*   波动性
*   mactime(来自 SleuthKit)

(在 Debian 9.6 上用 **Volatility 2.6-1** 和 **sleuthkit 4.4.0-5** 开发和测试)

## 它是如何工作的

AutoTimeline 自动执行此工作流程:

*   为内存映像确定正确的易失性配置文件。
*   使用易失性运行针对易失性内存转储的 **timeliner** 插件。
*   运行 **mftparser** volatility 插件，以便从内存中提取$MFT 并生成一个 bodyfile。
*   运行 **shellbags** volatility 插件，以生成用户活动的主体文件。(马泰奥·坎通尼建议)。
*   将 **timeliner** 、 **mftparser** 和 **shellbags** 输出文件合并成一个 bodyfile。
*   使用 **mactime** 对主体文件进行分类和过滤，并将数据导出为 CSV 格式。

## 安装

简单地克隆 GitHub 库:

`**git clone https://github.com/andreafortuna/autotimeliner.git**`

## 用法

**auto timeline . py[-h]-f image file[-t time frame][-p custom profile]
可选参数:
-h，–help 显示此帮助消息并退出
-f IMAGEFILE，–image file image file
内存转储文件
-t TIMEFRAME，–time frame time frame
用于过滤时间线的时间范围(YYYY-MM-DD
..YYYY-MM-DD)
-p CUSTOMPROFILE，–custom profile custom profile
跳转图像识别并使用自定义内存
profile**

### 例子

从 *TargetServerMemory.raw* 中提取时间线，限于从 **2018-10-17** 到 **2018-10-21** 的时间范围:

`**./autotimeline.py -f TargetServerMemory.raw -t 2018-10-17..2018-10-21**`

从当前目录中的所有图像中提取时间线，时间范围限于 2018-10-17 到 2018-10-21:

`**./autotimeline.py -f ./*.raw -t 2018-10-17..2018-10-21**`

使用自定义内存配置文件从 *TargetServerMemory.raw* 中提取时间轴:

`**./autotimeline.py -f TargetServerMemory.raw -p Win2008R2SP1x64**`

所有时间线将保存为**$ original filename-timeline . CSV**。

[**Download**](https://github.com/andreafortuna/autotimeliner)