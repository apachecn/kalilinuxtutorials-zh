# Gh-Dork : Github Dorking 工具

> 原文：<https://kalilinuxtutorials.com/gh-dork/>

[![](img/988cb94a41889621b5f6b6bbef9049ab.png)](https://blogger.googleusercontent.com/img/a/AVvXsEh9xr4Tcai7c787-XpOw_yPnNtHWUk4gzbY44qYilPeW2IbBSV4TDnM7A24rQm3y1IWBc0ku2bBUkY8jcbNAd0fEOR48hmU1qTxCfyB7QwW9DMDelxoECIBttWMAxUnEotEGl4XnFG9O5fUJc9rVrToNFGFHBoUJQtBMIGIUWiGkyPREieC1GU3iPWr=s728)

**Gh-Dork** 是一款 Github 的多机工具。提供一个呆瓜列表，并根据需要提供以下内容之一:

*   一个用户(`**-u**`)
*   包含用户列表的文件(`**-uf**`)
*   一个组织(`**-org**`)
*   带有组织列表的文件(`**-of**`)
*   回购(`**-r**`)

你也可以通过:

*   存储结果的输出目录(`**-o**`)
*   用于存储有效项目的文件名，如果您的用户或组织文件可能包含不存在的用户/组织(`**-vif**`)

所有输入文件(呆子、用户或组织)都应该换行。

**用法**

克隆存储库，然后运行`**pip install -r requirements.txt**`

唯一需要的参数是 dorks 文件(`**-d**`)。思路见 techguan 的 github-dorks.txt。

如果指定了一个输出目录，将为 dorks 列表中的每个 dorks 创建一个文件，结果将保存在那里并打印出来。仅使用空的/不存在的目录，否则它将被清除，其内容将被替换。

如果您的用户或组织文件还没有被过滤以删除不存在的用户/组织或没有任何公共代码的用户/组织，强烈建议您传入一个`**--valid-items-filename**` ( `**-vif**`)。这将在搜索第一个呆子时过滤掉任何无效的用户/组织，并避免搜索后续的呆子。然后，输出文件还可以用作输入用户/组织文件，以加速以后的脚本运行。

示例用法:

**python GH-dork . py-d dorks . txt #基本用法
python GH-dork . py-d dorks . txt-u Molly #搜索特定用户的 repos
python GH-dork . py-d dorks . txt-uf users . txt #搜索列表中所有用户的 repos
python GH-dork . py-d dorks . txt-uf users . txt-Vif valid _ users . txt #搜索列表中所有用户的 repos， 过滤掉不存在的用户
python GH-dork . py-d dorks . txt-org github #搜索特定组织的 repos
python GH-dork . py-d dorks . txt-搜索列表中所有组织的 repos
python GH-dork . py-d dorks . txt-of orgs . txt-Vif valid _ orgs . txt #搜索列表中所有组织的 repos，过滤掉不存在的组织
python GH-dorks**

**认证**

身份验证是通过环境变量完成的。您可以使用 Github 私有访问令牌(`**GH_TOKEN**`)或用户名和密码(`**GH_USER**`和`**GH_PASS**`)进行认证。如果启用了双因素身份验证，系统会提示您输入双因素代码。

您还可以传递一个 Github 企业基本 URL ( `**GH_URL**`)来搜索该 Github 实例；如果省略，这将与 github.com 背道而驰。

如果没有提供凭据或者凭据无效，脚本仍将运行，但会受到未经身份验证的用户的低得多的速率限制的限制。

[**Download**](https://github.com/molly/gh-dork)