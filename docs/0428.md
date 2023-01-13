# node.js 中编写的 nodecrypto 勒索软件

> 原文：<https://kalilinuxtutorials.com/nodecrypto-ransomware/>

nodeCrypto 是一个用 NodeJs 编写的 Linux 勒索软件，用于加密预定义的文件。这个项目是为教育目的，你是唯一负责使用 nodeCrypto。

**安装服务器**

将服务器/文件夹中的所有文件上传到您的 web 服务器上。
创建 sql 数据库并导入[SQL/node crypto . SQL](https://github.com/atmoner/nodeCrypto/blob/master/sql/nodeCrypto.sql)编辑 [server/libs/db.php](https://github.com/atmoner/nodeCrypto/blob/master/server/libs/db.php) 并添加您的 SQL ID。

**也读作:[SALT——Linux 内核的竹节分配器跟踪器](https://kalilinuxtutorials.com/salt/)**

**安装并运行**

git 克隆 https://github . com/atmoner/nodecrypt . git
CD nodecrypto&&NPM 安装

你必须编辑 index.js 中的第一个变量
一旦你的配置完成，你就可以启动勒索软件了。

节点索引. js

web 服务器根目录下的文件将被加密并发送到服务器。

**待办事项**

*   客户(受害者)
    *   加密 web 服务器
    *   使用私钥进行加密
    *   适配 SSL
*   计算机网络服务器
    *   恢复数据(用户+加密文件)
    *   格式化数据库
    *   为 web 服务器制作 GUI
*   制作一个可执行文件来解密文件(仅在请求时！联系我)

[**Download**](https://github.com/atmoner/nodeCrypto)