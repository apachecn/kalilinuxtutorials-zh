# PhEmail 开源工具，自动发送钓鱼邮件

> 原文：<https://kalilinuxtutorials.com/phemail-sending-phishing-emails/>

PhEmail 是一个 python 开源钓鱼邮件工具，它将发送钓鱼邮件的方式机械化，作为社交设计测试的一个组成部分。其背后的主要动机是发送一包网络钓鱼邮件，并证明是谁利用了这些邮件，而不是试图滥用互联网浏览器或电子邮件客户，然而却收集了尽可能多的数据。

它伴随着一台电机通过 LinkedIN 收集电子邮件地址，在数据收集阶段很有帮助。同样，该工具支持 Gmail 身份验证，这是在目标区域抵制源电子邮件或 IP 地址的情况下的一个重要替代方案。最后，这个设备可以用来克隆公司登录网关，记住最终目标是获得登录认证。

**也可理解为[reel phish——一种实时双因素网络钓鱼工具](https://kalilinuxtutorials.com/reelphish-phishing-tool/)**

## **PhEmail 安装**

您可以通过克隆 GitHub 存储库来下载 PhEmail 的最新版本:

```
git clone https://github.com/Dionach/PhEmail
```

## **用法**

```
PHishing EMAIL tool v0.13
Usage: phemail.py [-e <emails>] [-m <mail_server>] [-f <from_address>] [-r <replay_address>] [-s <subject>] [-b <body>]
          -e    emails: File containing list of emails (Default: emails.txt)
          -f    from_address: Source email address displayed in FROM field of the email (Default: Name Surname <name_surname@example.com>)
          -r    reply_address: Actual email address used to send the emails in case that people reply to the email (Default: Name Surname <name_surname@example.com>)
          -s    subject: Subject of the email (Default: Newsletter)
          -b    body: Body of the email (Default: body.txt)
          -p    pages: Specifies number of results pages searched (Default: 10 pages)
          -v    verbose: Verbose Mode (Default: false)
          -l    layout: Send email with no embedded pictures 
          -B    BeEF: Add the hook for BeEF
          -m    mail_server: SMTP mail server to connect to
          -g    Google: Use a google account username:password
          -t    Time delay: Add deleay between each email (Default: 3 sec)
          -R    Bunch of emails per time (Default: 10 emails)
          -L    webserverLog: Customise the name of the webserver log file (Default: Date time in format "%d_%m_%Y_%H_%M")
          -S    Search: query on Google
          -d    domain: of email addresses
          -n    number: of emails per connection (Default: 10 emails)
          -c    clone: Clone a web page
          -w    website: where the phishing email link points to
          -o    save output in a file
          -F    Format (Default: 0): 
                0- firstname surname
                1- firstname.surname@example.com
                2- firstnamesurname@example.com
                3- f.surname@example.com
                4- firstname.s@example.com
                5- surname.firstname@example.com
                6- s.firstname@example.com
                7- surname.f@example.com
                8- surnamefirstname@example.com
                9- firstname_surname@example.com 

Examples: phemail.py -e emails.txt -f "Name Surname <name_surname@example.com>" -r "Name Surname <name_surname@example.com>" -s "Subject" -b body.txt
          phemail.py -S example -d example.com -F 1 -p 12
          phemail.py -c https://example.com 
```

## 免责声明 

未经双方事先同意，使用 PhEmail 攻击目标是非法的。最终用户有责任遵守所有适用的地方、州和联邦法律。开发人员不承担任何责任，也不对本程序造成的任何误用或损坏负责。

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/Dionach/PhEmail)