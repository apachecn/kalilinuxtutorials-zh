# SQL scanner——使用 Charles 和 SQLmap API 进行自动 SQL 注入

> 原文：<https://kalilinuxtutorials.com/sqliscanner-automatic-sql-injection/>

SQLiScanner 是一个自动 SQL 注入工具，带有 Charles 和 sqlmap api，支持 Linux 和 osx。以下是这个自动注入工具的依赖项。

*   姜戈
*   一种数据库系统
*   芹菜
*   sqlcmap
*   雷迪斯

**又读:**[dawn Scanner——静态分析安全扫描器](https://kalilinuxtutorials.com/dawnscanner-security-scanner/)

### SQL scanner**安装**

如果您可以通过克隆 Git 存储库来下载它，这总是最好的:

**git 克隆 https://github.com/0xbug/SQLiScanner.git–深度 1**

用户还可以选择通过克隆 Git 存储库来下载 sqlmap:

**git 克隆 https://github.com/sqlmapproject/sqlmap.git–深度 1**

它可以在 Linux 和 osx 上使用 Python 版。

创建 virtualenv 并安装要求

**CD SQL scanner/
virtualenv–python =/usr/local/bin/python 3.5 venv
source venv/bin/activate
pip install-r requirements . txt**

### **设置**

对于这个工具，我们主要有两个设置，如数据库和发送电子邮件设置，下面我们提到了如何配置这两个设置。

**数据库设置**

**SQL scanner/settings . py:85
DATABASES = {
'默认':{
'引擎':' django.db.backends.postgresql '，
'名称': "，
'用户': "，
'密码': "，
'主机':' 127.0.0.1 '，
'端口':' 5432 '，
}
}**

**发送电子邮件设置**

**SQL scanner/settings . py:158**

**# Email
Email _ back end = ' django . core . mail . backends . SMTP . Email back end '
Email _ USE _ TLS = False
Email _ HOST = "
Email _ PORT = 25
Email _ HOST _ USER = "
Email _ HOST _ PASSWORD = "
DEFAULT _ FROM _ Email = "**

**scanner/tasks.py:14**

**类 SqlScanTask(object):
def init(self，sqli _ obj):
self . API _ URL = " http://127 . 0 . 0 . 1:8775 "
self . mail _ from = " "
self . mail _ to =[" "]**

### **Syncdb**

**python manage . py make migrations 扫描器
python manage.py migrate**

### **创建超级用户**

**python manage.py 创建超级用户**

### **运行**

一旦你按照上面提到的进行了设置和配置，你可以运行下面的命令来确保一切都是正确的，并开始使用它。

redis-server
python sqlmapapi . py-s-p 8775
python manage . py celery worker–log level = info
python manage . py runserver

[**Download**](https://github.com/0xbug/SQLiScanner)