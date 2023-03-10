# gokart:保护 Go 代码的静态分析工具

> 原文：<https://kalilinuxtutorials.com/gokart/>

[![](img/cfd13139fd5ea3d41f634ee9234c9dd3.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhHUbvHh1yPgVsBaE5lk1ij4wHvTFErIz7Ef8cou2WcSC_000yXZPwF2aq2zeGvMOxYaUnGapCNsmwYwX6R_MeslXtpxaEKYRoP3MUqteffIk-DXq3D3wKWamsMda4wUBms0fvn9B8EH7JINVkHxFQgXztRzDemnrkeOZyBfko2762nZ6yJ7ZQqJ-g9/s728/logo%20(2)%20(1).png)

**GoKart** 是一款针对 Go 的静态分析工具，使用 Go 源代码的 SSA (single static assignment)形式发现漏洞。它能够跟踪变量和函数参数的来源，以确定输入源是否安全，与其他 Go 安全扫描器相比，这减少了误报的数量。例如，一个与变量连接的 SQL 查询传统上可能被标记为 SQL 注入；但是，GoKart 可以计算出变量实际上是常数还是常数的等价物，在这种情况下就不存在漏洞。

GoKart 还帮助为 Praetorian 的安全平台**战车**提供动力，该平台可以帮助您发现、管理和修复源代码和云环境中的漏洞。Chariot 使得在你的源代码上运行自动的、连续的 GoKart 扫描变得简单。如果你想尝试 GoKart，你可以点击这里在几分钟内建立一个免费的战车帐户。

## 我们为什么建造 GoKart

静态分析是一种在源代码中寻找漏洞的强大技术。然而，这种方法存在噪音——也就是说，许多静态分析工具发现了相当多实际上并不存在的“漏洞”。这导致了开发人员的摩擦，因为用户厌倦了工具“狼来了”。

GoKart 的动机是为了解决这个问题:我们能否创造一种比现有工具假阳性率低得多的扫描仪？根据我们的实验，答案是肯定的。通过利用源到汇跟踪和 SSA，GoKart 能够跟踪变量赋值之间的变量污点，从而显著提高发现的准确性。我们的重点是可用性:实际上，这意味着我们已经优化了我们的方法来减少错误警报。

## 安装

您可以使用下面列出的任何一个选项在本地安装 GoKart。

### 用`**go install**`安装

**$去安装 github.com/praetorian-inc/gokart@latest**

### 安装一个发布二进制文件

*   从发布页面下载适用于您的操作系统的二进制文件。
*   (可选)下载`**checksums.txt**`文件以验证归档文件的完整性

## 入门–扫描示例应用程序

您可以按照下面的步骤在 Go Test Bench 上运行 GoKart，这是一个来自 Contrast Security 团队的故意易受攻击的 Go 应用程序

**克隆样本漏洞应用
git 克隆 https://github.com/Contrast-Security-OSS/go-test-bench.git
go kart 扫描 go-test-bench/**

输出应该显示一些已识别的漏洞，每个漏洞都有一个已识别的易受攻击的功能和用户输入源。

要测试一些额外的 GoKart 功能，您可以使用下面建议的 CLI 标志进行扫描。

**使用详细标志显示这些漏洞的完整踪迹
go kart scan go-test-bench/-v
使用 globalsTainted 标志忽略白名单来源
可能会增加误报结果
go kart scan go-test-bench/-v-g
使用调试标志显示对开发和调试有用的内部分析信息
go kart scan go-test-bench/-d
以 sarif 格式输出结果
go kart scan go-test-bench/- -o gokart-go-test-bench.txt
将 scarif 结果输出到文件
go kart Scan go-test-bench/-o go kart-go-test-bench . txt-s
扫描远程公共存储库
存储库将在本地克隆，扫描后删除
go kart Scan-r https://github.com/ShiftLeftSecurity/shiftleft-go-demo-v
指定要扫描的远程分支
go kart Scan-r https://github.com/ShiftLeftSecurity/shiftleft-go-demo-b actions _ fix
通过 ssh 扫描远程私有存储库 ssh/github_rsa_key
同时使用远程扫描和输出标志进行无缝安全审查
go kart scan-r https://github.com/ShiftLeftSecurity/shiftleft-go-demo-o go kart-shift left-go-demo . txt-v
使用远程扫描、输出和 sarif 标志进行无摩擦集成到 CI/CD 中
go kart scan-r https://github.com/ShiftLeftSecurity/shiftleft-go-demo-o go kart-shift left-go-demo . txt-s**

为了测试 GoKart 的可扩展性，您可以修改 GoKart 用来将新的易受攻击的接收器引入分析的配置文件。在`**util/analyzers.yml**`包含的默认配置文件中定义了一个测试接收器分析器。修改`**util/analyzers.yml**`以删除测试接收器分析器上的注释，然后指示 GoKart 使用带有`**-i**`标志的修改后的配置文件。

**使用修改后的 analyzer . yml 文件进行扫描并输出完整的轨迹
go kart Scan go-test-bench/-v-I/util/analyzer . yml**

输出现在应该包含其他漏洞，包括新的“用户输入可到达的测试接收器”漏洞。

[**Download**](https://github.com/praetorian-inc/gokart#install)