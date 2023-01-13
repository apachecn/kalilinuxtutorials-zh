# RapidRepoPull:从列表中快速提取并安装回购

> 原文：<https://kalilinuxtutorials.com/rapidrepopull/>

RapidRepoPull 的目标是快速从列表中拉出并安装回购。这个程序使用 Python 来克隆/维护多个使用线程和多重处理的安全相关的 repos。

**用例**

*   在新系统上快速安装您最喜爱的安全回购
*   利用 Python 启动多个并发 git 克隆任务
*   根据需要向 worker_data 列表中添加 remove repos，以满足个别用例/项目需求

**要求**

*   这个程序是用 Python 版本 3.7.2 64 位测试的
*   确保安装了 Python3 虚拟环境包(Ubuntu)

**sudo apt-get 安装 python3-venv**

*   确保安装了 git(Ubuntu)

**sudo apt-get 安装 git**

**也可以理解为-[remot 3d:为大圣灵降临者](https://kalilinuxtutorials.com/remot3d-pentesters/)T3 创造的简单工具**

**使用选项 1 自动(Docker)**

*   克隆代码回购

**git 克隆 https://github.com/tbalz2319/RapidRepoPull.git**

*   将目录更改为 RapidRepoPull

**cd 快速弹出**

*   该脚本将在一个最小的 Alpine Docker 容器(126 MB)中运行，并提取当前工作目录中的目录

**坞站-复合 up–build**

**使用选项 2 本地安装**

*   克隆代码回购

**git 克隆 https://github.com/tbalz2319/RapidRepoPull.git**

*   将目录更改为 RapidRepoPull

**cd 快速弹出**

*   执行下面的脚本

**。/install.sh**

**使用选项 3 手动**

*   克隆代码回购

**git 克隆 https://github.com/tbalz2319/RapidRepoPull.git**

*   将目录更改为 RapidRepoPull

**cd 快速弹出**

*   创建一个虚拟 Python3 环境来运行这段代码

**python3 -m venv venv**

*   激活虚拟环境

**源 venv/bin/activate**

*   安装要求

**pip install-r requirements . txt**

*   运行程序

**python3 rapid.py**

**更新程序**

*   运行以下脚本

**。/update.sh**

**批量更新所有现有回购**

*   运行命令，通过尝试获取最新版本来维护所有现有的回购协议

**。/update_repos.sh**

**待办事项**

*   添加错误处理

**清理代码**

[**Download**](https://github.com/tbalz2319/RapidRepoPull)