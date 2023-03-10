# Haptyc:测试生成框架

> 原文：<https://kalilinuxtutorials.com/haptyc/>

[![](img/ceb1a7784d7c2c0a1c2bad725259ce58.png)](https://blogger.googleusercontent.com/img/a/AVvXsEhYiZbMNKcwjIqJV7BjuuR3CemYQa6xb4javogeWsaM0u5Y8YIM_x4pC_ge57DiQP0sZ59CVRqB5yXAuZ9JvS2sqC7I0Gf54ZS2jmzvmWCWExG4wi-hhDgOPcACWEvfg077cSurqA2IUjLCUpxdvvBLhdDb2BxTlogMcCm_aFA1iOFUD-9jFWNVHRDu=s578)

Haptyc 是一个 python 库，它是为了给涡轮入侵者添加有效载荷位置支持和狙击手/集束炸弹/炮台/干草叉攻击类型而构建的。虽然 Haptyc 很好地实现了这些目标，但它也引入了一种更简单的方法来表达一般的测试序列。虽然这个库的目标是 Turbo intrusor，但它并不依赖于 Turbo intrusor，可以在任何需要在 Python 环境中生成测试的地方使用。不幸的是，由于 Haptyc 是为 jython 解释器构建的，所以目前它只支持 Python 2.7(不过未来的变化会解决这个问题)。

**什么是 Haptyc 标签？**

Haptyc 标签是测试者可以用来注释原始输入有效载荷的标签。测试人员可以使用多个标签来包围 HTTP 请求中的关键数据片段，以将其包装为位置有效载荷。当测试被生成时，Haptyc 将解析原始有效载荷中的所有标签，并根据与标签名称相关联的函数生成测试。当 Haptyc 评估 Haptyc 标签时，它将执行相关联的标签函数(这被称为 Haptyc 变换),以将测试有效载荷放置在请求中相关联标签的位置。每个标签函数将接收一个*数据*参数和一个*状态*参数。数据自变量可以包含标签的内部数据，或者可以包含一些其他测试有效载荷序列。状态参数是与标签相关联的状态对象，其中状态可以在测试迭代之间存储。我们来回顾一个例子。

**例 1:简单列表迭代**

**原始有效载荷**

**GET/animal/[+guess animal]dog[+end]HTTP/1.1**

**Haptyc 类& Haptyc 变换**

**from hap tyc import *
original = " GET/animal/[+guess animal]dog[+end]HTTP/1.1 "
类 test logic(Transform):
@ apply list([" snake "、" cat "、" owl "、" lion "])
def test _ guess animal(self，data，state):
返回数据+"？original = "+self . inner()+"&attempt = "+str(state . ITER)
TestFactory = test logic(original)
对于 test factory 中的测试:
print(test)**

**测试生成**

**得到/动物/蛇？original =狗&attempt = 0 HTTP/1.1
GET/animal/cat？original = dog&attempt = 1 HTTP/1.1
GET/animal/猫头鹰？original =狗&尝试= 2 HTTP/1.1
GET/动物/狮子？original = dog&attempt = 3 HTTP/1.1**

在上面的例子中，我们知道如何使用 Haptyc 以简单的方式表达测试。首先导入 Haptyc 库。其次，我们用 Haptyc 标签注释(GuessAnimal)定义了原始数据。接下来，TestLogic 类被定义并扩展为一个转换类。在这个类中，每个以`**test_**`开头的方法都将被注册为一个 Haptyc 标签，以便在原始有效载荷中进行评估。我们使用一个逻辑装饰器来为这个 Haptyc 转换应用状态逻辑。在这种情况下，我们使用`**@ApplyList(list)**` decorator 告诉 Haptyc 为指定列表中的每一项生成一个测试，并将该项作为数据参数放入 Haptyc 转换中。在转换中，我们返回数据的变异版本，以将其插回到标签的位置。在这种情况下，变异是列表项作为数据与标记(dog)包围的数据连接，然后与状态对象中的 iter 值连接。最后，剩下的 python 展示了在 for 循环迭代器中创建的 TestFactory 对象和生成的所有测试。这是一个标准的狙击手式攻击的例子，目标是一个单一的有效载荷位置。接下来让我们看看其他类型的攻击。

**例 2:集束炸弹**

**原始有效载荷**

**获得/动物？type =[% type]dog[% end]&name =[% name]fido[% end]HTTP/1.1**

**Haptyc 类& Haptyc 变换**

**from hap tyc import *
original = " GET/animal？type =[% type]dog[% end]&name =[% name]fido[% end]HTTP/1.1 "**
**类 TestLogic(Transform):
@ ApplyList(" snake "，" cat "，" owl "，" lion")
def test_type(self，data，state):
return data
@ ApplyList(" Frank "，" Lisa "，" Jin "，" Tooth")
def test_name(self，data，state):
return data
test factory = test factory**

**测试生成**

**获得/动物？type = snake&name = Frank HTTP/1.1
GET/animal？type = snake&name = Lisa HTTP/1.1
GET/animal？type = snake&name = Jin HTTP/1.1
GET/animal？type = snake&name = Tooth HTTP/1.1
GET/animal？type = cat&name = Frank HTTP/1.1
GET/animal？type = cat&name = Lisa HTTP/1.1
GET/animal？type = cat&name = Jin HTTP/1.1
GET/animal？type = cat&name = Tooth HTTP/1.1
GET/animal？type = owl&name = Frank HTTP/1.1
GET/animal？type = owl&name = Lisa HTTP/1.1
GET/animal？type = owl&name = Jin HTTP/1.1
GET/animal？type = owl&name = Tooth HTTP/1.1
GET/animal？type = lion&name = Frank HTTP/1.1
GET/animal？type = lion&name = Lisa HTTP/1.1
GET/animal？type = lion&name = Jin HTTP/1.1
GET/animal？type = lion&name = Tooth HTTP/1.1**

示例 1 展示了如何通过在标签`**[+tag][+end]**`中使用“+”符号注释来评估 transforms sniper 风格。示例 2 展示了我们如何使用 2 个变换/位置来进行集束炸弹式的攻击。正如你所看到的，我们使用了两个独立的转换标签，分别叫做`**[%type][%end]**`和`**[%name][%end]**`。“%”符号告诉 Haptyc 对这些转换进行 clusterbomb 式的评估，对于第一个转换中的每个有效负载，使用第二个转换中的有效负载创建一个测试。测试计数是所涉及的每个转换的测试数量相互相乘。

**例 3:干草叉/电池架**

使用相同的 python 代码，我们可以通过将“%”改为“#”来将攻击方式从集群炸弹切换到干草叉。干草叉式攻击会将阵地有效载荷全部平行放置。测试计数是所有涉及的转换中给定的最低测试数。

**原始有效载荷**

**获得/动物？type =[# type]dog[# end]&name =[# name]fido[# end]HTTP/1.1**

**测试生成**

**获得/动物？type = snake&name = Frank HTTP/1.1
GET/animal？type = cat&name = Lisa HTTP/1.1
GET/animal？type = owl&name = Jin HTTP/1.1
GET/animal？type = lion&name = Tooth HTTP/1.1**

**例子 4:持久转换**

**原始有效载荷**

**获得/动物？type = dog&id =[+idor]0[+end]&process =[@ rand bool]False[@ end]HTTP/1.1**

**Haptyc 类& Haptyc 变换**

**从 haptyc 导入*
导入随机
original = "GET /animal？type = dog&id =[+idor]0[+end]&process =[@ rand bool]False[@ end]HTTP/1.1 "
class test logic(Transform):
@ apply operation(10)
def test _ idor(self，data，state):
return str(state . ITER)
def per _ rand bool(self，data):
return random . choice([" True "，" False"])
TestFactory**

**测试生成**

**获得/动物？type = dog&id = 0&process = False HTTP/1.1
GET/animal？type = dog&id = 1&process = True HTTP/1.1
GET/animal？type = dog&id = 2&process = False HTTP/1.1
GET/animal？type = dog&id = 3&process = True HTTP/1.1
GET/animal？type = dog&id = 4&process = False HTTP/1.1
GET/animal？type = dog&id = 5&process = True HTTP/1.1
GET/animal？type = dog&id = 6&process = False HTTP/1.1
GET/animal？type = dog&id = 7&process = True HTTP/1.1
GET/animal？type = dog&id = 8&process = False HTTP/1.1
GET/animal？type = dog&id = 9&process = False HTTP/1.1**

持久化的转换由“@”符号表示，转换函数总是以`**per**_`开始。这是因为这些转换不是迭代的，它们不创建测试或者保持状态。这些转换只是简单的转换，您可以在有效负载中的任何地方应用它们进行无状态转换，而不会影响有状态转换。由于它们没有规定任何测试，您不能单独用持久化转换生成测试，它们意味着与迭代转换混合。在上面的例子中，我们有一个 10 测试 snipe 风格的转换，放置一个递增的 id。此外，我们有一个持久的转换，把一个随机布尔到它的位置。

**例 5:使用 state 和 state.init**

可能存在这样的情况，在测试序列开始之前，测试者可能想要执行一些处理/初始化。为了支持这一点，Haptyc 在执行测试生成的转换之前，执行初始化阶段的所有相关转换。该初始化步骤可用于执行测试人员要求的任何初始化，并将其放入状态对象中。为此，测试人员可以使用`**state.init**`作为布尔值来确定执行是否在初始化中。初始化步骤返回的任何数据都将被忽略。

**原始有效载荷**

**获得/动物？data =[+b64**mutate]sgvsbg8gsgfja 2 vyiq = =[+end]HTTP/1.1

**Haptyc 类& Haptyc 变换**

**from hap tyc import *
import base 64
original = " GET/animal？data =[+b64 mutate]sgvsbg8gsgfja 2 vyiq = =[+end]HTTP/1.1 "
类 TestLogic(Transform):
@ apply operation(10)
def test _ b64 mutate(self，data，state):
if state . init:
state . decoded = base64 . b64 decode(data)
return
return base64 . b64 encode(random _ insert(state . decoded，[" '))**

**测试生成**

**获得/动物？data = sgvsbg 8 gscdhy 2 tlcie = HTTP/1.1
GET/animal？data = sgvsbg8gsgfja 2 vyisc = HTTP/1.1
GET/animal？data = SGVsbG8gSGFjaydlciE = HTTP/1.1
GET/animal？data = sgvsbg 8 gsgeny 2 tlcie = HTTP/1.1
GET/animal？data = scdlbgxviehhy2tl CIE = HTTP/1.1
GET/animal？data = SGVsbG8gSGFjaydlciE = HTTP/1.1
GET/animal？data = sgvsbg8gsgfja 2 vyisc = HTTP/1.1
GET/animal？data = SCdlbGxvIEhhY2tlciE = HTTP/1.1
GET/animal？data = sgvsbg8gsgfjj 2 tlcie = HTTP/1.1
GET/animal？data = sgvsbg8gsgfjj 2 tlcie = HTTP/1.1**

在上面的例子中，测试在测试序列的开始使用`**state.init**`对包装的内部负载进行 base64 解码，并将结果存储到`**state.decoded**`中。然后对于所有正常的测试生成执行 **`state.decoded`** 被用作待处理的解码内部数据。这种类型的模式有助于提高转换的性能，因为在开始时只进行一次解码(与每次测试生成时解码相同的有效载荷相比)。

**文档**

**标签类型**

*   `[**+tag]inner[+end]**`–狙击手风格的迭代变换
*   `**[%tag]inner[%end]**`–集群炸弹式迭代转换
*   `**[#tag]inner[#end]**`–电池/干草叉式迭代变换
*   `**[@tag]inner[@end]**`–无状态持久转换

**逻辑装饰家**

| 名字 | 争论 | `data`输入 | 描述 |
| --- | --- | --- | --- |
| @应用操作(n) | n=迭代次数 | haptyc 标记的内部值 | 以内部为数据生成 N 个测试的逻辑 |
| @ApplyRange(b，e，s=1) | b =开始值，e =最大值，s =步长 | 范围的生成值 | 为每个步进值生成测试的逻辑，步进值作为数据给出 |
| @ApplyList(L) | L = python 列表 | 清单上的项目 | 为作为数据给出的列表中的每个值生成测试的逻辑 |
| @ApplyFilelist(路径) | path =文件系统路径 | 清单上的项目 | 为作为数据给出的文件列表中的每个值生成测试的逻辑 |
| @ApplyPayloads(名称) | name =内置列表名称 | 清单上的项目 | 为作为数据给出的内置列表中的每个值生成测试的逻辑 |

**Haptyc 类装饰师**

| 名字 | 争论 | 描述 |
| --- | --- | --- |
| @CloneTransform(srcname，destname) | srcname =复制自的转换方法的字符串，destname =复制到的不存在的转换方法的字符串 | CloneTransform 用于将一个转换的实现复制到另一个名称空间，而不需要复制/粘贴。当您需要在多个位置重用同一个转换实现时，这在“%”和“#”风格的攻击中非常有用 |

**变换类助手方法**

| 名字 | 描述 |
| --- | --- |
| self.inner() | 检索标签的内部负载 |
| self.stop() | 将立即停止转换测试生成 |
| self.me() | 将返回当前转换上下文的名称 |
| self.set_label(标签) | 将设置当前测试的标签 |
| self.get_label(标签) | 将获得当前测试的标签 |

**变换辅助状态属性**

| 名字 | 描述 |
| --- | --- |
| 状态. iter | 转换的当前迭代计数(从 0 开始) |
| 状态初始化 | 指示是否处于初始化阶段的布尔值 |

**辅助突变功能**

| 名字 | 描述 |
| --- | --- |
| 拉丹(数据) | 该函数将对输入数据执行 radamsa 并返回结果(需要安装 radamsa) |
| index_insert(数据，列表，索引) | 该函数将把列表中的有效负载插入到所提供的索引处的数据中 |
| random_insert(数据，列表) | 这个函数将从列表中插入一个有效载荷到随机索引提供的数据中 |

**Bulitin Wordlists**

*   @ApplyPayloads("0-9 ")
*   @ApplyPayloads("10 个字母的单词")
*   @ApplyPayloads("11 个字母的单词")
*   @ApplyPayloads("12 个字母的单词")
*   @ApplyPayloads("3 个字母的单词")
*   @ApplyPayloads("4 个字母的单词")
*   @ApplyPayloads("5 个字母的单词")
*   @ApplyPayloads("6 个字母的单词")
*   @ApplyPayloads("7 个字母的单词")
*   @ApplyPayloads("8 个字母的单词")
*   @ApplyPayloads("9 个字母的单词")
*   @ApplyPayloads("a-z ")
*   @ApplyPayloads("CGI 脚本")
*   @ApplyPayloads("目录-长型")
*   @ApplyPayloads("目录–短")
*   @ApplyPayloads("dirsearch ")
*   @ apply payloads(" Extensions–long ")
*   @ apply payloads(" Extensions–short ")
*   @ApplyPayloads("文件名–长型")
*   @ApplyPayloads("文件名–短")
*   @ApplyPayloads("格式字符串")
*   @ApplyPayloads("表单字段名–long ")
*   @ApplyPayloads("表单字段名–短")
*   @ApplyPayloads("表单字段值")
*   @ ApplyPayloads(" Fuzzing–full ")
*   @ apply payloads(" Fuzzing–JSON _ XML injection ")
*   @ApplyPayloads("模糊-带外")
*   @ApplyPayloads("模糊化-路径遍历")
*   @ ApplyPayloads(" Fuzzing–路径遍历(单个文件)")
*   @ ApplyPayloads(" Fuzzing–quick ")
*   @ apply payloads(" Fuzzing–SQL 注入")
*   @ApplyPayloads("模糊化–模板注入")
*   @ apply payloads(" Fuzzing–XSS ")
*   @ApplyPayloads("HTTP 头")
*   @ApplyPayloads("HTTP 动词")
*   @ApplyPayloads("IIS 文件和目录")
*   @ApplyPayloads("有趣的文件和目录")
*   @ApplyPayloads("本地文件–Java ")
*   @ApplyPayloads("本地文件–Linux ")
*   @ApplyPayloads("本地文件–Windows ")
*   @ApplyPayloads("密码")
*   @ApplyPayloads("服务器端变量名")
*   @ApplyPayloads("短词")
*   @ApplyPayloads("SSRF 目标")
*   @ApplyPayloads("用户代理 long ")
*   @ApplyPayloads("用户代理-短")
*   @ApplyPayloads("用户名")

**如何安装**

有两种安装 Haptyc 的方法

*   使用这个库附带的版本`**turbo-intruder-all_w_haptyc.jar**`的简单方法
*   手动方式

无论你选择哪种方式，这些版本都不包括 radamsa，如果你想要 radamsa 支持，你必须从这个 repo 安装它:(可选)通过 https://gitlab.com/akihe/radamsa 安装 radamsa

**如何安装——预包装(简单)**

*   克隆此存储库，并在发布目录中注明`**turbo-intruder-all_w_haptyc.jar**`
*   开放式打嗝
*   转到扩展器选项卡
*   点击`**Add**`按钮
*   点击`**Select File ...**`按钮，选择`**turbo-intruder-all_w_haptyc.jar**`

**如何安装–手动(修补 turbo-intrusor-all . jar)**

*   克隆此回购
*   在 bash 中执行`**./install.sh <absolute directory with turbo-intruder-all.jar>**`
*   在打嗝重装涡轮入侵者

[**Download**](https://github.com/defparam/haptyc)