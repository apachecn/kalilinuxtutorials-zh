# 交联:LinkedIn 枚举工具

> 原文：<https://kalilinuxtutorials.com/crosslinked-3/>

[![](img/a0835b7b40665af5285f50760482e764.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhetfEN_6kZBm2gjVzXhI0J33yX0F_wz-_ltC03EvS4OlFpYyAWKfNsbD1BYNeDxlG1N-zbYbWhTeKSzlPsR9AX_MS4EtN9y6YJqNzqFNGmKScoWLYJA4zrSN1YDpvVZOUM9mjMRCvhuB5p5jU5TTbfNCnHKFVclHAS8ewcV_BRPRFBm9downZtMB4D/s1280/logo.png)

**交联**是一个 LinkedIn 枚举工具，使用搜索引擎抓取从组织中收集有效的员工姓名。这种技术提供了准确的结果，而不需要使用 API 键、凭证或直接访问 LinkedIn！

## 安装

安装 PyPi 的最新稳定版本:

**pip3 安装交联**

或者，从 GitHub 安装最新的代码:

**git 克隆 https://github.com/m8sec/crosslinked
CD 交联
python3 安装安装**

## 先决条件

交联假设组织的帐户命名约定已经确定。这是执行所必需的，应该根据预期的输出添加到 CMD 参数中。参见下面的`**Naming Format**`和`**Example Usage**`部分:

### 命名格式

**{f}。{last} = j.smith
{first。{ last } = John . Smith
CMP { first } { l } = CMP \ Johns
{f}{last}@company.com = jsmith@company.com**

## 搜索

默认情况下，交联将使用`**google**`和`**bing**`搜索引擎来识别目标组织的员工。执行后，两个文件( **`names.txt` & `names.csv`** )会出现在当前目录下，除非在 CMD args 中修改。

*   *names . txt*–指定格式的唯一用户帐户列表。
*   *names . CSV*–原始搜索数据。更多信息见下面的`**Parse**`部分。

### 用法举例

**python3 交联. py-f“{ first }”。{last}@domain.com '公司名称**

**python3 交联. py-f ' domain { f } { last } '-t 15-j 2 company _ name**

## 从语法上分析

执行后账户命名规则改变了，现在你可以点击验证码了？没问题！

交联 v0.2.0 现在包括一个`**names.csv**`输出文件，存储所有刮削数据，包括:**`first name``last name``job`** `**title**`**`url`。**这可以被接收和解析，以根据需要重新格式化用户帐户。

### 用法举例

**python3 交联. py-f“{ f } { last } @ domain . com”names . CSV**

## 附加选项

### 代理旋转

最新版本的交联提供代理支持，以轮换源地址。用户可以用`**--proxy 127.0.0.1:8080**`输入单个代理，也可以通过**T1 使用多个代理。**

**cat proxies . txt
127 . 0 . 0 . 1:8080
socks 4://111 . 111 . 111 . 111
socks 5://222 . 222 . 222 . 222
python 3 crossed . py–proxy-file proxies . txt-f“{ first }。{last}@company.com' -t 10 "公司"**

## 使用

**位置参数:
company_name 目标公司名称
可选参数:
-h，–help 显示帮助消息并退出
-t TIMEOUT 每次搜索的最大超时(默认=15)
-j JITTER 请求之间的抖动(默认=1)
搜索参数:
–搜索引擎搜索引擎(默认='google，bing')
输出参数:
-f 格式名称，例如:' domain{f}{last} '，' {first}。{ last } @ domain . com '
-o OUTFILE 更改输出文件的名称(omit_extension)
代理参数:
–代理代理代理请求(IP:Port)
–代理文件代理从文件加载代理进行循环**

[**Download**](https://github.com/m8sec/CrossLinked)