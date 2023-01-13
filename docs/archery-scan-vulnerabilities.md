# 射箭——开源漏洞评估和管理帮助开发人员和测试人员执行扫描和管理漏洞

> 原文：<https://kalilinuxtutorials.com/archery-scan-vulnerabilities/>

射箭是一个开源的漏洞评估和管理工具，帮助开发人员和测试人员执行扫描和管理漏洞。它使用流行的开源工具对 web 应用程序和网络进行全面扫描。

## **射箭要求**

1.  Python 2.7
2.  OpenVas 8，9
3.  OWASP ZAP 2.7.0
4.  Selenium Python Firefox Web 驱动程序

## **启动应用程序**

```
$ python manage.py runserver 0.0.0.0:8000
```

## **安装**

```
$ git clone https://github.com/archerysec/archerysec.git
$ cd archerysec
$ chmod +x install.sh
$ sudo ./install.sh
```

**也读[BootStomp——一个 Bootloader 漏洞 Bug 发现者](https://kalilinuxtutorials.com/bootstomp-vulnerability-bug-finder/)**

## **手动安装**

```
$ git clone https://github.com/archerysec/archerysec.git
$ cd archerysec
$ pip install -r requirements.txt
$ python manage.py collectstatic
$ python manage.py makemigrations networkscanners
$ python manage.py makemigrations webscanners
$ python manage.py makemigrations projects
$ python manage.py makemigrations APIScan
$ python manage.py makemigrations osintscan
$ python manage.py makemigrations jiraticketing
$ python manage.py makemigrations tools
$ python manage.py makemigrations archerysettings
$ python manage.py migrate
$ python manage.py createsuperuser
$ python manage.py runserver
```

**注意:**确保这些步骤应该在每次 git 拉取之后执行。

## **码头工人安装**

```
$ docker pull archerysec/archerysec
$ docker run -it -p 8000:8000 archerysec/archerysec:latest

# For persistence
```

## **设定设置**

#### **ZAP 运行守护模式**

找到您的 ZAP 启动脚本，并使用下面详述的选项执行它。

**视窗:**

```
zap.bat -daemon -host 0.0.0.0 -port 8080 -config api.disablekey=true -config api.addrs.addr.name=.* -config api.addrs.addr.regex=true
```

**其他:**

```
zap.sh -daemon -host 0.0.0.0 -port 8080 -config** **api.disablekey=true -config api.addrs.addr.name=.* -config api.addrs.addr.regex=true
```

### **Zap 设置**

*   转到设置页面
*   编辑 ZAP 设置或导航 URL:[http://host:port/web scanners/setting _ edit/](http://host:port/webscanners/setting_edit/)
*   填写以下所需信息。
    **Zap API 密钥:**如果您使用 Zap 作为守护进程，请留空**`api.disablekey=true`**
    **Zap API 主机:**您的 Zap API 主机 ip 或系统 IP Ex。`**127.0.0.1**`或`**192.168.0.2**`
    **Zap API 端口:** ZAP 运行端口 Ex。 **`8080`**

### **OpenVAS 设置**

*   转到设置页面
*   编辑 OpenVAS 设置或导航 URL:[http://host:port/network scanners/open vas _ setting](http://host:port/networkscanners/openvas_setting)
*   填写所有必需的信息，然后单击保存。

### **路线图**

*   扫描仪解析器和插件
    *   nesus(XML)
    *   Webinspect (XML)
    *   Acunetix (XML)
    *   应用程序扫描(XML)
    *   Netsparker (XML)
    *   AppSpider
*   流行工具插件支持
    *   Nmap
    *   SSL 分析
    *   Nikto
    *   WPScan
    *   OWASP JoomScan
*   报告
    *   便携文档格式
    *   Docx
    *   可扩展标记语言
    *   擅长
    *   JSON
*   API 自动漏洞扫描。
*   漏洞 poco 图片
*   云安全扫描。
*   源代码评审项目管理？
*   设防插件
*   复选标记？….

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/archerysec/archerysec)