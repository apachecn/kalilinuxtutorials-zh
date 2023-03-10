# OWTF——攻击性 Web 测试框架很棒的工具&让笔测试更高效

> 原文：<https://kalilinuxtutorials.com/owtf-offensive-web-testing-framework/>

OWTF 或进攻性 Web 测试框架，是一个试图联合优秀工具并使 pen 测试更有效的框架。 **OWASP OWTF** 是一个专注于渗透测试效率和安全测试符合安全标准的项目，如 OWASP 测试指南(v3 和 v4)、OWASP 十大标准、PTES 和 NIST，以便 pentesters 有更多时间

*   看到全局，跳出框框思考
*   更高效地查找、验证和组合漏洞
*   有时间调查复杂的漏洞，如业务逻辑/架构缺陷或虚拟主机会话
*   对看似危险的区域进行更多的战术/目标模糊化
*   展示真正的影响，尽管我们通常要测试的时间很短。

该工具是高度可配置的，任何人都可以轻松地创建简单的插件或在配置文件中添加新的测试，而无需任何开发经验。

**注意**:然而，这个工具不是**银弹**，它只会和使用它的人一样好:需要理解和经验来正确地解释工具输出并决定进一步调查什么以证明影响。

**又读[EVI losx——MAC OS/OS X](https://kalilinuxtutorials.com/evilosx-remote-administration-tool/)T5 的邪恶远程管理工具**

## **要求**

*   OWTF 是在 KaliLinux 和 macOS 上开发的，但它是为 Kali Linux(或其他 Debian 衍生物)开发的
*   OWTF 同时支持 Python2 和 Python3。

## **OWTF 安装**

**推荐:**强烈推荐使用 virtualenv！

**`pip install git+https://github.com/owtf/owtf#egg=owtf`** 或者克隆回购和`**python setup.py install**`。

如果您想在 Docker 编写设置中更改数据库密码，请编辑`**docker-compose.yml**`文件中的环境变量。如果您喜欢在一个`.env`文件中覆盖环境变量，使用文件名`**owtf.env**`，这样 Docker Compose 就知道要包含它。

为了在 Windows 或 MacOS 上运行 OWTF，OWTF 使用 Docker Compose。您需要安装 Docker Compose(通过`**docker-compose -v**`检查)。安装 Docker Compose 后，只需运行`**docker-compose up**`，打开 OWTF web 界面的 **`localhost:8009`** 。

**依赖关系:**安装[自制软件](https://brew.sh/)并遵循以下步骤:

```
$ virtualenv <venv name>
$ source <venv name>/bin/activate
$ brew install coreutils gnu-sed openssl
# We need to install 'cryptography' first to avoid issues
$ pip install cryptography --global-option=build_ext --global-option="-L/usr/local/opt/openssl/lib" --global-option="-I/usr/local/opt/openssl/include"
$ git clone <this repo>
$ cd owtf
$ python setup.py install
# Run OWTF!
$ owtf
```

## **特性**

*   **弹性**:如果一个工具崩溃 **OWTF** ，将继续下一个工具/测试，保存工具的部分输出，直到它崩溃。
*   **灵活**:暂停和恢复你的工作。
*   **测试分离** : **OWTF** 将其到目标的流量主要分成 3 种类型的插件:
    *   **被动**:没有流量到达目标
    *   **半被动**:目标正常交通
    *   **主动**:直接漏洞探测
*   广泛的 REST API。
*   几乎拥有完整的 OWASP 测试指南(v3，v4)，Top 10，NIST，CWE 覆盖范围。
*   **Web 界面**:轻松管理大型渗透项目。
*   **互动报道**:
*   **工具输出的自动**插件排名，完全由用户配置。
*   **可配置的**风险等级
*   每个插件的内嵌注释编辑器。

[![https://github.com/Nekmo/dirhunt](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/owtf/owtf)