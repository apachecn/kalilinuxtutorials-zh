# NodeJsScan——node . js 应用程序的静态安全代码扫描器

> 原文：<https://kalilinuxtutorials.com/nodejsscan-static-security-code-scanner/>

NodeJsScan 是一个用于 Node.js 应用程序的静态安全代码扫描器(SAST)。

## **配置&运行** 

安装 Postgres 并在`core/settings.py`中配置`SQLALCHEMY_DATABASE_URI`

```
pip3 install -r requirements.txt
python3 migrate.py # Run once to create database entries required
python3 app.py # Testing Environment
gunicorn -b 0.0.0.0:9090 app:app --workers 3 --timeout 10000 # Production Environment
```

这将在`http://0.0.0.0:9090`运行

如果需要调试，在`core/settings.py`中设置`DEBUG = True`

**也读作 [渗透测试中的 osme deus——自动侦察和扫描](https://kalilinuxtutorials.com/osmedeus-penetration-testing/)**

## 节点扫描 CLI

命令行界面(CLI)允许您将其与 DevSecOps CI/CD 管道集成。结果是 JSON 格式的。当您使用 CLI 时，结果永远不会与它一起存储在后端。

```
virtualenv venv -p python3
source venv/bin/activate
(venv)pip install nodejsscan
(venv)$ nodejsscan
usage: nodejsscan [-h] [-f FILE [FILE ...]] [-d DIRECTORY [DIRECTORY ...]]
                  [-o OUTPUT] [-v]

optional arguments:
  -h, --help            show this help message and exit
  -f FILE [FILE ...], --file FILE [FILE ...]
                        Node.js file(s) to scan
  -d DIRECTORY [DIRECTORY ...], --directory DIRECTORY [DIRECTORY ...]
                        Node.js source code directory/directories to scan
  -o OUTPUT, --output OUTPUT
                        Output file to save JSON report
  -v, --version         Show nodejsscan version
```

### **Python API**

```
import core.scanner as njsscan
res_dir = njsscan.scan_dirs(['/Code/Node.Js-Security-Course'])
res_file = njsscan.scan_file(['/Code/Node.Js-Security-Course/deserialization.js'])
print(res_file)

[{'title': 'Deserialization Remote Code Injection', 'description': "User controlled data in 'unserialize()' or 'deserialize()' function can result in Object Injection or Remote Code Injection.", 'tag': 'rci', 'line': 11, 'lines': 'app.use(cookieParser())\n\napp.get(\'/\', function(req, res) {\n            if (req.cookies.profile) {\n                var str = new Buffer(req.cookies.profile, \'base64\').toString();\n                var obj = serialize.unserialize(str);\n                if (obj.username) {\n                    res.send("Hello " + escape(obj.username));\n                }\n            } else {', 'filename': 'deserialization.js', 'path': '/Users/ajin/Code/Node.Js-Security-Course/deserialization.js', 'sha2': '06f3f0ff3deed27aeb95955a17abc7722895d3538c14648af97789d8777cee50'}]
```

### **码头工人**

```
docker build -t nodejsscan .
docker run -it -p 9090:9090 nodejsscan
```

### **DockerHub**

```
**docker pull opensecurity/nodejsscan
docker run -it -p 9090:9090 opensecurity/nodejsscan:latest**
```

## **[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/ajinabraham/NodeJsScan)**

***你可以在 [Linkedin](https://www.linkedin.com/company/gbhackers/) 、 [Twitter](https://twitter.com/GbhackerOn) 、[脸书](https://www.facebook.com/gbhackersadmin)上关注我们的日常网络安全更新，你也可以在线参加[最佳网络安全课程](https://ethicalhackersacademy.com/)以保持自我更新。***