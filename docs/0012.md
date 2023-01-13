# Hack Windows Installer For Hack 字样

> 原文：<https://kalilinuxtutorials.com/hack-windows-installer/>

## **黑掉 Windows Installer**

Hack 字体的 Windows 安装程序。

虽然利用 windows 安装程序来安装字体看起来毫无意义，但在 Windows 平台上这背后有合理的解释。当人们试图手动安装或更新不时更新的字体时，各种事情都会变得很糟糕。

该安装程序倾向于解决大部分常见问题。

## **黑客 Windows Installer 的使用**

*   从 [下载`HackFontsWindowsInstaller.exe`发布](https://github.com/source-foundry/Hack-windows-installer/releases/latest)
*   双击`HackFontsWindowsInstaller.exe`
*   如果您看到“Windows 保护您的电脑”消息，请点击“更多信息”并选择“仍然运行”。这个 Windows SmartScreen 警告可以被安全地忽略，安装程序没有病毒和附加软件。
*   遵循安装说明
*   如果安装或删除了字体文件，安装程序将要求重新启动

## **安装程序来源**

你可以在[hackwindowsinstaller . ISS中查看安装程序源代码的注释。](https://github.com/source-foundry/Hack-windows-installer/blob/master/src/HackWindowsInstaller.iss)

要自己构建这个设置，请下载 Inno Setup 的最新 ANSI(非 Unicode)版本。安装它并启动安装 Inno Setup 预处理器的选项。双击 HackWindowsInstall.iss，这将在 Inno Setup 中堆叠它，并选择 Build–Compile。

我们发布带有 SHA256 哈希进程的聚合安装程序，VirusTotal malware 检查发布中的报告链接。

## **安静安装**

要安装它，请使用附带的命令:

`start /wait HackFontsWindowsInstaller.exe /VERYSILENT /SUPPRESSMSGBOXES /NORESTART /CLOSEAPPLICATIONS /NORESTARTAPPLICATIONS`

要删除它:

`C:\Program Files\Hack Fonts\unins000.exe /VERYSILENT /SUPPRESSMSGBOXES /NORESTART`

## 解决纷争

安装程序在途中生成一个日志文件`C:\Users\ (Username) \AppData\Local\Temp\Setup Log (Year-Month-Day) #XXX.txt`，其中包含全部信息，而`C:\Program Files\Hack Fonts\Log-FontData.txt;.`后者只包含前者的一个子集。

如果你使用的是 EMET:如果“只信任字体”选项被激活，你需要声明 Hack 是可信的，否则它将不可用。

[![](img/a51de913dc60eee505c4a68651ee8e4d.png)](https://github.com/source-foundry/Hack-windows-installer)