# cloud mapper–该工具有助于分析您的 AWS 环境

> 原文：<https://kalilinuxtutorials.com/cloudmapper/>

**CloudMapper** 帮助您分析您的亚马逊网络服务(AWS)环境。最初的目的是生成网络图，并在浏览器中显示出来。它现在包含了更多的功能。点击[此处](https://duo-labs.github.io/cloudmapper/)观看演示。

![](img/4b5c0c2dcea27b6dd4bb91b5bdb0cf15.png)

**也读[Frisky——辅助二进制 App 倒车的工具&增强](https://kalilinuxtutorials.com/frisky/)**

## **安装**

##### **要求:**

*   `pip`和`**virtualenv**`
*   你还需要`**jq**`和库`**pyjq**`，这需要安装一些额外的工具。

###### **在 macOS 上:**

```
# clone the repo
git clone git@github.com:duo-labs/cloudmapper.git
# Install pre-reqs for pyjq
brew install autoconf automake libtool jq awscli python3
cd cloudmapper/
python3 -m venv ./venv
source venv/bin/activate
pip install -r requirements.txt
```

###### **在 Linux 上:**

```
# clone the repo
git clone git@github.com:duo-labs/cloudmapper.git
# (Centos, Fedora, RedHat etc.):
# sudo yum install autoconf automake libtool python34-devel jq awscli
# (Debian, Ubuntu etc.):
# You may additionally need "build-essential"
sudo apt-get install autoconf automake libtool python3-dev jq awscli
cd cloudmapper/
python3 -m venv ./venv
source venv/bin/activate
pip install -r requirements.txt
```

## **设置云映射器**

##### **1。配置您的帐户**

*   **手动编辑配置文件**

将`config.json.demo`复制到`config.json`并编辑它以包含您的帐户 ID 和名称(例如“prod”)，以及任何外部 CIDR 名称。CIDR 是一个 IP 范围，如`1.2.3.4/32`，这意味着只有 IP `1.2.3.4`。

*   **生成配置文件**

CloudMapper 具有配置您的帐户的命令:

```
python cloudmapper.py configure {add-account|remove-account} --config-file CONFIG_FILE --name NAME --id ID [--default DEFAULT]
python cloudmapper.py configure {add-cidr|remove-cidr} --config-file CONFIG_FILE --cidr CIDR --name NAME
```

这将允许您定义在您的环境中使用的不同 AWS 帐户和已知的 CIDR IP。

##### **2。收集关于账户的数据**

这一步使用 CLI 进行`describe`和`list`调用，并将 json 记录在`account-data`下帐户名指定的文件夹中。

在本地，必须使用正确的访问密钥和区域信息来配置 AWS CLI。在 AWS 控制台中生成新的访问密钥，并将生成的密钥输入到`aws configure`(如果您还没有这样做的话)。

您必须配置 AWS 凭据，CLI 可以使用这些凭据并对要收集的不同元数据具有读取权限。如果您计划使用 CloudMapper 的所有特性，请授予`SecurityAudit`策略。如果您仅计划使用网络可视化，这可以减少到更小的权限集:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Resource": "*",
      "Action": [
        "ec2:DescribeRegions",
        "ec2:DescribeAvailabilityZones",
        "ec2:DescribeVpcs",
        "ec2:DescribeSubnets",
        "ec2:DescribeSecurityGroups",
        "ec2:DescribeVpcPeeringConnections",
        "ec2:DescribeInstances",
        "ec2:DescribeNetworkInterfaces",
        "rds:DescribeDBInstances",
        "elasticloadbalancing:DescribeLoadBalancers"
      ]
    }
  ]
}
```

可以使用 bash 脚本或通过 python 代码库来收集数据。两个选项都支持一个`--profile`来指定要使用的 AWS 帐户配置文件。

*   **Bash 脚本**

如果您需要别人为您获取这些数据，而不需要设置 python 环境，那么使用脚本会很有帮助。

注意:该脚本将收集一小部分可用数据。最好尽可能使用下面的选项 2。

```
./collect_data.sh --account my_account
```

`my_account`只是您帐户的名称(例如“prod”)。如果您配置了多个 AWS 概要文件，您也可以传递一个`--profile`选项。您现在应该有一个包含。描述你的帐号的 json 文件在一个以帐号名命名的目录中。

*   **Python 代码**

```
python cloudmapper.py collect --account my_account
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/duo-labs/cloudmapper)