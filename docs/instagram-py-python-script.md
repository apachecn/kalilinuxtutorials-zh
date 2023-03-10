# insta gram-Py–暴力攻击的 Python 脚本

> 原文：<https://kalilinuxtutorials.com/instagram-py-python-script/>

Instagram-Py 是一个简单的 python 脚本，用于对 Instagram 进行暴力攻击，该脚本可以绕过错误密码的登录限制，因此基本上可以测试无限数量的密码。

Instagram-Py 经过演示，可以用尽可能少的资源在一个单独的 Instagram 账户上测试超过 600 万个密码。

这个脚本复制了 instagram android 应用程序的练习，并通过 tor 发送请求，所以你是安全的，但是如果你的 tor 安装配置错误，那么责任就在你。

### **也读 [Evasi0n 苹果 iOS 7.x 的越狱工具& 6.x 用户](http://kalilinuxtutorials.com/evasi0n-jailbreaking/)**

## **安装 Instagram-Py**

### **使用 pip 获取 Instagram-py**

确保您已经安装了最新版本的 pip(>= 9.0)和 python(>= 3.6)

```
$ sudo easy_install3 -U pip # you have to install python3-setuptools , update pip
$ sudo pip3 install requests --upgrade
$ sudo pip3 install requests[socks]
$ sudo pip3 install stem
$ sudo pip3 install instagram-py
$ instagram-py # installed successfully
$ # Now lets copy the config file to your hard drive!
$ wget -O ~/instapy-config.json "https://git.io/v5DGy"

```

## **配置 Instagram-Py**

打开你在主目录下找到的配置文件，这个文件**非常重要**位于 **~/instapy-config.json** ，除了 tor 配置，不要修改任何东西

```
$ vim ~/instapy-config.json # open it with your favorite text editior!
```

**配置文件看起来像这样**

```
{
 "api-url" : "https://i.instagram.com/api/v1/",
 "user-agent" : "Instagram 10.26.0 Android (18/4.3; 320dp..... ",
 "ig-sig-key" : "4f8732eb9ba7d1c8e8897a75d6474d4eb3f5279137431b2aafb71fafe2abe178",
 "ig-sig-version" : "4",
 "tor" : {
    "server" : "127.0.0.1",
    "port" : "9050",
    "protocol" : "socks5",
    "control" : {
          "password" : "",
          "port" : "9051"
      }
  }

}

```

api-url :除非你知道你在做什么，否则不要改变它

用户代理:除非你知道你的东西，否则不要改变它

**ig-sig_key** :除非是新版本，否则不要更改，这是从 instagram apk 文件中提取的

**tor** :根据你的 tor 服务器配置改变一切，不要搞砸！

### **配置 Tor 服务器打开控制端口**

打开通常位于 **/etc/tor/torrc** 的 **tor 配置**文件

```
$ sudo vim /etc/tor/torrc # open it with your text editor

```

**在**中搜索该**特定章节**的文件

```
## The port on which Tor will listen for local connections from Tor
## controller applications, as documented in control-spec.txt.
#ControlPort 9051

```

**通过删除“控制端口”前的 **#** 取消对**“控制端口”的注释，**现在保存文件并重启 tor 服务器**

现在你已经准备好破解任何 instagram 账号了，确保你的 tor 配置匹配~/instapy-config.json

## **用法**

**终于**了，现在可以用 instagram-py 了！

```
$ instagram-py your_account_username path_to_password_list

```

[![](img/a51de913dc60eee505c4a68651ee8e4d.png)](https://github.com/getsecnow/instagram-py)