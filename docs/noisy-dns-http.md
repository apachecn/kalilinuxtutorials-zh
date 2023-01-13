# 噪声–简单随机 DNS、HTTP/S 互联网流量噪声发生器

> 原文：<https://kalilinuxtutorials.com/noisy-dns-http/>

**noise**是一个简单的 python 脚本，当您进行常规 web 浏览时，它会在后台生成随机的 HTTP/DNS 流量噪声，从而降低您的 web 流量数据的销售价值和额外的隐蔽性。在 MacOS High Sierra、Ubuntu 16.04 和 Raspbian Stretch 上测试，与 Python 2.7 和 3.6 兼容

这些指令将让您在本地机器上启动并运行项目的副本。

**也可理解为 [轨道——使用递归爬行](https://kalilinuxtutorials.com/orbit-crypto-wallets/)** 绘制加密钱包之间的关系

## **依赖关系**

如果尚未安装，使用`**pip**`安装`**requests**`:

```
pip install requests
```

## **用法**

**克隆存储库**

```
git clone https://github.com/1tayH/noisy.git
```

**导航到`noisy`目录**

```
cd noisy
```

**运行脚本**

```
python noisy.py --config config.json
```

**程序可以接受许多命令行参数:**

```
$ python noisy.py --help
usage: noisy.py [-h] [--log -l] --config -c [--timeout -t]**

**optional arguments:
  -h, --help    show this help message and exit
  --log -l      logging level
  --config -c   config file
  --timeout -t  for how long the crawler should be running, in seconds
```

只有配置文件参数是必需的。

## **噪声输出**

```
$ docker run -it noisy --config config.json --log debug
DEBUG:urllib3.connectionpool:Starting new HTTP connection (1): 4chan.org:80
DEBUG:urllib3.connectionpool:http://4chan.org:80 "GET / HTTP/1.1" 301 None
DEBUG:urllib3.connectionpool:Starting new HTTP connection (1): www.4chan.org:80
DEBUG:urllib3.connectionpool:http://www.4chan.org:80 "GET / HTTP/1.1" 200 None
DEBUG:root:found 92 links
INFO:root:Visiting http://boards.4chan.org/s4s/
DEBUG:urllib3.connectionpool:Starting new HTTP connection (1): boards.4chan.org:80
DEBUG:urllib3.connectionpool:http://boards.4chan.org:80 "GET /s4s/ HTTP/1.1" 200 None
INFO:root:Visiting http://boards.4chan.org/s4s/thread/6850193#p6850345
DEBUG:urllib3.connectionpool:Starting new HTTP connection (1): boards.4chan.org:80
DEBUG:urllib3.connectionpool:http://boards.4chan.org:80 "GET /s4s/thread/6850193 HTTP/1.1" 200 None
INFO:root:Visiting http://boards.4chan.org/o/
DEBUG:urllib3.connectionpool:Starting new HTTP connection (1): boards.4chan.org:80
DEBUG:urllib3.connectionpool:http://boards.4chan.org:80 "GET /o/ HTTP/1.1" 200 None
DEBUG:root:Hit a dead end, moving to the next root URL
DEBUG:urllib3.connectionpool:Starting new HTTPS connection (1): www.reddit.com:443
DEBUG:urllib3.connectionpool:https://www.reddit.com:443 "GET / HTTP/1.1" 200 None
DEBUG:root:found 237 links
INFO:root:Visiting https://www.reddit.com/user/Saditon
DEBUG:urllib3.connectionpool:Starting new HTTPS connection (1): www.reddit.com:443
DEBUG:urllib3.connectionpool:https://www.reddit.com:443 "GET /user/Saditon HTTP/1.1" 200 None
...
```

## **使用 Docker** 构建

*   **构建图像**

`**docker build -t noisy .**`

**或者**如果你想做一个**树莓派**(运行 Raspbian stretch):

`**docker build -f Dockerfile.pi -t noisy .**`

*   **创建容器并运行:**

`**docker run -it noisy --config config.json**`

[![https://github.com/Nekmo/dirhunt](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/1tayH/noisy)