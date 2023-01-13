# 悄悄话:识别静态结构化文本中的硬编码秘密

> 原文：<https://kalilinuxtutorials.com/whispers-2/>

[![](img/1b31d75f4a9b181c575b5c4bd95194c7.png)](https://blogger.googleusercontent.com/img/a/AVvXsEhkkvomAOGOtGYEpNXMK54e2an3tyF00cP-w-gILOtsX3yVzB7l6C87BLxronVFdrJVkFO-2TBi49HG-17Nf1HLV8htqGGSRVJVKNW4UU8QY_gO-Yhy_O-1uKcNvz-ueod3-Ihm7b9EbXZQwThogRyB2ekFx860GEjnZ0pgjzg3eO9Lfyq_j6pRpsba=s676)

**Whispers** 是一款静态代码分析工具，专为解析各种常见数据格式，搜索硬编码凭证和危险函数而设计。Whispers 可以在 CLI 中运行，也可以集成到 CI/CD 管道中。

**检测到**

*   密码
*   API 令牌
*   AWS 键
*   私钥
*   哈希凭据
*   认证令牌
*   危险的功能
*   敏感文件

**支持的格式**

Whispers 旨在成为一个**结构化文本**解析器，而不是代码解析器。

当前支持以下常用格式:

*   亚姆
*   JSON
*   可扩展标记语言
*   。npmrc
*   。pypirc
*   。htpasswd 程序
*   。性能
*   pip.conf
*   会议/ ini
*   Dockerfile
*   Dockercfg
*   外壳脚本
*   Python3

由于本地语言支持，Python3 文件被解析为 ASTs。

**申报&赋值** **格式**

以下语言文件被解析为文本，并检查公共变量声明和赋值模式:

*   Java Script 语言
*   Java 语言(一种计算机语言，尤用于创建网站)
*   去
*   服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

**特殊格式**

*   AWS 凭据文件
*   JDBC 连接字符串
*   Jenkins 配置文件
*   SpringFramework Beans 配置文件
*   Java 属性文件
*   Dockercfg 私有注册表授权文件
*   Github 令牌

**安装**

**来自 PyPI**

**pip3 安装窃窃私语**

**来自 GitHub**

**git 克隆 https://github.com/Skyscanner/whispers
CD 低语
make 安装**

**用途**

**CLI**

**密语–帮助
密语–信息
密语来源/代码/文件 OrDir
密语–配置 config.yml 来源/代码/文件 OrDir
密语–输出/tmp/secrets.yml 来源/代码/文件 OrDir
密语–规则 aws-id、AWS-秘密来源/代码/文件 OrDir
密语–严重性拦截器、关键来源/代码/文件 OrDir
密语–退出代码 7 来源/代码/文件 OrDir**

**Python**

**from whispers . CLI import parse _ args
from whispers . core import run
src = " tests/fixtures "
configfile = " whispers/config . yml "
args = parse _ args(["-c "，config file，src])
for secret in run(args):
print(secret)**

**配置**

在 Whispers 中有几个可用的配置选项。可以根据文件路径、键或值来包含/排除结果。文件路径规范被解释为全局变量。键和值接受正则表达式和其他几个参数。有一个默认的内置配置文件，如果您不提供自定义文件，将会使用该文件。

`**config.yml**`应具有以下结构:

**包括:
文件:
–“/*。yml " exclude:files:–"/test//*"–"/tests/**/*"
keys:
–^foo
values:
–bar $
规则:
starks:
消息:来自北方的低语
严重性:临界
value:
regex:(aria | ned)stark
ignore case:true**

调整检测(即删除误报和不想要的结果)的最快方法是将默认的 [config.yml](https://github.com/Skyscanner/whispers/blob/master/whispers/config.yml) 复制到一个新文件中，对其进行修改，并将其作为参数传递给 Whispers。

`**whispers --config config.yml --rules starks src/file/or/dir**`

**自定义规则**

规则指定了应该从键值对中提取的实际内容。有几个常见的内置规则，如 AWS 密钥和密码，但该工具可以根据新规则轻松扩展。

*   自定义规则可以在`**rules:**`下的主配置文件中定义
*   自定义规则可以添加到耳语/规则

**rule-id: # unique rule name
描述:格式类似 AWS 会话令牌
的值消息:AWS 会话令牌#报告将显示此消息
严重性:BLOCKER # BLOCKER、CRITICAL、MAJOR、MINOR、INFO
关键字:#指定关键字格式
regex: (aws。？会话。？token)？
ignorecase: True #不区分大小写匹配
value: #指定值格式
regex: ^(？=.*【a-z】)(？=.*【A-Z】)【A-Za-z0-9+\/】{ 270，450}$
ignorecase: False #区分大小写匹配
minlen: 270 #值至少有这么长
isBase64: True #值是 Base64 编码的
isAscii: False #值在解码时是二进制数据
isUri: False #值的格式不像 URI
相似:0.35 #最大值**

**插件**

所有解析功能都是通过插件实现的。每个插件用`pairs()`方法实现一个类，该方法遍历文件并返回要用规则检查的键值对。

**class PluginName:
def pairs(self，file):
yield "key "，" value"**

[**Download**](https://github.com/Skyscanner/whispers)