# nova hot——渗透测试人员的 Webshell 框架

> 原文：<https://kalilinuxtutorials.com/novahot-penetration-testers/>

Novahot 是一个面向渗透测试人员的 webshell 框架。它实现了一个基于 JSON 的 API，可以与任何语言编写的木马进行通信。默认情况下，它附带了用 PHP、ruby 和 python 编写的特洛伊木马。

除了执行系统命令，novahot 还能够模拟交互式终端，包括 mysql、sqlite3 和 psql。此外，它还实现了“虚拟命令”,可以使用您喜欢的应用程序在本地上传、下载、编辑和查看远程文件。

**也读作[FindYara–IDA Python 插件用 Yara 规则扫描二进制](https://kalilinuxtutorials.com/findyara-ida-python-plugin/)**

## **新热安装**

直接从 npm 安装可执行文件:

```
[sudo] npm install -g novahot
```

然后植入一个配置文件:

```
novahot config > ~/.novahotrc
```

## **用途**

*   查看可用的木马有 **`novahot trojan list`** 。
*   选择一种适合您的目标语言的特洛伊木马，然后将其源代码复制到一个新文件中。(例:`**novahot trojan view basic.php > ~/my-trojan.php**`)
*   在新创建的木马中更改控制密码。
*   将特洛伊木马上传到目标上可通过 web 访问的位置。
*   在`**~/.novahotrc**`的`**targets**`属性中配置目标信息。
*   运行 **`novahot shell <target>`** 打开一个外壳。

## **外壳模式**

在内部，novahot 使用“模式”和“适配器”来模拟各种交互式客户端，目前包括 mysql、psql (postgres)和 sqlite3 客户端。

要更改 novahot 的模式，请发出适当的“点命令”:

```
.mysql { "username" : "mysql-user", "password" : "the-password", "database" : "the-database" }
```

(改变模式时，连接参数可以指定为 JSON，或者保存为`**~/.novahotrc**`中的目标配置数据。)

例如，mysql 模式可以直接运行如下查询:

```
mysql> SELECT ID, user_login, user_email, user_pass FROM wp_users;
```

## **虚拟命令**

Novahot 实现了四个“虚拟命令”,利用木马内置的有效载荷来扩展外壳的功能:

### **下载**

```
download <remote-filename> [<local-filename>]
```

下载`**<remote-filename>**`到 **`--download-dir`** ，如果指定的话还可以选择重命名为`**<local-filename>**`。

### **上传**

```
upload <local-filename> [<remote-filename>]
```

将`**<local-filename>**`上传到外壳的 **`cwd`** ，如果指定的话，可以选择将`**<local-filename>**`重命名为`**<remote-filename>**`。

### **视图**

```
view <remote-filename> [<local-filename>]
```

将`**<remote-filename>**`下载到 **`--download-dir`** ，并可选地将其重命名为`**<local-filename>**`，下载后，文件将由[配置](https://github.com/chrisallenlane/novahot/wiki/Configuring)中指定的“查看器”应用程序打开。

### **编辑**

```
edit <remote-filename>
```

将 **`<remote-filename>`** 下载到临时文件，然后使用[配置](https://github.com/chrisallenlane/novahot/wiki/Configuring)中指定的“编辑器”打开该文件进行编辑。之后，如果对文件的更改保存在本地，文件将自动重新上传到服务器。

## **提供测试环境**

这个库包含一个建立在[流浪者](https://www.vagrantup.com/)、[码头工人](https://www.docker.com/)和[该死的易受攻击的 Web 应用](http://www.dvwa.co.uk/)(“DVWA”)之上的实验室环境。配置环境的步骤因物理主机的功能而异。

### **使用 docker-compose**

如果您的物理主机上安装了`**docker**`和`**docker-compose**`，您只需执行以下操作:

1.  克隆 **`cd`** 到这个资源库
2.  跑: **`docker-compose up`**

docker 容器启动后，DVWA 将可以在 [http://localhost:80](http://localhost:80) 访问。

### **使用流浪汉**

如果您的物理主机上没有安装`**docker**`,您可以使用 vagger/Virtualbox 来访问支持 docker 的虚拟机:

1.  克隆 **`cd`** 到这个资源库
2.  调配虚拟机: **`vagrant up`**
3.  SSH 进入虚拟机:`**vagrant ssh**`
4.  启动 docker 容器:`**sudo su; cd /vagrant; docker-compose up**`

DVWA 将可在 [http://localhost:8000](http://localhost:8000) 访问。

### **根据实验室环境配置 novahot】**

在您的 **`~/.novahotrc`** 文件中指定以下连接字符串，将 **`novahot`** 客户端连接到嵌入在 DVWA 容器中的 PHP 木马:

```
{

  "targets": {
    "dvwa" : {
      "uri"      : "http://localhost:8000/novahot.php",
      "password" : "the-password",

      "mysql" : {
        "username": "root",
        "password": "vulnerables",
        "database": "dvwa"
      }
    }
  }

}
```

然后，您可以通过以下方式建立一个 webshell:

```
novahot shell dvwa
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/chrisallenlane/novahot#shell-modes)