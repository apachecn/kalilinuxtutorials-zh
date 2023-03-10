# 攻击性 Azure:针对微软 Azure 的攻击性工具集合

> 原文：<https://kalilinuxtutorials.com/offensive-azure/>

[![](img/4b4c88ae623504489a931edda521434b.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjL7BpCi1Ic2At8CsSSOaJsMJek_UBsZP_qDPZ0uQEb3o5ekbCDwB68JkOdTZyvHxrWFE48Zg2L5nYyuImQT-9mMHl0VbpcG8vCGCv_UuvLTvqlB_7YC1XM06WHgLDLOzWvMvDY6W3dCWCYJweZl61xjZzs5ZZ_nlp-6QHD8tNFFWm03Q73Ba0x7Zcz/s728/160513484-cb70370c-9fce-48d1-84ec-8b9ea3cf8e5a%20(1).png)

是一个针对微软 Azure 的攻击性工具的集合，用 Python 编写，与平台无关。下面是当前的工具列表及其功能的简要描述。

*   `**./Device_Code/device_code_easy_mode.py**`
    *   生成由目标用户输入的代码
    *   可用于一般令牌生成或网络钓鱼/社交工程活动。
*   `**./Access_Tokens/token_juggle.py**`
    *   以各种方式接收刷新令牌，并为指定的资源检索新的刷新令牌和访问令牌
*   `**./Access_Tokens/read_token.py**`
    *   接收访问令牌并解析包含的声明信息，检查是否过期，尝试验证签名
*   `**./Outsider_Recon/outsider_recon.py**`
    *   接受一个域并枚举尽可能多的关于租户的信息，而不需要身份验证
*   `**./User_Enum/user_enum.py**`
    *   接受用户名或用户名列表，并尝试使用以下三种方法之一来枚举有效帐户
    *   也可以用来执行密码喷雾
*   `**./Azure_AD/get_tenant.py**`
    *   接收访问令牌或刷新令牌，输出租户 ID 和租户名称
    *   创建文本输出文件以及与 BloodHound 兼容的 aztenant 文件
*   `**./Azure_AD/get_users.py**`
    *   接受访问令牌或刷新令牌，输出 Azure AD 中的所有用户和 Microsoft Graph 中的所有可用用户属性
    *   创建三个数据文件，一个压缩的 json 文件，一个原始的 json 文件，以及一个与嗜血猎犬兼容的 azusers 文件
*   `**./Azure_AD/get_groups.p**y`
    *   接受访问令牌或刷新令牌，输出 Azure AD 中的所有组和 Microsoft Graph 中的所有可用组属性
    *   创建三个数据文件，一个压缩的 json 文件、一个原始 json 文件和一个与 BloodHound 兼容的 azgroups 文件
*   `**./Azure_AD/get_group_members.py**`
    *   接受访问令牌或刷新令牌，输出 Azure AD 中的所有组成员身份以及 Microsoft Graph 中的所有可用组成员属性
    *   创建三个数据文件，一个压缩的 json 文件、一个原始 json 文件和一个与 BloodHound 兼容的 azgroups 文件
*   `**./Azure_AD/get_subscriptions.py**`
    *   接受 ARM 令牌或刷新令牌，输出 Azure 中的所有订阅以及 Azure 资源管理器中的所有可用订阅属性
    *   创建三个数据文件，一个压缩的 json 文件、一个原始 json 文件和一个与 BloodHound 兼容的 azgroups 文件
*   `**./Azure_AD/get_resource_groups.py**`
    *   接受 ARM 令牌或刷新令牌，输出 Azure 中的所有资源组和 Azure 资源管理器中的所有可用资源组属性
    *   创建两个数据文件，一个原始 json 文件和一个与 BloodHound 兼容的 azgroups 文件
*   `**./Azure_AD/get_vms.py**`
    *   接受 ARM 令牌或刷新令牌，输出 Azure 中的所有虚拟机和 Azure 资源管理器中的所有可用虚拟机属性
    *   创建两个数据文件，一个原始 json 文件和一个与 BloodHound 兼容的 azgroups 文件

# 安装

攻击性 Azure 可以通过多种方式安装，也可以根本不安装。

欢迎您克隆存储库并执行您想要的特定脚本。每个模块都包含一个`**requirements.txt**`文件，以尽可能简化这个过程。

## 诗歌

该项目是为与`**poetry**`一起工作而构建的。要使用，请遵循以下几个步骤:

git 克隆 https://github.com/blacklanternsecurity/offensive-azure.git
CD。/攻势-蔚蓝
诗歌安装

## 诗意

该项目是为与`**poetry**`一起工作而构建的。要使用，请遵循以下几个步骤:

git 克隆 https://github.com/blacklanternsecurity/offensive-azure.git
CD。/攻势-蔚蓝
诗歌安装

## 点

repo 的打包版本也保存在 pypi 上，所以您也可以使用`**pip**`来安装。我们建议您使用 **`pipenv`** 来保持您的环境尽可能的干净。

**pipenv shell
pip install offensive _ azure**

# 使用

如何使用这个工具包取决于你自己。每个模块都可以独立运行，或者你可以把它作为一个包来安装并使用它。每个模块都被导出到一个与模块文件同名的脚本中。例如:

## 诗歌

**诗歌安装
诗歌跑局外人 _ 侦察 your-domain.com**

## 点

**pipenv shell
pip 安装攻势 _azure
局外人 _ 侦察 your-domain.com**

[**Download**](https://github.com/blacklanternsecurity/offensive-azure)