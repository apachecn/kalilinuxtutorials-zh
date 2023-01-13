# 用 Python 和 Jinja2 编写的钓鱼框架

> 原文：<https://kalilinuxtutorials.com/credsniper-phishing-framework/>

使用 CredSniper 轻松启动一个完全由 SSL 呈现的新网络钓鱼网站，并捕获凭据以及 2FA 令牌。API 提供了对当前捕获的凭证的安全访问，其他应用程序可以使用随机生成的 API 令牌来使用这些凭证。

 ***   通过“让我们加密”完全支持 SSL
*   真实网络钓鱼的精确登录形式克隆
*   任意数量的中间页面
    *   (即 Gmail 登录、密码和双因素页面，然后是重定向)
*   支持网络钓鱼 2FA 令牌
*   用于将凭证集成到其他应用程序中的 API
*   使用模板框架易于个性化

#### **也读作[Androl4b——安卓安全虚拟机](http://kalilinuxtutorials.com/androl4b-2/)**

## **基本用法**

用法:**cred sniper . py**[-h]–模块 MODULE[–two factor][–PORT PORT][–SSL][–verbose]–FINAL FINAL–HOSTNAME 主机名

```
optional arguments:
  -h, --help           show this help message and exit
  --module MODULE      phishing module name - for example, "gmail"
  --twofactor          enable two-factor phishing
  --port PORT          listening port (default: 80/443)
  --ssl                use SSL via Let's Encrypt
  --verbose            enable verbose output
  --final FINAL        final url the user is redirected to after phishing is done
  --hostname HOSTNAME  hostname for SSL 
```

### **国书**

**。缓存**:钓鱼 2FA 时临时存储用户名/密码

**。sniped** :捕获凭证和其他信息的平面文件存储

### **API 终点**

*   查看凭证(获取)`https://<phish site>/creds/view?api_token=<api token>`
*   将凭证标记为可见(获取)`https://<phish site>/creds/seen/<cred_id>?api_token=<api token>`
*   更新配置(后)`https://<phish site>/config`

```
 {
	   'enable_2fa': true,
	   'module': 'gmail',
	   'api_token': 'some-random-string'
	} 
```

### **模块**

通过将`--module <name>`命令传递给 CredSniper，可以加载所有模块。这些都是从`/modules`中的一个目录加载的。CredSniper 使用 [Python Flask](http://flask.pocoo.org/) 构建，所有模块 HTML 模板使用 [Jinja2](http://jinja.pocoo.org/docs/2.9/) 渲染。

*   **Gmail** :最新的 Gmail 登录被克隆和定制，以触发/钓鱼所有形式的 2FA
    1.  **modules/gmail/gmail.py** :加载主模块 w/–模块 gmail
    2.  **modules/Gmail/templates/Error . html**:404 错误页面
    3.  **模块/Gmail/模板/login.html** : Gmail 登录页面
    4.  **modules/Gmail/templates/Password . html**:Gmail 密码页面
    5.  **modules/Gmail/templates/Authenticator . html**:Google Authenticator 2FA 页面
    6.  **modules/Gmail/templates/SMS . html**:SMS 2FA 页面
    7.  **模块/Gmail/模板/触摸屏. html** :电话提示 2FA 页面

**GMAIL 更新:**谷歌在使用 U2F 时要求 2FA 的备份形式。通过强制一个回退选项而不是提示用户使用他们的 U2F 设备，可以绕过 U2F。如果短信可用，CredSniper 会尝试强制短信，否则会强制 TOTP。对于精通安全的受害者来说，如果提示他们输入短信或 TOTP 令牌而不是 U2F 设备，他们可能会感到厌倦。

*   **示例**:演示带有 2FA 令牌的标准网络钓鱼的示例模块
    1.  **modules/example/example . py**:主模块加载 w/–模块示例
    2.  **模块/示例/模板/login.html** :标准登录表单
    3.  **modules/example/templates/two factor . html**:标准 2FA 令牌形式

[![](img/a51de913dc60eee505c4a68651ee8e4d.png)](https://github.com/ustayready/CredSniper)**