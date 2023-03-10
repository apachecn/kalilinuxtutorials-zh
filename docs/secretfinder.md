# SecretFinder:基于 LinkFinder 的 Python 脚本

> 原文：<https://kalilinuxtutorials.com/secretfinder/>

[![SecretFinder : A Python Script Based On LinkFinder](img/455339d2f7c975f250a331ad407c24a1.png "SecretFinder : A Python Script Based On LinkFinder")](https://1.bp.blogspot.com/-eP2X7t83zhk/XwKhuYc3MdI/AAAAAAAAGyg/DjTTC2GmWTY-kWwFNUBI3Mt472xKtSEsQCLcBGAsYHQ/s1600/SecretFinder%25281%2529.png)

**SecretFinder** 是一个基于 [LinkFinder](https://github.com/GerbenJavado/LinkFinder) (此处为的 burpsuite [版本)的 python 脚本，用于发现 apikeys、accesstoken、authorizations、jwt、..JavaScript 文件中。](https://github.com/m4ll0k/BurpSuite-Secret_Finder)

它通过结合使用 jsbeautifier for python 和一个相当大的正则表达式来实现这一点。正则表达式由四个小正则表达式组成。它们负责查找和搜索 js 文件上的任何内容。

输出以 HTML 或明文的形式给出。

**帮助**

```
usage: SecretFinder.py [-h] [-e] -i INPUT [-o OUTPUT] [-r REGEX] [-b]
                       [-c COOKIE] [-g IGNORE] [-n ONLY] [-H HEADERS]
                       [-p PROXY]

optional arguments:
  -h, --help            show this help message and exit
  -e, --extract         Extract all javascript links located in a page and
                        process it
  -i INPUT, --input INPUT
                        Input a: URL, file or folder
  -o OUTPUT, --output OUTPUT
                        Where to save the file, including file name. Default:
                        output.html
  -r REGEX, --regex REGEX
                        RegEx for filtering purposes against found endpoint
                        (e.g: ^/api/)
  -b, --burp            Support burp exported file
  -c COOKIE, --cookie COOKIE
                        Add cookies for authenticated JS files
  -g IGNORE, --ignore IGNORE
                        Ignore js url, if it contain the provided string
                        (string;string2..)
  -n ONLY, --only ONLY  Process js url, if it contain the provided string
                        (string;string2..)
  -H HEADERS, --headers HEADERS
                        Set headers ("Name:Value\nName:Value")
  -p PROXY, --proxy PROXY
                        Set proxy (host:port) 
```

**安装**

它支持 Python 3。

**$ git 克隆 https://github.com/m4ll0k/SecretFinder.git secret finder
$ CD secret finder
$ python-m pip install-r requirements . txt 或 pip install-r requirements . txt $ python secret finder . py**

**又读-[针:即时访问你在各种平台上的 Bug 赏金提交仪表盘](https://kalilinuxtutorials.com/needle/)**

**用途**

*   在在线 JavaScript 文件中使用默认正则表达式查找敏感数据并将 HTML 结果输出到 results.html 的最基本用法:

**python 3 secret finder . py-I https://example.com/1.js-o results.html**

*   CLI/STDOUT 输出(不使用 jsbeautifier，这使得它非常快):

**python 3 secret finder . py-I https://example.com/1.js-o CLI**

*   分析整个域及其 JS 文件:

**python 3 secret finder . py-I https://example.com/-e**

*   忽略由`-g --ignore`提供的某些 js 文件(如外部库)

**python 3 secret finder . py-I https://example.com/-e-g ' jquery；自举；api.google.com'**

*   只处理`-n --only`提供的某个 js 文件:

**python 3 secret finder . py-I https://example.com/-e-n ' d 3 I 4 yxtzktqr 9n . cloudfront . net；www.myexternaljs.com'**

*   使用您的正则表达式:

**python 3 secret finder . py-I https://example.com/1.js-o CLI-r ' API key = my . API . key[a-zA-Z]+'**

*   其他选项:添加标题、代理和 cookies:

**python 3 secret finder . py-I https://example.com/-e-o CLI-c ' my ssionid = 111234 '-H ' x-header:value 1 \ NX-header 2:value 2 '-p 127 . 0 . 0 . 1:8080-r ' API key = my . API . key[a-zA-Z]+'**

*   输入接受所有这些条目:
*   Url:例如，[https://www.google.com/](https://www.google.com/)[-e]是必需的
*   Js 网址:例如[https://www.google.com/1.js](https://www.google.com/1.js)
*   文件夹:例如 myjsfiles/*
*   本地文件:例如/js/myjs/file.js

**添加正则表达式**

*   打开`SecretFinder.py`并添加您的正则表达式:

```
_regex = {
    'google_api'     : r'AIza[0-9A-Za-z-_]{35}',
    'google_captcha' : r'6L[0-9A-Za-z-_]{38}|^6[0-9a-zA-Z_-]{39}$',
    'google_oauth'   : r'ya29\.[0-9A-Za-z\-_]+',
    'amazon_aws_access_key_id' : r'AKIA[0-9A-Z]{16}',
    'amazon_mws_auth_toke' : r'amzn\\.mws\\.[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}',
    'amazon_aws_url' : r's3\.amazonaws.com[/]+|[a-zA-Z0-9_-]*\.s3\.amazonaws.com',
    'facebook_access_token' : r'EAACEdEose0cBA[0-9A-Za-z]+',
    'authorization_basic' : r'basic\s*[a-zA-Z0-9=:_\+\/-]+',
    'authorization_bearer' : r'bearer\s*[a-zA-Z0-9_\-\.=:_\+\/]+',
    'authorization_api' : r'api[key|\s*]+[a-zA-Z0-9_\-]+',
    'mailgun_api_key' : r'key-[0-9a-zA-Z]{32}',
    'twilio_api_key' : r'SK[0-9a-fA-F]{32}',
    'twilio_account_sid' : r'AC[a-zA-Z0-9_\-]{32}',
    'twilio_app_sid' : r'AP[a-zA-Z0-9_\-]{32}',
    'paypal_braintree_access_token' : r'access_token\$production\$[0-9a-z]{16}\$[0-9a-f]{32}',
    'square_oauth_secret' : r'sq0csp-[ 0-9A-Za-z\-_]{43}|sq0[a-z]{3}-[0-9A-Za-z\-_]{22,43}',
    'square_access_token' : r'sqOatp-[0-9A-Za-z\-_]{22}|EAAA[a-zA-Z0-9]{60}',
    'stripe_standard_api' : r'sk_live_[0-9a-zA-Z]{24}',
    'stripe_restricted_api' : r'rk_live_[0-9a-zA-Z]{24}',
    'github_access_token' : r'[a-zA-Z0-9_-]*:[a-zA-Z0-9_\-]+@github\.com*',
    'rsa_private_key' : r'-----BEGIN RSA PRIVATE KEY-----',
    'ssh_dsa_private_key' : r'-----BEGIN DSA PRIVATE KEY-----',
    'ssh_dc_private_key' : r'-----BEGIN EC PRIVATE KEY-----',
    'pgp_private_block' : r'-----BEGIN PGP PRIVATE KEY BLOCK-----',
    'json_web_token' : r'ey[A-Za-z0-9-_=]+\.[A-Za-z0-9-_=]+\.?[A-Za-z0-9-_.+/=]*$',

    'name_for_my_regex' : r'my_regex', 
    # for example
    'example_api_key'    : r'^example\w+{10,50}'
}
```

[**Download**](https://github.com/m4ll0k/SecretFinder)