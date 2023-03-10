# node XP——一个服务器端 Javascript 注入工具，能够检测和利用 Node.js 漏洞

> 原文：<https://kalilinuxtutorials.com/nodexp/>

**NodeXP** 是一个集成的工具，用 Python 2.7 编写，能够**检测 **Node.js** 服务上可能的漏洞**以及**以自动化的方式利用**它们，基于**S**(erver)**S**(ide)**J**(avascript)**I**(njection)攻击！

## **Nodexp 入门——安装&使用**

通过克隆 Git 存储库下载 NodeXP:

```
git clone https://github.com/esmog/nodexp
```

要获得所有选项的列表，请运行:

```
python2.7 nodexp -h
```

相应的 POST 和 GET 案例示例:

```
python2.7 nodexp.py --url="http://nodegoat.herokuapp.com/contributions" --pdata="preTax=[INJECT_HERE]" -c="connect.sid=s:i6fKU7kSLPX1l00WkOxDmEfncptcZP1v.fy9whjYW0fGAvbavzYSBz1C2ZhheDuQ1SU5qpgVzbTA"
python2.7 nodexp.py --url="http://nodegoat.herokuapp.com/contributions" --pdata="preTax=[INJECT_HERE]" -c="connect.sid=s:i6fKU7kSLPX1l00WkOxDmEfncptcZP1v.fy9whjYW0fGAvbavzYSBz1C2ZhheDuQ1SU5qpgVzbTA" --tech=blind

python2.7 nodexp.py --url="http://192.168.64.30/?name=[INJECT_HERE]" -c="connect.sid=s:i6fKU7kSLPX1l00WkOxDmEfncptcZP1v.fy9whjYW0fGAvbavzYSBz1C2ZhheDuQ1SU5qpgVzbTA"
python2.7 nodexp.py --url="http://192.168.64.30/?name=[INJECT_HERE]" -c="connect.sid=s:i6fKU7kSLPX1l00WkOxDmEfncptcZP1v.fy9whjYW0fGAvbavzYSBz1C2ZhheDuQ1SU5qpgVzbTA" --tech=blind
```

**也读[neo fetch——一个命令行系统信息工具](https://kalilinuxtutorials.com/neofetch/)**

## **设置和使用试验台**

为了熟悉 NodeXP，您可能需要设置所提供的 Node.js 测试服务(/testbeds)并开始使用该工具。需要一台运行 Node.js 服务器的本地计算机。

首先，你应该在 GET 和 POST 目录中安装“body-parser”和“express”包。

转到本地计算机上的“testbeds/GET”目录，将下面的命令粘贴到终端中:

```
npm install express --save
```

转到“testbeds/POST”目录，将以下命令粘贴到终端中:

```
npm install body-parser --save
nmp install express --save
```

在正确安装包之后，您可以通过运行命令“node”和所需的 js 文件(例如节点 eval.js)。

在您的服务器启动并运行之后，您就可以运行 NodeXP 并在这些服务上测试它了！

GET case 示例如下所示:

```
python2.7 nodexp.py --url=http://localiprunningnodejsserver:3001/?name=[INJECT_HERE]
```

如下所示的 POST 案例示例:

```
python2.7 nodexp.py --url=http://localiprunningnodejsserver:3001/post.js --pdata=username=[INJECT_HERE]
```

## **维护&更新有效载荷文件**

盲注和基于结果的注入技术所使用的有效载荷存储在“/files/blind_payloads.txt”和“/files/payloads.txt”中。

有效负载被写入文本文件的每一个奇数行，并且在基于结果的注入的情况下，它们的预期响应被写入“有效负载. txt”文件的每一个偶数行，作为用逗号分隔的列表。“blind_payloads.txt”文件的偶数行号为空。

为了停止注入过程，对于盲注入和基于结果的注入情况，“—end(nextline)—end”被用作能够停止解析和注入有效载荷的定界符。

每个用户都可以用自己的有效载荷来维护和更新有效载荷 txt 文件，只要她/他遵循上面的说明。

## **免责声明**

该工具的目的是严格的学术和开发，以进行我的硕士论文。在对 Node.js 服务进行渗透测试的过程中，这也很有帮助。强烈建议不要对该工具进行任何其他恶意或非法使用，这显然不是本次研究的目的。

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/esmog/nodexp)