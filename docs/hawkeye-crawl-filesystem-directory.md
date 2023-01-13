# 鹰眼——抓取文件系统或目录的工具

> 原文：<https://kalilinuxtutorials.com/hawkeye-crawl-filesystem-directory/>

HawkEye 是一个简单的工具，可以抓取文件系统或目录，寻找有趣的东西，如 SSH 密钥、日志文件、Sqlite 数据库、密码文件等。Hawkeye 使用一个快速的文件系统爬行器递归地浏览文件，然后发送它们进行实时分析，并以 json 格式和简单的控制台输出来呈现数据。该工具采用模块化方法构建，易于使用和扩展。

在 pentests 期间，它可以用作权限提升工具来查看文件系统，找到有时由系统管理员留下的配置文件或 ssh 密钥。

# **特性**

1.  简单和模块化的代码基础使其易于贡献。
2.  快速和强大的目录爬行模块做实时分析
3.  易于扩展的大型扫描仪(感谢 Gitrob)
4.  各种格式的输出

**也读作 [使用 Cymothoa 维护对 Linux 机器的访问——后期利用](https://kalilinuxtutorials.com/cymothoa/)**

# **安装说明**

安装很容易。Git 克隆 repo 并运行 go build。

```
go get github.com/Ice3man543/hawkeye
```

## **升级**

如果您希望升级软件包，您可以使用:

```
go get -u github.com/Ice3man543/hawkeye
```

## **鹰眼用法**

鹰眼首先需要一个目录。目录可以提供有`-d`标志。例如–

```
./hawkeye -d <directory>
```

为了对我的主目录运行它，我可以传递/home/ice3man 作为参数。

```
./hawkeye -d /home/ice3man

 ✘ ice3man@TheDaemon ** ~/tmp  ./hawkeye -d /home/ice3man 
 _  _                _    ___           
| || | __ _ __ __ __| |__| __|_  _  ___ 
| __ |/ _  |\ V  V /| / /| _|| || |/ -_)
|_||_|\__,_| \_/\_/ |_\_\|___|\_, |\___|
                              |__/     
	    Analysis v1.0 - by @Ice3man

[13:31:59] HawkEye : An advance filesystem analysis tool
[13:31:59] Written By : @Ice3man
[13:31:59] Github : https://github.com/Ice3man543

[Log file] /home/ice3man/.tplmap/tplmap.log
[Log file] /home/ice3man/burpsuite-master/hs_err_pid3028.log
[Log file] /home/ice3man/.log/jack/jackdbus.log
[Shell command history file] /home/ice3man/oldvps/root/.bash_history
[Shell configuration file] /home/ice3man/oldvps/root/.bashrc 
```

**你可以使用`-v`标志来显示详细的输出。还可以使用`-o`标志获得 json 输出。**

```
[
    {
        "path": "/home/ice3man/oldvps/root/.bash_history",
        "description": "Shell command history file",
        "comment": ""
    },
    {
        "path": "/home/ice3man/oldvps/root/.profile",
        "description": "Shell profile configuration file",
        "comment": "Shell configuration files can contain passwords, API keys, hostnames and other goodies"
    },
    {
        "path": "/home/ice3man/oldvps/root/.bashrc",
        "description": "Shell configuration file",
        "comment": "Shell configuration files can contain passwords, API keys, hostnames and other goodies"
    },
]
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/Ice3man543/hawkeye)