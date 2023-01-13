# 一个概念验证的 WordPress 插件 Fuzzer

> 原文：<https://kalilinuxtutorials.com/wpgarlic/>

[![](img/1aee42196f24650e3009c8b203916cb4.png)](https://www.blogger.com/blog/post/edit/1980184639205218685/7009012641885962644?pli=1#)

WP 大蒜是一个概念验证的 WordPress 插件 fuzzer，在 https://kazet.cc/2022/02/03/fuzzing-wordpress-plugins.html 描述的研究中使用，帮助发现了安装在近 1500 万个网站上的 WordPress 插件中的 140 多个漏洞。

如果你想继续研究，从不太受欢迎的插件开始——如果一个插件在 2021 年 10 月到 2022 年 1 月之间实现了至少 10000 次活跃安装，我很可能已经看过 fuzzer 的报告了(大部分重点放在了至少 20000 次活跃安装的插件上)。因为 fuzzer 的工作方式有很大的随机性，这些插件中的一些漏洞仍未被发现——但数量较少。

Fuzzer 报告包含大量误报，其中大多数并不表示存在漏洞。看到报告后，首先分析您观察到的行为是漏洞还是误报。不要向 wps can/供应商发送原始模糊报告，而是提供概念验证漏洞。

## 例子

由于显而易见的原因，这些示例将只包含已经修复的漏洞。

### 任意文件读取

让我们假设你正在 6.4.0 版本中模糊化`**responsive-vector-maps**`:

**。/bin/fuzz _ plugin responsive-vector-maps–版本 6.4.0**

(要模糊最新版本，直接跳过`**--version**`)。

fuzzing 完成后(这个插件需要 10-30 分钟),你可以调用:

**。/bin/print _ 发现数据/plugin_fuzz_results/**

这意味着引信检测到在一个已知的有效载荷上执行`**fopen()**`。大多数有效载荷都包含单词`**GARLIC**`，以便在输出中自动检测。你可以在`**docker_image/magic_payloads.php**`中看到或配置它们。

然后，您可能会浏览源代码，看到`**wp_ajax_rvm_import_markers**`端点确实使用文件内容来呈现输出，从而允许您读取服务器上的任意文件:CVE-2021-24947。

你看到的白色部分是一个有趣的崩溃(你可以在`**crash_detectors.py**`中修改它们或者添加新的)。绿色是背景。蓝色显示的是报告文件名(带有插件名)、插件流行度和端点名(这里是 ajax 动作名)。

黄色的数据是什么样的有效载荷被注入了什么样的变量。

### 映 XSS

让我们假设你在版本 1.4.9.4 中模糊化`**page-builder-add**`:

**。/bin/fuzz_plugin 页面生成器-添加-版本 1.4.9.4**

导致存储 XSS 的选项更新

**。/bin/fuzz _ plugin duplicate-page-or-post-版本 1.4.6**

### 假阳性

不幸的是，对于大多数插件，fuzzer 没有发现任何有趣的崩溃，对于其余的，**大多数报告都是误报**。例如，如果您看到:

**调用:WP _ mail arguments = { ' to ':' Plugin @ Plugin vendor . com '，' subject ':[Plugin contact]–http://garlicgarlic 大蒜. example.com'}**

这可能意味着,`**wp_mail**`确实被调用了，但是你不能控制接收者和大部分主体。如果你想确定，看看插件源码。

### 阅读 fuzzer 报告的其他提示

*   如果看到消息；*也可以等于:……和……*——这意味着假设已知有效载荷等于任何其他字符串的机制(在 https://kazet . cc/2022/02/03/fuzzing-WordPress-plugins . html # patched-equality 中描述)被触发。
*   如果您看到`**__GARLIC_ACCESSED__ _FILES[files] __ENDGARLIC__**`–这意味着检测到上传的文件访问。目前没有进行进一步的检查–要检查这是否是一个漏洞，请查看代码。
*   有时 fuzzer 注入到 GET、POST 等中的内容。参数在现实世界中是不可复制的:例如，如果您想要显示一个特定的菜单页面，您不能向`**$_GET['page']**`中注入任何东西。

## 使用说明书

fuzzing 或测试的第一次运行可能需要大约一个小时，因为我们需要用工具 PHP 和 WordPress 构建 Docker 映像。

### 按名称模糊插件

**。/bin/fuzz_plugin PLUGIN_SLUG**

### 模糊化文件中的插件

您也可以从本地 zip 文件安装插件:

**。/bin/fuzz _ PLUGIN PLUGIN _ FILE _ name . zip**

### 打印结果

要打印 fuzzer 找到的内容，请使用:

。**/bin/print _ 发现数据/plugin_fuzz_results/**

### 运行测试

要运行测试，请使用:

**。/bin/test**

## 手动测试环境

您可以使用以下命令启动一个只安装了一个插件的测试环境:

**。/bin/manual _ testing PLUGIN _ SLUG | PLUGIN _ path . zip[版本]**

你可以使用插件的 slug 或者从本地 zip 文件安装插件。

它将侦听 http://127.0.0.1:8001/

数据库中将有两个测试用户:

*   用户名:管理员，密码:管理员，权限:管理员
*   用户名:订户，密码:订户，权限:订户

## 扩展和配置模糊器

该工具是一个概念验证工具—**本节包含可以改进的地方，以发现更多漏洞**。

你可能想要编辑`**filtering.py**`——它包含了认为一个特定的崩溃重要与否的规则。如果您更改它们，您可能会有更多的误报，但也会发现更多的漏洞。例如，我认为发出时唯一感兴趣的头是 Location 头，用于检测开放重定向漏洞。这只是一个想法，你可能还有其他想法。

另一个可能值得扩展的文件是`**docker_image/patch_wordpress.sh**`。它描述了将被记录为感兴趣的函数的调用。

如果你想注入其他有效载荷(或者改变它们被注入的概率)，编辑`**docker_image/magic_payloads.php**`和**T1。**

`**crash_detector.py**`包含发现有趣的崩溃或有趣的信息(如电子邮件)被暴露的正则表达式。

模糊文件(即执行每个注入有效载荷的 PHP 文件)已被禁用，因为它不会导致许多发现。取消对`**config.DEFAULT_ENABLED_FEATURES**`中的`**files**`的注释，以进行更改。

## 起毛器内部构件

### 黑名单

有些插件需要其他插件(如 woocommerce)作为依赖。当模糊一个有依赖关系的插件时，我们只想模糊选择的插件，跳过依赖 AJAX 动作、REST 路径和菜单页面。只有当我们选择 woocommerce 来模糊时，我们才希望模糊 woocommerce 操作/路线/页面。

依赖动作/路由/页面的列表称为阻止列表，列在`**docker_image/blocklists/**`中。名为`**common**`的文件包含了 WordPress 核心动作/路线/页面——我们不想混淆这些。

要更新这些黑名单，请使用`**./bin/update_blocklists**`。

[**Download**](https://github.com/kazet/wpgarlic)