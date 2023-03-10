# 域入口–滥用安全轨道域的工具

> 原文：<https://kalilinuxtutorials.com/domaindouche/>

[![](img/ddd34ea5d8fe1d7c05cd465a84866a1e.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhXJHhSzYlSBttmPdhfY1uqyJ0q7yTlTjufrumvyFUdvO8VOwz3tKO9lJp6yXIZmMhTyK1KEQWkONLPGKM8KnelmRTbTiJhGF7mEDXoV3XEe8RDSOA5_yQZ7uLK-zGF6NiPyPiFamKT5YkaJHu10zUc8YSvMOT4vr6vecDPQ0BLdaucTUg3W5t8aakg/s728/DomainDouche.gif)

**DomainDouche** 是一个滥用 securitytrails 域建议 API，通过关键字和暴力寻找潜在相关的域。

## 演示

![](img/e085ecfef67218ffe213a2be07e9fd4c.png)

## **用途**

```
usage: domaindouche.py [-h] [-n N] -c COOKIE -a USER_AGENT [-w NUM] [-o OUTFILE] keyword

Abuses SecurityTrails API to find related domains by keyword.
Go to https://securitytrails.com/dns-trails, solve any CAPTCHA you might encounter,
copy the raw value of your Cookie and User-Agent headers and use them with the -c and -a arguments.

positional arguments:
  keyword               keyword to append brute force string to

options:
  -h, --help            show this help message and exit
  -n N, --num N         number of characters to brute force (default: 2)
  -c COOKIE, --cookie COOKIE
                        raw cookie string
  -a USER_AGENT, --useragent USER_AGENT
                        user-agent string (must match the browser where the cookies are from)
  -w NUM, --workers NUM
                        number of workers (default: 5)
  -o OUTFILE, --output OUTFILE
                        output file path
```

[Click Here To Download](https://github.com/n0kovo/DomainDouche)