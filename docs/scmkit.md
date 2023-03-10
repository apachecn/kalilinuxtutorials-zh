# SCMKit:源代码管理攻击工具包

> 原文：<https://kalilinuxtutorials.com/scmkit/>

[![](img/8e0f6a377595c5a34afee56c819434ff.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEioXPLuSZu0eqODkxwuzkIJKIvu2mS2Eq3-eAIZot5SDWuMfZKeywLkph1zioji_Th-0ZWsLGIRdSX9r6Amdgx6GKeQODvn9vUnXmVaiwwZXuWoVVIM1AAqiztUk8mmbZ_P8_XnSFVCZ3Xtd5cD-8xTIK-BMFVkqP-E26w0TIxbrNPybATjW9AIjxi5/s728/SCMKit.png)

**源代码管理攻击工具包–SCM kit**是一个可以用来攻击 SCM 系统的工具包。SCMKit 允许用户指定要使用的 SCM 系统和攻击模块，以及指定相应 SCM 系统的有效凭证(用户名/密码或 API 密钥)。目前 SCMKit 支持的 SCM 系统有 GitHub Enterprise、GitLab Enterprise 和 Bitbucket Server。支持的攻击模块包括侦察、权限提升和持久性。SCMKit 采用模块化方法构建，因此信息安全社区可以在未来添加新的模块和 SCM 系统。

## 安装/建筑

### 使用的库

本项目中使用了以下第三方库。

| 图书馆 | 统一资源定位器 | 许可证 |
| --- | --- | --- |
| 八月号 | [https://github.com/octokit/octokit.net](https://github.com/octokit/octokit.net) | 带许可证 |
| 福迪雀 | [https://github.com/Fody/Fody](https://github.com/Fody/Fody) | 带许可证 |
| GitLabApiClient | [https://github.com/nmklotas/GitLabApiClient](https://github.com/nmklotas/GitLabApiClient) | 带许可证 |
| 纽顿软件。Json | [https://github.com/JamesNK/Newtonsoft.Json](https://github.com/JamesNK/Newtonsoft.Json) | 带许可证 |

### 预编译

*   在发行版中使用预编译的二进制文件

### 打造自己

采取以下步骤安装 Visual Studio，以便自己编译项目。这需要一个可以从 NuGet 包管理器安装的. NET 库。

*   加载 Visual Studio 项目，进入“工具”—>“获取包管理器”—>“包管理器设置”
*   转到“NuGet 包管理器”—>“包源”
*   添加 URL 为`https://api.nuget.org/v3/index.json`的包源
*   安装下面的 NuGet 包
    *   `Install-Package Costura.Fody -Version 3.3.3`
    *   `Install-Package Octokit`
    *   `Install-Package GitLabApiClient`
    *   `Install-Package Newtonsoft.Json`
*   您现在可以自己构建项目了！

## 用法

### 论据/选项

*   **-c，-凭证**-认证凭证(用户名:密码或 apiKey)
*   **-s，-system**-要攻击的系统(github，gitlab，bitbucket)
*   **-u，-url**–GitHub Enterprise、GitLab Enterprise 或 Bitbucket Server 的 URL
*   **-m，-模块**-要运行的模块
*   **-o，-选项**-选项(适用时)

### 系统(-s，-系统)

*   **github:** GitHub 企业
*   **gitlab:** GitLab 企业
*   **位桶:**位桶服务器

### 模块(-m，-模块)

*   **listrepo:** 列出当前用户可以看到的所有回购
*   **搜索回购:**搜索给定的回购
*   **searchcode:** 搜索包含关键字搜索词的代码
*   **searchfile:** 搜索包含关键字搜索词的文件名
*   **listsnippet:** 列出当前用户的所有片段
*   **listrunner:** 列出当前用户可用的所有 GitLab runners
*   **列表要点:**列出当前用户的所有要点
*   **listorg:** 列出当前用户所属的所有组织
*   **权限:**获取当前 API 令牌的权限
*   **添加管理员:**将给定用户提升为管理员角色
*   **removeadmin:** 将给定用户从管理员角色中降级
*   **createpat:** 为目标用户创建个人访问令牌
*   **listpat:** 列出目标用户的个人访问令牌
*   **removepat:** 删除目标用户的个人访问令牌
*   **创建 sshkey:** 为当前用户创建 sshkey
*   **listshkey:**列出当前用户的 SSH 密钥
*   **删除 sshkey:** 删除当前用户的 sshkey
*   **adminstats:** 获取管理统计数据(用户、回购、组织、gists)
*   **保护:**获取支路保护设置

### 模块详情表

下表显示了每个模块的支持位置

| 攻击场景 | 组件 | 需要管理员？ | GitHub 企业 | GitLab 企业 | 伺服器位元组 |
| --- | --- | --- | --- | --- | --- |
| 侦察 | `listrepo` | 不 | X | X | X |
| 侦察 | `searchrepo` | 不 | X | X | X |
| 侦察 | `searchcode` | 不 | X | X | X |
| 侦察 | `searchfile` | 不 | X | X | X |
| 侦察 | `listsnippet` | 不 |  | X |  |
| 侦察 | `listrunner` | 不 |  | X |  |
| 侦察 | `listgist` | 不 | X |  |  |
| 侦察 | `listorg` | 不 | X |  |  |
| 侦察 | `privs` | 不 | X | X |  |
| 侦察 | `protection` | 不 | X |  |  |
| 坚持 | `listsshkey` | 不 | X | X | X |
| 坚持 | `removesshkey` | 不 | X | X | X |
| 坚持 | `createsshkey` | 不 | X | X | X |
| 坚持 | `listpat` | 不 |  | X | X |
| 坚持 | `removepat` | 不 |  | X | X |
| 坚持 | `createpat` | 是(仅限 GitLab Enterprise) |  | X | X |
| 权限提升 | `addadmin` | 是 | X | X | X |
| 权限提升 | `removeadmin` | 是 | X | X | X |
| 侦察 | `adminstats` | 是 | X |  |  |

## 例子

### 列出休息时间

#### 使用案例

*发现特定 SCM 系统中使用的存储库*

#### 语法

提供`listrepo`模块，以及任何相关的认证信息和 URL。这将输出存储库名称和 URL。

##### GitHub 企业

这将列出用户可以看到的所有存储库。

`SCMKit.exe -s github -m listrepo -c userName:password -u https://github.something.local`

`SCMKit.exe -s github -m listrepo -c apiKey -u https://github.something.local`

##### GitLab 企业

这将列出用户可以看到的所有存储库。

`SCMKit.exe -s gitlab -m listrepo -c userName:password -u https://gitlab.something.local`

`SCMKit.exe -s gitlab -m listrepo -c apiKey -u https://gitlab.something.local`

##### 比特巴克服务器

这将列出用户可以看到的所有存储库。

`SCMKit.exe -s bitbucket -m listrepo -c userName:password -u https://bitbucket.something.local`

`SCMKit.exe -s bitbucket -m listrepo -c apiKey -u https://bitbucket.something.local`

#### 示例输出

```
C:\>SCMKit.exe -s gitlab -m listrepo -c username:password -u https://gitlab.hogwarts.local

==================================================
Module:         listrepo
System:         gitlab
Auth Type:      Username/Password
Options:
Target URL:     https://gitlab.hogwarts.local

Timestamp:      1/14/2022 8:30:47 PM
==================================================

                                    Name | Visibility |                                                URL
----------------------------------------------------------------------------------------------------------
                            MaraudersMap |    Private | https://gitlab.hogwarts.local/hpotter/maraudersmap
                            testingStuff |   Internal | https://gitlab.hogwarts.local/adumbledore/testingstuff
                               Spellbook |   Internal |    https://gitlab.hogwarts.local/hpotter/spellbook
       findShortestPathToGryffindorSword |   Internal | https://gitlab.hogwarts.local/hpotter/findShortestPathToGryffindorSword
                                  charms |     Public |      https://gitlab.hogwarts.local/hgranger/charms
                           Secret-Spells |   Internal | https://gitlab.hogwarts.local/adumbledore/secret-spells
                              Monitoring |   Internal | https://gitlab.hogwarts.local/gitlab-instance-10590c85/Monitoring

```

### 搜索休息

#### 使用案例

*在特定的 SCM 系统中按存储库名称搜索存储库*

#### 语法

在`-o`命令行开关中提供`searchrepo`模块和您的搜索标准，以及任何相关的认证信息和 URL。这将输出匹配的存储库名称和 URL。

##### GitHub 企业

GitHub 回购搜索是一个“包含”搜索，您输入的字符串将搜索名称包含您的搜索词的回购。

`SCMKit.exe -s github -m searchrepo -c userName:password -u https://github.something.local -o "some search term"`

`SCMKit.exe -s github -m searchrepo -c apikey -u https://github.something.local -o "some search term"`

##### GitLab 企业

GitLab 回购搜索是一个“包含”搜索，您输入的字符串将搜索名称包含您的搜索词的回购。

`SCMKit.exe -s gitlab -m searchrepo -c userName:password -u https://gitlab.something.local -o "some search term"`

`SCMKit.exe -s gitlab -m searchrepo -c apikey -u https://gitlab.something.local -o "some search term"`

##### 比特巴克服务器

Bitbucket repo 搜索是一种“开头为”的搜索，您输入的字符串将搜索名称以您的搜索词开头的回购。

`SCMKit.exe -s bitbucket -m searchrepo -c userName:password -u https://bitbucket.something.local -o "some search term"`

`SCMKit.exe -s bitbucket -m searchrepo -c apikey -u https://bitbucket.something.local -o "some search term"`

#### 示例输出

```
C:\>SCMKit.exe -s gitlab -m searchrepo -c apiKey -u https://gitlab.hogwarts.local -o "spell"

==================================================
Module:         searchrepo
System:         gitlab
Auth Type:      API Key
Options:        spell
Target URL:     https://gitlab.hogwarts.local

Timestamp:      1/14/2022 8:32:30 PM
==================================================

                                    Name | Visibility |                                                URL
----------------------------------------------------------------------------------------------------------
                               Spellbook |   Internal |    https://gitlab.hogwarts.local/hpotter/spellbook
                           Secret-Spells |   Internal | https://gitlab.hogwarts.local/adumbledore/secret-spells

```

### 搜索代码

#### 使用案例

*在特定的 SCM 系统中搜索包含给定关键字的代码*

#### 语法

在`-o`命令行开关中提供`searchcode`模块和您的搜索标准，以及任何相关的认证信息和 URL。这将输出匹配代码文件的 URL，以及匹配的代码行。

##### GitHub 企业

GitHub 代码搜索是一个“包含”搜索，您输入的字符串将搜索任何一行中包含您的搜索词的代码。

`SCMKit.exe -s github -m searchcode -c userName:password -u https://github.something.local -o "some search term"`

`SCMKit.exe -s github -m searchcode -c apikey -u https://github.something.local -o "some search term"`

##### GitLab 企业

GitLab 代码搜索是一个“包含”搜索，您输入的字符串将搜索任何一行中包含您的搜索词的代码。

`SCMKit.exe -s gitlab -m searchcode -c userName:password -u https://gitlab.something.local -o "some search term"`

`SCMKit.exe -s gitlab -m searchcode -c apikey -u https://gitlab.something.local -o "some search term"`

##### 比特巴克服务器

位桶代码搜索是一种“包含”搜索，其中您输入的字符串将搜索任何一行中包含您的搜索词的代码。

`SCMKit.exe -s bitbucket -m searchcode -c userName:password -u https://bitbucket.something.local -o "some search term"`

`SCMKit.exe -s bitbucket -m searchcode -c apikey -u https://bitbucket.something.local -o "some search term"`

#### 示例输出

```
C:\>SCMKit.exe -s gitlab -m searchcode -c username:password -u https://gitlab.hogwarts.local -o "api_key"

==================================================
Module:         searchcode
System:         gitlab
Auth Type:      Username/Password
Options:        api_key
Target URL:     https://gitlab.hogwarts.local

Timestamp:      1/14/2022 8:34:14 PM
==================================================

[>] URL: https://gitlab.hogwarts.local/adumbledore/secret-spells/stuff.txt
    |_ API_KEY=abc123

Total number of items matching code search: 1

```

### 搜索文件

#### 使用案例

*在特定的 SCM 系统中搜索文件名中包含给定关键字的存储库中的文件*

#### 语法

在`-o`命令行开关中提供`searchfile`模块和您的搜索标准，以及任何相关的认证信息和 URL。这将把 URL 输出到相应存储库中的匹配文件。

##### GitHub 企业

GitLab 文件搜索是“包含”搜索，您输入的字符串将搜索文件名中包含您的搜索词的文件。

`SCMKit.exe -s github -m searchfile -c userName:password -u https://github.something.local -o "some search term"`

`SCMKit.exe -s github -m searchfile -c apikey -u https://github.something.local -o "some search term"`

##### GitLab 企业

GitLab 文件搜索是“包含”搜索，您输入的字符串将搜索文件名中包含您的搜索词的文件。

`SCMKit.exe -s gitlab -m searchfile -c userName:password -u https://gitlab.something.local -o "some search term"`

`SCMKit.exe -s gitlab -m searchfile -c apikey -u https://gitlab.something.local -o "some search term"`

##### 比特巴克服务器

Bitbucket 文件搜索是一种“包含”搜索，您输入的字符串将搜索文件名中包含您的搜索词的文件。

`SCMKit.exe -s bitbucket -m searchfile -c userName:password -u https://bitbucket.something.local -o "some search term"`

`SCMKit.exe -s bitbucket -m searchfile -c apikey -u https://bitbucket.something.local -o "some search term"`

#### 示例输出

```
 C:\source\SCMKit\SCMKit\bin\Release>SCMKit.exe -s bitbucket -m searchfile -c apikey -u http://bitbucket.hogwarts.local:7990 -o jenkinsfile

==================================================
Module:         searchfile
System:         bitbucket
Auth Type:      API Key
Options:        jenkinsfile
Target URL:     http://bitbucket.hogwarts.local:7990

Timestamp:      1/14/2022 10:17:59 PM
==================================================

[>] REPO: http://bitbucket.hogwarts.local:7990/scm/~HPOTTER/hpotter
    [>] FILE: Jenkinsfile

[>] REPO: http://bitbucket.hogwarts.local:7990/scm/STUD/cred-decryption
    [>] FILE: subDir/Jenkinsfile

Total matching results: 2 
```

### 列出片段

#### 用例

> *在 GitLab 中列出当前用户拥有的代码片段*

#### 句法

提供`listsnippet`模块，以及任何相关的认证信息和 URL。

##### GitLab 企业

`SCMKit.exe -s gitlab -m listsnippet -c userName:password -u https://gitlab.something.local`

`SCMKit.exe -s gitlab -m listsnippet -c apikey -u https://gitlab.something.local`

#### 示例输出

```
 C:\>SCMKit.exe -s gitlab -m listsnippet -c username:password -u https://gitlab.hogwarts.local

==================================================
Module:         listsnippet
System:         gitlab
Auth Type:      Username/Password
Options:
Target URL:     https://gitlab.hogwarts.local

Timestamp:      1/14/2022 9:17:36 PM
==================================================

               Title |                                                                Raw URL
---------------------------------------------------------------------------------------------
        spell-script |                         https://gitlab.hogwarts.local/-/snippets/2/raw 
```

### 列出跑步者

#### 用例

> *列出 GitLab 中当前用户可用的所有 GitLab 跑步者*

#### 句法

提供`listrunner`模块，以及任何相关的认证信息和 URL。如果用户是管理员，您将能够列出 GitLab 企业实例中的所有运行者，包括共享和组运行者。

##### GitLab 企业

`SCMKit.exe -s gitlab -m listrunner -c userName:password -u https://gitlab.something.local`

`SCMKit.exe -s gitlab -m listrunner -c apikey -u https://gitlab.something.local`

#### 示例输出

```
 C:\>SCMKit.exe -s gitlab -m listrunner -c username:password -u https://gitlab.hogwarts.local

==================================================
Module:         listrunner
System:         gitlab
Auth Type:      Username/Password
Options:
Target URL:     https://gitlab.hogwarts.local

Timestamp:      1/25/2022 11:40:08 AM
==================================================

   ID |                 Name |                                      Repo Assigned
---------------------------------------------------------------------------------
    2 |        gitlab-runner | https://gitlab.hogwarts.local/hpotter/spellbook.git
    3 |        gitlab-runner | https://gitlab.hogwarts.local/hpotter/maraudersmap.git 
```

### 列表列表

#### 用例

> *在 GitHub 中列出当前用户拥有的列表*

#### 句法

提供`listgist`模块，以及任何相关的认证信息和 URL。

##### GitHub 企业

`SCMKit.exe -s github -m listgist -c userName:password -u https://github.something.local`

`SCMKit.exe -s github -m listgist -c apikey -u https://github.something.local`

#### 示例输出

```
 C:\>SCMKit.exe -s github -m listgist -c username:password -u https://github-enterprise.hogwarts.local

==================================================
Module:         listgist
System:         github
Auth Type:      Username/Password
Options:
Target URL:     https://github-enterprise.hogwarts.local

Timestamp:      1/14/2022 9:43:23 PM
==================================================

                             Description | Visibility |                                                URL
----------------------------------------------------------------------------------------------------------
            Shell Script to Decode Spell |     public | https://github-enterprise.hogwarts.local/gist/c11c6bb3f47fe67183d5bc9f048412a1 
```

### 器官列表

#### 用例

> *在 GitHub 中列出当前用户所属的所有组织*

#### 句法

提供`listorg`模块，以及任何相关的认证信息和 URL。

##### GitHub 企业

`SCMKit.exe -s github -m listorg -c userName:password -u https://github.something.local`

`SCMKit.exe -s github -m listorg -c apiKey -u https://github.something.local`

#### 示例输出

```
 C:\>SCMKit.exe -s github -m listorg -c username:password -u https://github-enterprise.hogwarts.local

==================================================
Module:         listorg
System:         github
Auth Type:      Username/Password
Options:
Target URL:     https://github-enterprise.hogwarts.local

Timestamp:      1/14/2022 9:44:48 PM
==================================================

                          Name |                                                URL
-----------------------------------------------------------------------------------
                      Hogwarts | https://github-enterprise.hogwarts.local/api/v3/orgs/Hogwarts/repos 
```

### 获取 API 令牌的权限

#### 用例

> *获取特定 SCM 系统中使用的访问令牌的分配权限*

#### 句法

提供`privs`模块，以及 API 键和 URL。

##### GitHub 企业

`SCMKit.exe -s github -m privs -c apiKey -u https://github.something.local`

##### GitLab 企业

`SCMKit.exe -s gitlab -m privs -c apiKey -u https://gitlab.something.local`

#### 示例输出

```
 C:\>SCMKit.exe -s gitlab -m privs -c apikey -u https://gitlab.hogwarts.local

==================================================
Module:         privs
System:         gitlab
Auth Type:      API Key
Options:
Target URL:     https://gitlab.hogwarts.local

Timestamp:      1/14/2022 9:18:27 PM
==================================================

          Token Name |    Active? |            Privilege |                                                            Description
---------------------------------------------------------------------------------------------------------------------------------
  hgranger-api-token |       True |                  api | Read-write for the complete API, including all groups and projects, the Container Registry, and the Package Registry.
  hgranger-api-token |       True |            read_user | Read-only for endpoints under /users. Essentially, access to any of the GET requests in the Users API.
  hgranger-api-token |       True |             read_api | Read-only for the complete API, including all groups and projects, the Container Registry, and the Package Registry.
  hgranger-api-token |       True |      read_repository |                      Read-only (pull) for the repository through git clone.
  hgranger-api-token |       True |     write_repository | Read-write (pull, push) for the repository through git clone. Required for accessing Git repositories over HTTP when 2FA is enabled. 
```

### 添加管理员

#### 用例

> *将普通用户提升为特定 SCM 系统中的管理角色*

#### 句法

提供`addadmin`模块，以及任何相关的认证信息和 URL。此外，提供您要向其添加管理角色的目标用户。

##### GitHub 企业

`SCMKit.exe -s github -m addadmin -c userName:password -u https://github.something.local -o targetUserName`

`SCMKit.exe -s github -m addadmin -c apikey -u https://github.something.local -o targetUserName`

##### GitLab 企业

`SCMKit.exe -s gitlab -m addadmin -c userName:password -u https://gitlab.something.local -o targetUserName`

`SCMKit.exe -s gitlab -m addadmin -c apikey -u https://gitlab.something.local -o targetUserName`

##### 伺服器位元组

仅支持用户名/密码身份验证来执行与 Bitbucket 中的回购或项目无关的操作。

`SCMKit.exe -s bitbucket -m addadmin -c userName:password -u https://bitbucket.something.local -o targetUserName`

#### 示例输出

```
 C:\>SCMKit.exe -s gitlab -m addadmin -c apikey -u https://gitlab.hogwarts.local -o hgranger

==================================================
Module:         addadmin
System:         gitlab
Auth Type:      API Key
Options:        hgranger
Target URL:     https://gitlab.hogwarts.local

Timestamp:      1/14/2022 9:19:32 PM
==================================================

[+] SUCCESS: The hgranger user was successfully added to the admin role. 
```

### 远程管理

#### 用例

> *将特定 SCM 系统中的管理用户降级为普通用户角色*

#### 句法

提供`removeadmin`模块，以及任何相关的认证信息和 URL。此外，提供您要从中删除管理角色的目标用户。

##### GitHub 企业

`SCMKit.exe -s github -m removeadmin -c userName:password -u https://github.something.local -o targetUserName`

`SCMKit.exe -s github -m removeadmin -c apikey -u https://github.something.local -o targetUserName`

##### GitLab 企业

`SCMKit.exe -s gitlab -m removeadmin -c userName:password -u https://gitlab.something.local -o targetUserName`

`SCMKit.exe -s gitlab -m removeadmin -c apikey -u https://gitlab.something.local -o targetUserName`

##### 伺服器位元组

仅支持用户名/密码身份验证来执行与 Bitbucket 中的回购或项目无关的操作。

`SCMKit.exe -s bitbucket -m removeadmin -c userName:password -u https://bitbucket.something.local -o targetUserName`

#### 示例输出

```
 C:\>SCMKit.exe -s gitlab -m removeadmin -c username:password -u https://gitlab.hogwarts.local -o hgranger

==================================================
Module:         removeadmin
System:         gitlab
Auth Type:      Username/Password
Options:        hgranger
Target URL:     https://gitlab.hogwarts.local

Timestamp:      1/14/2022 9:20:12 PM
==================================================

[+] SUCCESS: The hgranger user was successfully removed from the admin role. 
```

### 创建访问令牌

#### 用例

> *创建在特定 SCM 系统中使用的访问令牌*

#### 句法

提供`createpat`模块，以及任何相关的认证信息和 URL。此外，提供要为其创建访问令牌的目标用户。

##### GitLab 企业

这只能以管理员身份执行。您将提供想要为其创建 PAT 的用户名。

`SCMKit.exe -s gitlab -m createpat -c userName:password -u https://gitlab.something.local -o targetUserName`

`SCMKit.exe -s gitlab -m createpat -c apikey -u https://gitlab.something.local -o targetUserName`

##### 伺服器位元组

为验证为的当前用户创建 PAT。在 Bitbucket 中，您不能为其他用户创建 PAT，即使是作为管理员。仅支持用户名/密码身份验证来执行与 Bitbucket 中的回购或项目无关的操作。记下创建后显示的 PAT ID。当您将来需要删除 PAT 时，您将需要它。

`SCMKit.exe -s bitbucket -m createpat -c userName:password -u https://bitbucket.something.local`

#### 示例输出

```
 C:\>SCMKit.exe -s gitlab -m createpat -c username:password -u https://gitlab.hogwarts.local -o hgranger

==================================================
Module:         createpat
System:         gitlab
Auth Type:      Username/Password
Options:        hgranger
Target URL:     https://gitlab.hogwarts.local

Timestamp:      1/20/2022 1:51:23 PM
==================================================

   ID |         Name |                          Token
-----------------------------------------------------
   59 | SCMKIT-AaCND |           R3ySx_8HUn6UQ_6onETx

[+] SUCCESS: The hgranger user personal access token was successfully added. 
```

### 列出访问令牌

#### 用例

> *列出用户在特定 SCM 系统上的访问令牌*

#### 句法

提供`listpat`模块，以及任何相关的认证信息和 URL。

##### GitLab 企业

如果您想列出另一个用户的 PAT，只需要 admin。普通用户可以列出自己的 PAT。

`SCMKit.exe -s gitlab -m listpat -c userName:password -u https://gitlab.something.local -o targetUser`

`SCMKit.exe -s gitlab -m listpat -c apikey -u https://gitlab.something.local -o targetUser`

##### 伺服器位元组

列出当前用户的访问令牌。仅支持用户名/密码身份验证来执行与 Bitbucket 中的回购或项目无关的操作。

`SCMKit.exe -s bitbucket -m listpat -c userName:password -u https://bitbucket.something.local`

列出另一个用户的访问令牌(需要管理员)。仅支持用户名/密码身份验证来执行与 Bitbucket 中的回购或项目无关的操作。

`SCMKit.exe -s bitbucket -m listpat -c userName:password -u https://bitbucket.something.local -o targetUser`

#### 示例输出

```
 C:\>SCMKit.exe -s gitlab -m listpat -c username:password -u https://gitlab.hogwarts.local -o hgranger

==================================================
Module:         listpat
System:         gitlab
Auth Type:      Username/Password
Options:        hgranger
Target URL:     https://gitlab.hogwarts.local

Timestamp:      1/20/2022 1:54:41 PM
==================================================

   ID |                 Name |    Active? |                                             Scopes
----------------------------------------------------------------------------------------------
   59 |         SCMKIT-AaCND |       True |             api, read_repository, write_repository 
```

### 删除访问令牌

#### 用例

> *删除特定 SCM 系统中用户的访问令牌*

#### 句法

提供`removepat`模块，以及任何相关的认证信息和 URL。此外，提供要删除其访问令牌的目标用户 PAT ID。

##### GitLab 企业

仅当您想要删除另一个用户的 PAT 时才需要管理员权限。普通用户可以删除自己的 PAT。您必须提供 PAT ID 才能删除。每当您创建 PAT 以及您列出 PAT 时，都会显示此 ID。

`SCMKit.exe -s gitlab -m removepat -c userName:password -u https://gitlab.something.local -o patID`

`SCMKit.exe -s gitlab -m removepat -c apikey -u https://gitlab.something.local -o patID`

##### 伺服器位元组

仅支持用户名/密码身份验证来执行与 Bitbucket 中的回购或项目无关的操作。您必须提供 PAT ID 才能删除。每当您创建 PAT 时，都会显示该 ID。

`SCMKit.exe -s bitbucket -m removepat -c userName:password -u https://bitbucket.something.local -o patID`

#### 示例输出

```
 C:\>SCMKit.exe -s gitlab -m removepat -c apikey -u https://gitlab.hogwarts.local -o 58

==================================================
Module:         removepat
System:         gitlab
Auth Type:      API Key
Options:        59
Target URL:     https://gitlab.hogwarts.local

Timestamp:      1/20/2022 1:56:47 PM
==================================================

[*] INFO: Revoking personal access token of ID: 59

[+] SUCCESS: The personal access token of ID 59 was successfully revoked. 
```

### 创建 SSH 密钥

#### 用例

> *创建一个用于特定 SCM 系统的 SSH 密钥*

#### 句法

提供`createsshkey`模块，以及任何相关的认证信息和 URL。

##### GitHub 企业

为验证为的当前用户创建 SSH 密钥。

`SCMKit.exe -s github -m createsshkey -c userName:password -u https://github.something.local -o "ssh public key"`

`SCMKit.exe -s github -m createsshkey -c apiToken -u https://github.something.local -o "ssh public key"`

##### GitLab 企业

为验证为的当前用户创建 SSH 密钥。记下创建后显示的 SSH 密钥 ID。当您将来需要删除 SSH 密钥时，您将需要它。

`SCMKit.exe -s gitlab -m createsshkey -c userName:password -u https://gitlab.something.local -o "ssh public key"`

`SCMKit.exe -s gitlab -m createsshkey -c apiToken -u https://gitlab.something.local -o "ssh public key"`

##### 伺服器位元组

为验证为的当前用户创建 SSH 密钥。仅支持用户名/密码身份验证来执行与 Bitbucket 中的回购或项目无关的操作。记下创建后显示的 SSH 密钥 ID。当您将来需要删除 SSH 密钥时，您将需要它。

`SCMKit.exe -s bitbucket -m createsshkey -c userName:password -u https://bitbucket.something.local -o "ssh public key"`

#### 示例输出

```
 C:\>SCMKit.exe -s bitbucket -m createsshkey -c username:password -u https://bitbucket.hogwarts.local -o "ssh-rsa..."

==================================================
Module:         createsshkey
System:         bitbucket
Auth Type:      Username/Password
Options:        ssh-rsa ...
Target URL:     http://bitbucket.hogwarts.local:7990

Timestamp:      2/7/2022 1:02:31 PM
==================================================

  SSH Key ID
------------
          16

[+] SUCCESS: The hpotter user SSH key was successfully added. 
```

### 列出 SSH 密钥

#### 用例

> *列出特定 SCM 系统用户的 SSH 密钥*

#### 句法

提供`listsshkey`模块，以及任何相关的认证信息和 URL。

##### GitHub 企业

列出当前用户的 SSH 密钥。这将包括 SSH 密钥 ID，当您想要删除 SSH 密钥时需要它。

`SCMKit.exe -s github -m listsshkey -c userName:password -u https://github.something.local`

`SCMKit.exe -s github -m listsshkey -c apiToken -u https://github.something.local`

##### GitLab 企业

列出当前用户的 SSH 密钥。

`SCMKit.exe -s gitlab -m listsshkey -c userName:password -u https://gitlab.something.local`

`SCMKit.exe -s gitlab -m listsshkey -c apiToken -u https://gitlab.something.local`

##### 伺服器位元组

列出当前用户的 SSH 密钥。仅支持用户名/密码身份验证来执行与 Bitbucket 中的回购或项目无关的操作。

`SCMKit.exe -s bitbucket -m listsshkey -c userName:password -u https://bitbucket.something.local`

#### 示例输出

```
 C:\>SCMKit.exe -s gitlab -m listsshkey -u http://gitlab.hogwarts.local -c apiToken

==================================================
Module:         listsshkey
System:         gitlab
Auth Type:      API Key
Options:
Target URL:     https://gitlab.hogwarts.local

Timestamp:      2/7/2022 4:09:40 PM
==================================================

  SSH Key ID |             SSH Key Value |                Title
---------------------------------------------------------------
           9 | .....p50edigBAF4lipVZkAM= |         SCMKIT-RLzie
          10 | .....vGJLPGHiTwIxW9i+xAs= |         SCMKIT-muFGU 
```

### 删除 SSH 密钥

#### 用例

> *删除特定 SCM 系统中用户的 SSH 密钥*

#### 句法

提供`removesshkey`模块，以及任何相关的认证信息和 URL。此外，提供要删除的目标用户 SSH 密钥 ID。

##### GitHub 企业

您必须提供 SSH 密钥 ID 才能删除。每当您列出 SSH 密钥时，都会显示这个 ID。

`SCMKit.exe -s github -m removesshkey -c userName:password -u https://github.something.local -o sshKeyID`

`SCMKit.exe -s github -m removesshkey -c apiToken -u https://github.something.local -o sshKeyID`

##### GitLab 企业

您必须提供 SSH 密钥 ID 才能删除。每当创建 SSH 密钥时都会显示这个 ID，在列出 SSH 密钥时也会显示这个 ID。

`SCMKit.exe -s gitlab -m removesshkey -c userName:password -u https://gitlab.something.local -o sshKeyID`

`SCMKit.exe -s gitlab -m removesshkey -c apiToken -u https://gitlab.something.local -o sshKeyID`

##### 伺服器位元组

仅支持用户名/密码身份验证来执行与 Bitbucket 中的回购或项目无关的操作。您必须提供 SSH 密钥 ID 才能删除。每当创建 SSH 密钥时都会显示这个 ID，在列出 SSH 密钥时也会显示这个 ID。

`SCMKit.exe -s bitbucket -m removesshkey -c userName:password -u https://bitbucket.something.local -o sshKeyID`

#### 示例输出

```
 C:\>SCMKit.exe -s bitbucket -m removesshkey -u http://bitbucket.hogwarts.local:7990 -c username:password -o 16

==================================================
Module:         removesshkey
System:         bitbucket
Auth Type:      Username/Password
Options:        16
Target URL:     http://bitbucket.hogwarts.local:7990

Timestamp:      2/7/2022 1:48:03 PM
==================================================

[+] SUCCESS: The SSH key of ID 16 was successfully revoked. 
```

### 列出管理统计数据

#### 用例

> *在 GitHub Enterprise 中列出管理统计数据*

#### 句法

提供`adminstats`模块，以及任何相关的认证信息和 URL。使用该模块需要 GitHub Enterprise 中的站点管理员访问权限

##### GitHub 企业

`SCMKit.exe -s github -m adminstats -c userName:password -u https://github.something.local`

`SCMKit.exe -s github -m adminstats -c apikey -u https://github.something.local`

#### 示例输出

```
 C:\>SCMKit.exe -s github -m adminstats -c username:password -u https://github-enterprise.hogwarts.local

==================================================
Module:         adminstats
System:         github
Auth Type:      Username/Password
Options:
Target URL:     https://github-enterprise.hogwarts.local

Timestamp:      1/14/2022 9:45:50 PM
==================================================

     Admin Users |  Suspended Users |      Total Users
------------------------------------------------------
               1 |                0 |                5

     Total Repos |      Total Wikis
-----------------------------------
               4 |                0

      Total Orgs |   Total Team Members |      Total Teams
----------------------------------------------------------
               1 |                    0 |                0

   Private Gists |     Public Gists
-----------------------------------
               0 |                1 
```

### 列出分支保护

#### 用例

> *列出 GitHub 企业中的分支保护*

#### 句法

提供`protection`模块，以及任何相关的认证信息和 URL。或者，在 options 参数中提供一个字符串，以返回包含在 repo 名称中的匹配结果

##### GitHub 企业

`SCMKit.exe -s github -m protection -c userName:password -u https://github.something.local`

`SCMKit.exe -s github -m protection -c apikey -u https://github.something.local`

`SCMKit.exe -s github -m protection -c apikey -u https://github.something.local -o reponame`

#### 示例输出

```
C:\>.\SCMKit.exe -u http://github.hogwarts.local -s github -c apiToken -m protection -o public-r

==================================================
Module:         protection
System:         github
Auth Type:      API Key
Options:        public-r
Target URL:     http://github.hogwarts.local

Timestamp:      8/29/2022 2:02:42 PM
==================================================

                     Repo |                    Branch |                                         Protection
----------------------------------------------------------------------------------------------------------
              public-repo |                       dev | Protected: True
                                                        Status checks must pass before merge:
                                                          Branch must be up-to-date before merge: True
                                                        Owner review required before merge: True
                                                        Approvals required before merge: 2
                                                        Protections apply to repo admins: True
              public-repo |                      main | Protected: False 
```

[Click Here To Download](https://github.com/h4wkst3r/SCMKit)