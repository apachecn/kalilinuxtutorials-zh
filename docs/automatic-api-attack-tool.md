# 自动 API 攻击工具 2019

> 原文：<https://kalilinuxtutorials.com/automatic-api-attack-tool/>

[![Automatic API Attack Tool 2019](img/7490cd4fb7036d5a1e6a6db255f5afb1.png "Automatic API Attack Tool 2019")](https://1.bp.blogspot.com/-X7_A_eaLqbo/Xf_gilAYohI/AAAAAAAAEFg/EOZW5Y0BnecJ-Scmj2MSMuR75TtUUxpXgCLcBGAsYHQ/s1600/Automatic%2BAPI%2BAttack%2BTool%25281%2529.png)

**自动 API 攻击工具**是 imperva 的可定制 API 攻击工具，它将 API 规范作为输入，生成并运行基于它的攻击作为输出。

自动 API 攻击工具能够解析 API 规范，并根据 API 规范中定义的内容创建模糊攻击场景。在规范定义的范围内，每个端点被注入巧妙生成的值，在规范之外，发送适当的请求，并以详细的方式报告它们的成功或失败。您还可以扩展它来运行各种安全攻击媒介，如非法资源访问、XSS、SQLi 和 RFI，这些都是针对现有的端点，甚至是不存在的端点。不需要人工干预。只需运行工具并获得结果。

该工具可以轻松地进行扩展，以满足各种需求，例如，对于想要测试其 API 的开发人员，或者想要对其公共 API 运行定期漏洞或积极安全扫描的组织。它是在考虑 CI/CD 的情况下构建的。

**要求**

*   Java 8 或更高版本
*   Gradle

**运行中**

*   从 GitHub 检查代码并运行“gradle build”
*   您可以在 build/libs 文件夹下找到可执行文件 jar
*   运行“Java-jar imper va-API-attack-tool . jar”查看帮助菜单

**制作 Linux 可执行文件**

*   将 runnable.sh 文件从 src/main/resources 文件夹复制到 jar 文件所在的目录中。
*   现在运行:' cat runnable . sh imper va-API-attack-tool . jar > API-attack . sh & & chmod+x API-attack . sh '
*   您可以将 api-attack.sh 文件用作常规的可执行文件

**也可阅读-[PBTK:逆向工程工具集&模糊化基于 Protobuf 的应用](https://kalilinuxtutorials.com/pbtk-toolset-reverse-engineering-fuzzing-protobuf-based/)**

**用途**

##### 必需的参数:

**-f，–specFile =*specFile path***

> 要运行的 API 规范文件(swagger 2.0)。JSON/YAML 格式。为了获得更好的结果，请确保为每个端点都很好地定义了响应。

**-n，–主机名= *主机名***

> 要连接的主机名。也可以是 IP

**-s，–host scheme =*host scheme***

> 将使用此方案连接到主机；例如:https 或 http

##### 可选参数:

**-p，–主机端口= *主机端口***

> 主机监听 API 调用的端口，默认为:443

**-ph，–代理主机= *代理主机***

> 指定通过代理发送请求的代理主机

**-pp，–代理端口= *代理端口***

> 代理端口，默认为:80

**-rcn，–add negative ERC =*response code[，responseCode…]***

> 在负面攻击(如不良价值攻击)中接受的附加响应代码。支持多个值，用逗号分隔

**-rcp，–addPositiveRC =*response code[，responseCode…]***

> 正面检查中接受的附加响应代码(合法值攻击)。支持多个值，用逗号分隔

**典型使用场景**

*   您想要检查您的 API 是否受到 API 安全解决方案的保护。示例运行:`**api-attack.sh -f swaggerPetStore.json -n myapisite.com -s http -rcn=403**`我们添加了`403`响应代码作为否定检查的合法响应代码。这是因为 API 安全解决方案会阻止此类请求，并返回 403 状态。另一方面，该规范不一定为其任何端点定义 HTTP 代码为 403 的响应。这将使此类响应合法，尽管它们不在规范中，并在否定检查未收到此类响应时提醒您。这种情况意味着您没有受到 API 安全解决方案的保护。
*   您想要检查您的代理如何减轻 API 攻击，但是没有实际的站点支持它。示例运行:`**api-attack.sh -f swaggerPetStore.json -n myapisite.com -s http -ph 127.0.0.1 -pp=4010 -rcn=403 -rcp=404**`这次我们已经将`404`状态代码添加到正面场景中。因此，当场景没有被阻塞时，我们不会报告失败，而是接受合法的 **`404`** (未找到资源)响应。
*   您想要检查您的 API 是否正确处理了所有输入。此外，您希望在每晚的基础上运行它，或者甚至在每次开发人员向项目推送新代码之后运行它。示例运行:`**api-attack.sh -f myapi_swagger.yaml -n staging.myorg.com -s https**`这一次我们运行时没有任何排除。API 规范文件必须准确地声明其响应代码。该工具将只接受它们是合法的，否则检查将失败。有关检查失败的条件，请参见下文。在 Jenkins 作业(或您喜欢的任何其他 CI/CD 软件)中运行上述命令，这将由 cron 或 repo 代码推送活动触发。确保您已经安装了 **`TestNG`** 插件，该插件将解析用`**build/testng-results**`编写的结果，以便在 CI/CD 场景中有更好的可视性。
*   您想要检查这个 API 是否可能对 fuzzing 尝试开放。只需运行该工具并检查报告的故障。运行示例:`**api-attack.sh -f publiclyAvailableSwaggerOfAPI.yaml -n api.corporate.com -s https**`
*   您希望检查您的 API 是否在服务器端正确实现，或者它的定义是否与服务器实现相对应。运行示例:`**api-attack.sh -f publiclyAvailableSwaggerOfAPI.yaml -n api.corporate.com -s https**`

**检查失败的条件**

*   该工具验证生成的请求响应代码是否与 swagger 中声明的响应代码相匹配。然而，
*   肯定检查:如果这是一个明显的错误(代码是 5xx)，我们仍然会检查失败，即使这个响应代码没有在规范中定义，但是如果您提供了一个覆盖，就不会了。
*   否定检查:如果响应不是合法的错误(1xx、2xx、5xx)，我们将检查失败，除非您提供覆盖。如果合法的错误代码不在规范中，检查也会失败。
*   您可以在 swagger 的 response 部分使用“default”定义，但不建议这样做。总是精确地定义你的合法答案。

**检查失败的条件**

*   该工具验证生成的请求响应代码是否与 swagger 中声明的响应代码相匹配。然而，
*   肯定检查:如果这是一个明显的错误(代码是 5xx)，我们仍然会检查失败，即使这个响应代码没有在规范中定义，但是如果您提供了一个覆盖，就不会了。
*   否定检查:如果响应不是合法的错误(1xx、2xx、5xx)，则检查失败。除非你提供了超驰装置。如果合法的错误代码不在规范中，检查也会失败。
*   您可以在 swagger 的 response 部分使用“default”定义，但不建议这样做。总是精确地定义你的合法答案。

**预期产出**

*   该工具使用 testng 报告框架，因此任何处理 testng 运行的插件都可以在这里使用。只需注意结果是写在 build/testng-results 文件夹下的。当然，这是可以改变的。
*   该工具根据其检查套件生成请求，每个请求检查特定的内容。因此，每次检查都会在命令行输出中显示所有相关的详细信息，以及正在检查的内容、响应是什么，以及是否符合预期。
*   任何错误的请求都将存储在`bad_requests`文件夹中，以便您可以在以后对其进行分析(例如，如果它运行在 CI/CD 服务器上，并且您不能立即访问该机器)
*   最后，您将获得一份摘要

失败的否定检查示例:

**测试 API 端点
测试 ID: 1575128763286-74212
测试:错误属性:/username (STRING)，值:{，URL 编码:% 7B
–>URL:/user/{
–>方法:GET
–>Headers:[]
——-*——-
请求为:GET/user/{[Accept:application/JSON]，响应**

为什么检查失败了？该请求得到 200，即使不包含合法的 URL

另一个例子:

*测试 API 端点*
**测试 ID: 1575128763286-25078
测试:坏属性:/body/quantity(整数)，值:0.4188493，URL 编码:0.4188493
–>URL:/store/order
–>方法:POST
–>头:[]
–>Body**

服务器期望获得一个整数，但接受了一个双精度值。这可能是尝试利用服务器中的一些缓冲区溢出的好机会。

成功检查的示例:

**测试 API 端点
测试 ID: 1575128763137-43035
测试:/user/{ username }
–>Url:/user/% e 68 e 97 EDB 4 OQ-(！BbG，Y$p'A-KW%65f9FA6jt5vvDz-cW。QGsLS+AA~RIHC3wgy25lDJsGzcT。；kJ+(
–>方法:GET
–>头:[]
————*————
请求为:GET /user/%E68E97EDB4Oq-(！BbG，Y$p'A-KW%65f9FA6jt5vvDz-cW。QGsLS+AA~RIHC3wgy25lDJsGzcT。；kJ+( [Accept: application/json]，响应状态码:404
响应(未解析):
{"statusCode":404，" error ":"未找到"，" message ":"未找到" }**

根据 API 规范，我们提供了一个不存在但合法的用户名。服务器知道如何处理这个请求并返回一个合法的错误。

**支持的检查场景**

我们在这里将使用术语 **`endpoint`** ，作为端点 URL 和方法元组。

积极的情景

*   对于每个端点，使用为其所有参数生成的值创建请求。这些是随机生成的，但是遵守 API 规范中定义的规则。
*   对于每个端点，创建一个仅包含所需参数的请求，其值按上述方式生成。

负面情景

*   对于每个端点，创建多个请求，每个请求检查一个不同的参数。该工具通过在检查的参数中注入一个随机的错误输入值，并用“正”值填充其余的值来实现这一点，这些值是以与正场景中描述的相同方式生成的。

[**Download**](https://github.com/imperva/automatic-api-attack-tool)