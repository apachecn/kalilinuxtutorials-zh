# win pirate–自动粘滞键破解

> 原文：<https://kalilinuxtutorials.com/winpirate-automated-sticky-keys-hack/>

我们创造了一种从可引导 USB 自动破解窗口粘滞键的方法。然后，我们自动获取尽可能多的保存的密码，删除一个监听器，并删除我们在那里的所有痕迹..如果发现计算机正在运行且未锁定，我们应该添加一个 mimikittenz 选项，否则我们可以稍后远程运行它

## **如何用粘滞键黑掉** 

**需求:**一个 linux 可引导的 USB，这个 repo 在 USB 上(不在 OS 中，只是放在根目录下)

#### **也读[DVIA——该死的易受攻击的 iOS 应用](http://kalilinuxtutorials.com/dvia-damn-vulnerable/)**

*   关闭窗口(确保按住 shift 键的同时不要休眠)
*   点击 F12 并选择 USB
*   `**sudo -i**`
*   **`fdisk -l`** (注意:如果你在 Kali Linux 上，运行`parted -l`)
*   `**mkdir /media/windows**`
*   **T2`mount /dev/WHATEVERTHEWINDOWSPARTITIONWASCALLED /media/windows -t ntfs`**
*   运行 Stickykeys.sh
*   重新启动并引导至 Windows
*   快速按 Shift 5 次，会出现一个命令提示
*   cd 到 USB 并运行 WinPirate.bat

**如果计算机没有锁定:**然后 cd 到 USB 并运行 Run.bat(这将在后台静默运行 WinPirate.bat，它应该在< 10 秒内完成

## **本期**

*   我做的 chrome 密码抓取器仍然是一个. py 文件，我需要把它转换成 exe 文件，这样就不需要在系统上安装 python 了。
    你可以用`python chromepasswords.py -csv`运行它，它会解密 Chrome 保存的密码数据库并导出为 CSV 格式
*   从冗长的“如何使用”一节可以明显看出，粘滞键自动化并没有像我之前认为的那样加速这个过程
*   我还没能写出任何为 IE 或 Firefox 抓取密码的工具

[![](img/a51de913dc60eee505c4a68651ee8e4d.png)](https://github.com/thepaulbenoit/WinPirate)