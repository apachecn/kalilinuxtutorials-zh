# Red-Kube:基于 Kubectl 的红队 K8S 对手仿真

> 原文：<https://kalilinuxtutorials.com/red-kube/>

[![Red-Kube : Red Team K8S Adversary Emulation Based On Kubectl](img/71e27cc4dccc4a30c62672686bcd2514.png "Red-Kube : Red Team K8S Adversary Emulation Based On Kubectl")](https://1.bp.blogspot.com/-vTpR9SOSnIs/YKzROhkBvRI/AAAAAAAAJOA/GwORoWF62f8zkolpJA9y3YJ5K2ZYmrZZwCLcBGAsYHQ/s728/redcube%2B%25281%2529.png)

Red-Kube 是从攻击者的角度评估 Kubernetes 集群的安全状况而编写的 kubectl 命令的集合。

这些命令要么是被动的，用于数据收集和信息披露，要么是主动的，用于执行影响集群的实际操作。

这些命令被映射到米特 ATT 和 CK 的策略中，以帮助了解我们最大的差距在哪里，并对我们的发现进行优先排序。

当前版本包装了一个 python 编排模块，可以基于不同的场景或策略一次运行几个命令。

请小心使用，因为有些命令是活动的，并且会主动部署新容器或更改基于角色的访问控制配置。

**先决条件**

python3 要求

**pip 3 install-r requirements . txt**

kubectl (Ubuntu / Debian)

**sudo apt-get update
sudo apt-get install-y apt-transport-https ca 凭证 curl
sudo curl-fsslo/usr/share/key rings/ku bletes 归档金钥环。gpg https://packages . cloud . Google . com/apt/doc/apt-key . gpg
echo】deb[signed-by =/usr/share/key ring**

kubectl(基于红帽)

**cat</etc/yum . repos . d/kubricks . repo
【kubricks】
【名称】
base URL = https://packages . cloud . Google . com/yum/repos/kubricks-El 7-x86 _ 64
enabled = 1
【gpg check = 1】**

japan quarterly 日本季刊

sudo apt-get update-y
sudo apt-get install-y jq

**用途**

**用法:python 3 main . py[-h][–mode active/passive/all][–TACTIC _ NAME][–show _ tactics][–clean up]
必需参数:
–mode run ku bectl 命令哪些是主动/被动/所有模式
–tactice choose tactice
其他参数:
-h–帮助显示此帮助信息并退出
–show _ tactics 显示所有战术**

**ATT 指挥& CK 战术**

| 战略 | 数数 |
| --- | --- |
| 侦察 | Two |
| 初始访问 | Zero |
| 执行 | Zero |
| 坚持 | Two |
| 权限提升 | four |
| 防御规避 | one |
| 凭证访问 | eight |
| 发现 | Fifteen |
| 横向运动 | Zero |
| 收藏品 | one |
| 指挥和控制 | Two |
| 漏出 | one |
| 影响 | Zero |

[**Download**](https://github.com/lightspin-tech/red-kube)