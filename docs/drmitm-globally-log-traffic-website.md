# DrMITM:一个设计用来记录网站所有流量的程序

> 原文：<https://kalilinuxtutorials.com/drmitm-globally-log-traffic-website/>

[![DrMITM : A Program Designed To Globally Log All Traffic Of A Website](img/5648e0af7934e76f345c9f277a08a99d.png "DrMITM : A Program Designed To Globally Log All Traffic Of A Website")](https://1.bp.blogspot.com/-9o0Jv43zWjY/XVVRNAt0pTI/AAAAAAAAB8E/9A7Vd-Gyz4Mxl2IMAbI3ElUSicfOx8i9QCLcBGAs/s1600/Image-1.png)

DrMITM 是一个设计用来记录所有流量的程序。它向网站发送请求，并返回网站的 IP，以防网站的服务器被设计为依赖网站 IP 进行请求。

发送到网站的请求也最终被发送到服务器，它将记录网站发送的消息，然后它将返回相同的消息并将其直接发送到服务器，服务器可能会将其视为网站，但一旦程序更改 IP，它也会将我们的请求定向到网站。

一旦它将我们的请求发送到网站，该程序就会暂停我们的流量，并等待传入的流量，当一个新用户试图登录或任何网站向服务器发送请求时，DrMITM 将接收它，它将数据返回给我们的方式是将相同的数据发送到一个文件。

**也可阅读-[ThreatHunting:一款映射到米特 ATT&CK](https://kalilinuxtutorials.com/threathunting-splunk-mitre-attck/)的 Splunk 应用**

**如何入门？**

*   对于 Nim 版本:安装 19.0 Nim(使用 choosenim 或 git clone) Git 将 repo cd 克隆到目录中运行 nim DrMITM.nim
*   对于 Python 版本:安装 Python git 将 repo cd 克隆到目录中运行 python DrMITM.py

 ***   e(实时记录)
*   b(交通阻塞)
*   r(重定向用户)

**即将推出的功能**

– **-ᴘʀᴇᴠᴇɴᴛɪɴɢ ᴄʟɪᴇɴᴛ ᴛʀᴀғғɪᴄ ғʀᴏᴍ ʀᴇᴀᴄʜɪɴɢ ᴛʜᴇ sᴇʀᴠᴇʀ.–(ɴᴏᴡ ᴀᴠᴀɪʟᴀʙʟᴇ)
–ʀᴇᴅɪʀᴇᴄᴛɪɴɢ ᴛʀᴀғғɪᴄ–(ɴᴏᴡ ᴀᴠᴀɪʟᴀʙʟᴇ)**

**ᴛʜᴇᴏʀᴇᴛɪᴄᴀʟ ᴄᴏɴ**

ᴛʜᴇʀᴇ ᴍᴀʏ ʙᴇ ᴀ ᴘᴏssɪʙɪʟɪᴛʏ ᴛʜᴀᴛ ᴅʀᴍɪᴛᴍ ᴡɪʟʟ ғᴀɪʟ ᴀᴛ sɴɪғғɪɴɢ ᴛʀᴀғғɪᴄ ᴏғ ᴡᴇʙsɪᴛᴇs ᴛʜᴀᴛ ᴄᴏᴍᴍᴜɴɪᴄᴀᴛᴇ ᴛʜʀᴏᴜɢʜ ᴍᴜʟᴛɪᴘʟᴇ sᴇʀᴠᴇʀs ʙᴇᴄᴀᴜsᴇ ᴏғ ᴄᴏɴғɪɢᴜʀᴀᴛɪᴏɴ ʀᴇᴀsᴏɴs ᴏʀ ᴘᴏssɪʙʟʏ ᴀ ᴄʜᴀɴɢᴇ ᴏғ ᴇɴᴄʀʏᴘᴛɪᴏɴ ᴏʀ ʀᴇǫᴜɪʀᴇᴍᴇɴᴛs ᴏғ ɴᴇᴇᴅɪɴɢ ᴛᴏ ᴛʀɪᴄᴋ ᴛʜᴇ sᴇʀᴠᴇʀ. ᴀɴᴅ ɪ sᴀʏ “ᴛʜᴇʀᴇ ᴍᴀʏ” ʙᴇᴄᴀᴜsᴇ ɪᴛ ʜᴀsɴ’ᴛ ʙᴇᴇɴ ᴛᴇsᴛᴇᴅ ʏᴇᴛ.

**问题报告**

如果您有问题，请提交并提供以下详细信息:

**你的问题
你的 Nim 或 Python 版本
操作系统**

问题发生前您正在做的事情的过程

问&答:

问:实时日志是如何工作的？答:它只是将记录的数据发送到一个文件中，并在屏幕上输出。
问:交通阻塞是如何工作的？答:unicode 从服务器发送到网站，并使流量向传入流量溢出。
问:如何重定向？专题作品？
答:它从修改了位置的服务器发送一个假的错误消息+重定向状态码。

[**Download**](https://github.com/Imgp3Dev/DrMITM)**