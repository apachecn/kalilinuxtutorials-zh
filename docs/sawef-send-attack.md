# SAWEF–发送攻击 Web 表单

> 原文：<https://kalilinuxtutorials.com/sawef-send-attack/>

这个 SAWEF 工具背后的动机是为任何使用 HTTP 的个人提供一个瑞士武装部队，到目前为止，她是必不可少的，带来了需要她拥有的少数功能中的一部分，无论如何，我们已经能够在这个设备上找到:

*   网站中的电子邮件爬虫
*   页面上的爬网程序表单
*   网页上的爬虫链接
*   发送 POST 并获取
*   支持用户代理
*   对线程的支持
*   对 COOKIES 的支持

**也读作[Gcat——潜回后门利用 Gmail 作为命令&控制服务器](https://kalilinuxtutorials.com/gcat-gmail-command-control-server/)**

## **R 要求 s 为 SAWEF**

#### **导入:**

*   穿线
*   时间
*   抱怨吗
*   要求
*   json
*   关于
*   美丽的声音

**权限:**阅读&写作
用户: root 权限，或者是在 sudoers 组
**操作系统:**LINUX
**Python:**2.7

## **一世 **杀头**** 

##### **`git clone http://github.com/danilovazb/SAWEF`**

sudo apt-get 安装 python-bs4 python-请求

##### **``**

 `### **帮助**

```
usage: tool [-h] --url http://url.com/
            [--user_agent '{"User-agent": "Mozilla/5.0 Windows; U; Windows NT 5.1; hu-HU; rv:1.7.8 Gecko/20050511 Firefox/1.0.4"}"]
            [--threads 10] [--data '{"data":"value", "data1":"value"}']
            [--qtd 5] [--method post|get]
            [--referer '{"referer": "http://url.com"}']
            [--response status_code|headers|encoding|html|form|links|emails]
            [--cookies '{"__utmz":"176859643.1432554849.1.1.utmcsr=direct|utmccn=direct|utmcmd=none"}']
            [--modulo crawler]

optional arguments:
  -h, --help        show this help message and exit
  --url http://url.com/
                    URL to request
  --user_agent '{"User-agent": "Mozilla/5.0 (Windows; U; Windows NT 5.1; hu-HU; rv:1.7.8) Gecko/20050511 Firefox/1.0.4"}"
                    For a longer list, visit:
                    http://www.useragentstring.com/pages/useragentstring.php
  --threads 10      Threads
  --data '{"data":"value", "data1":"value"}'
                    Data to be transmitted by post
  --qtd 5           Quantity requests
  --method post|get
                    Method sends requests
  --referer '{"referer": "http://url.com"}'
                    Referer
  --response status_code|headers|encoding|html|form|links|emails
                    Status return
  --cookies '{"__utmz":"176859643.1432554849.1.1.utmcsr=(direct)|utmccn=(direct)|utmcmd=(none)"}'
                    Cookies from site
  --modulo crawler  Carrega modulo adcional
```

### **例如**

```
*Send 1 SMS anonymous to POST [in BR]:
-------------
$:> python sawef.py --url "https://smsgenial.com.br/forms_teste/enviar.php" --data '{"celular":"(11) XXXX-XXXXX","mensagem":"Teste","Testar":"Enviar"}' --threads 10 --qtd 1 --user_agent '{"User-agent":"Mozilla/5.0 Windows; U; Windows NT 5.1; hu-HU; rv:1.7.8) Gecko/20050511 Firefox/1.0.4"}'

*List Form attributes:
-------------
$:> python sawef.py --url "https://smsgenial.com.br/" --method post --response form
OUTPUT:

--------------------------------
NOME_FORM[None]
URL[http://paineldeenvios.com/painel/app/login/login.php]
METHOD[post]

email:Digite Seu Login        (text)
passwd:Senha        (password)
Entrar:Entrar        (submit)

--------------------------------
NOME_FORM[form1]
URL[/forms_teste/criaruser.php]
METHOD[post]

action:criarconta        (hidden)
nome:<NONE>        (text)
celular:<NONE>        (text)
email:<NONE>        (text)
Testar:Criar        (submit)
Testar:Enviar        (hidden)

--------------------------------
NOME_FORM[None]
URL[/forms_teste/enviar.php]
METHOD[post]

celular:<NONE>        (text)
Testar:Enviar        (submit)

* Get email web pages
$:> python sawef.py --url "http://pastebin.com/ajaYnLYc" --response emails
[...]
[+] EMAIL = manothradevi@yahoo.com
[+] EMAIL = fantaghiroaziera@yahoo.com
[+] EMAIL = naqibjohari@yahoo.com
[+] EMAIL = azliey3036@yahoo.com
[+] EMAIL = azlin_4531@yahoo.com.my
[+] EMAIL = urshawal96@yahoo.com
[+] EMAIL = weeta_aida88@yahoo.com.my
FOUND = 3065

* Get links on web pages
$:> python sawef.py --url "http://terra.com.br" --response links
[...]
[+] LINK = http://uol.com.br/https://pagseguro.uol.com.br/vender
[+] LINK = http://www.uolhost.com.br/registro-de-dominio.html
[+] LINK = http://noticias.uol.com.br/arquivohome/
[+] LINK = http://noticias.uol.com.br/erratas/
[+] LINK = http://uol.com.br/#
[+] FOUND = 360

* Crawling site

$:> python sawef.py --url "http://www.100security.com.br" --modulo "crawler"
Emails: 

[+] marcos@aulasdeti.com.br
[+] marcos@100security.com.br
[+] danilovazb@gmail.com
[+] cve@mitre.org
[+] cve-id-change@mitre.org
[+] devon@digitalsanctuary.com
[+] g5382139@trbvm.com
[+] editor@www.com
[+] support@senderbase.org
[+] 0x0ptim0us@gmail.com
[+] ramiro.caire@gmail.com
[+] fgmassa@vanguardsec.com
[+] crime.internet@dpf.gov.br
[+] cgpre@dpf.gov.br
[+] dpat.dcor@dpf.gov.br
[+] dicof.cgcsp@dpf.gov.br
[+] coain.coger@dpf.gov.br
[+] dprev.cgpfaz@dpf.gov.br
[+] dicat@pcdf.df.gov.br
[+] nureccel@pc.es.gov.br
[+] devir@pc.ms.gov.br
[+] comunicacao@policiacivil.pa.gov.br
[+] cibercrimes@pc.pr.gov.br
[+] policiac@fisepe.pe.gov.br
[+] drci@policiacivil.rj.gov.br
[+] drci@pcerj.rj.gov.br
[+] drci@pc.rs.gov.br
[+] 4dp.dig.deic@policiacivil.sp.gov.br
[+] marcos@marcoshenrique.com
[+] contato@fabricadeaplicativos.com.br
[+] email@mail.com.br
[+] lcm@lcm.com.br
[+] luizwt at gmail.com
[+] luizwt@gmail.com
[+] geoff@deconcept.com
[+] revista@espiritolivre.org
[+] email@email.com
[+] s**********s@gmail.com
[+] //iriok@hotmail.com

Twitter:
[+] https://twitter.com/100security

Linkedin:

Google Plus:

Facebook:
[+] https://www.facebook.com/seguranca.da.informacao

Youtube:
[+] http://www.youtube.com/user/videos100security/videos
```

### **截图**
![](img/46a11ff784143478b216035ae5ca953e.png)

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/danilovazb/sawef#install)`