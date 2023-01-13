# SilentHound:通过 LDAP 解析用户、管理员、组等，悄悄地枚举一个活动目录域。

> 原文：<https://kalilinuxtutorials.com/silenthound/>

[![](img/74ab71b5a217cde5fed2f1e156b5a7e7.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjEiDI94zZQmbz3qtklZ6D0YOz7ooNGFYmA5kG00TXToW_oWJn35nBRjKJIOd63k-Z9X8kRpwpm9R7Sg3PCSB_Ob5qbeiw1lwdwJS3RjBsj7gSWNpysn6I_owtcwebUCtNlwrjYu3RUDzM3i9lXqd5gdT806phQXRvIXQEDupmcMwSEwjjFfEZ7D5TP/s728/96061566-93d8af00-0e61-11eb-8b84-3fd207290be2%20(2).png)

**SilentHound** 通过 LDAP 解析用户、管理员、组等悄悄枚举一个活动目录域。由第八层安全部门的尼克·斯温克创建。

### 安装

#### 使用 pipenv(推荐方法)

**sudo python3 -m pip 安装–用户 pipenv
git 克隆 https://github.com/layer8secure/SilentHound.git
CD silen sound
pipenv 安装**

#### 来自 requirements.txt(传统)

不推荐使用这种方法，因为 python-ldap 会导致许多依赖错误。

安装与`**pip**`的依赖关系:

**python 3-m pip install-r requirements . txt
python 3 silenthound . py-h**

**用途**

**$ pipenv 运行 python silen sound . py-h
用法:silen sound . py[-h][-u 用户名] [-p 密码] [-o 输出] [-g] [-n] [-k]目标域
悄悄枚举一个活动目录环境。
位置参数:
目标域控制器 IP
域点(。)分隔域名，包括两个上下文，例如 ACME.com/home . local/htb.net
可选参数:
-h，–帮助显示此帮助消息并退出
-u 用户名，–用户名用户名
LDAP 用户名–与用户主体名称不同。例如，用户名:bob.dole 可能是' bob
dole'
-p PASSWORD，–PASSWORD PASSWORD
LDAP PASSWORD–使用单引号' password'
-o OUTPUT，–OUTPUT OUTPUT
输出文件的名称。在当前工作目录中为主机、用户、域管理员和描述
创建输出文件。
-g，–组显示包含用户成员的组名。
-n，–org-unit 显示组织单位。
-k，–keywords 在 LDAP 对象中搜索关键字。**

### 关于

一个轻量级的工具，快速和安静地枚举一个活动目录环境。该工具的目标是在尽可能减少网络噪音的同时了解地形。该工具将生成一个用于解析的 LDAP 查询，并创建一个缓存文件以防止网络上的进一步查询/干扰。如果没有传递凭证，它将尝试匿名绑定。

使用`**-o**`标志将导致每个部分的输出文件通常出现在 stdout 中。使用所有标志创建的文件将是:

**rw-r-r-1 kali 122 jun 30 11:37 base name-description . txt
rw-r-r-1 kali 60 jun 30 11:37 base name-domain _ administry . txt
rw-r-r-1 kali 2620 jun 30 11:37 base name-groups . txt
rw-r-r-1 kali 89 jun**

[**Download**](https://github.com/layer8secure/SilentHound)