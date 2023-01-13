# WinPirate:从可启动 USB 自动破解粘滞键

> 原文：<https://kalilinuxtutorials.com/winpirate-automated-hack-bootable-usb/>

自动化粘滞键破解。攻击后，它会获取浏览器密码、历史记录和网络密码。计划是这样的。我们创造了一种从可启动的 USB 自动执行粘滞键 windows hack 的方法，我们称之为 WinPirate。然后，我们自动获取尽可能多的保存密码，删除一个监听器，并删除所有我们在那里的痕迹。

所有这些都没有被反病毒软件检测到。如果发现计算机正在运行且未锁定，我们应该添加一个 mimikittenz 选项，否则我们可以稍后远程运行它。

#### **也读作 [恶意 app 改名回谷歌 Play 商店](http://kalilinuxtutorials.com/malicious-apps-google-play-store/)**

## **如何使用 WinPirate**

**需求**:一个 linux 可引导 USB，这个 repo 在 USB 上(不在 OS 里，只是放在根目录下)

注意:chromepasswords.py 需要 PyWin32

**如果电脑被锁定:**

*   关闭窗口(确保按住 shift 键的同时不要休眠)
*   点击 F12 并选择 USB
*   `sudo -i`
*   `fdisk -l`(注意:如果你在 Kali Linux 上，运行`parted -l`)
*   `mkdir /media/windows`
*   `mount /dev/WHATEVERTHEWINDOWSPARTITIONWASCALLED /media/windows -t ntfs`
*   运行 Stickykeys.sh
*   重新启动并引导至 Windows
*   快速按 Shift 5 次，会出现一个命令提示
*   cd 到 USB 并运行 WinPirate.bat

**如果电脑没有锁定:**

cd 到 USB 并运行 Run.bat(这将在后台静默运行 WinPirate.bat，它应该在 10 秒内完成

## **本期**

1.  我做的 chrome 密码抓取器仍然是一个. py 文件，我需要把它转换成 exe 文件，这样就不需要在系统上安装 python 了。
    你可以用`python chromepasswords.py -csv`运行它，它会解密 Chrome 保存的密码数据库并导出为 CSV 格式
2.  从冗长的“如何使用”一节可以明显看出，粘滞键自动化并没有像我之前认为的那样加速这个过程
3.  我还没能写出任何为 IE 或 Firefox 抓取密码的工具

[![](img/a51de913dc60eee505c4a68651ee8e4d.png)](https://github.com/thepaulbenoit/WinPirate)