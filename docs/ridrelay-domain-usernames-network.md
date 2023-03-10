# rid relay–在内部网络上获取域名用户名的简单方法

> 原文：<https://kalilinuxtutorials.com/ridrelay-domain-usernames-network/>

在内部网络上获取域名用户名的快捷方式。RidRelay 结合了 SMB 中继攻击、常见的基于 lsarpc 的查询和 RID 循环来获得域用户名列表。它采取以下步骤:

*   启动 SMB 服务器并等待传入的 SMB 连接
*   传入的凭据被中继到指定的目标，从而创建与中继用户的上下文的连接
*   通过 SMB 连接到 lsarpc 管道进行查询，以获得域用户名列表。这通过循环高达 50000 RIDs 来完成。

**也可理解为[Mercure——安全经理用来训练他们的同事进行网络钓鱼的工具](https://kalilinuxtutorials.com/mercure-tool-security-managers-phishing/)**

## **RidRelay 依赖关系**

*   Python 2.7(抱歉，impacket 和 3 不兼容🙁)
*   impactet v0.9.17 或更高版本

## **安装**

```
pipenv install --two
pipenv shell

# Optional: Run if installing impacket
git submodule update --init --recursive
cd submodules/impacket
python setup.py install
cd ../..
```

## **用途**

首先，找到一个目标主机进行中继。目标必须是域的成员，并且必须有 SMB 登录。CrackMapExec 可以很快为您获取这些信息！

启动指向目标的 RidRelay:

```
python ridrelay.py -t 10.0.0.50
```

运筹学

还将用户名输出到文件

```
python ridrelay.py -t 10.0.0.50 -o path_to_output.txt
```

[![https://github.com/Nekmo/dirhunt](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/skorov/ridrelay)