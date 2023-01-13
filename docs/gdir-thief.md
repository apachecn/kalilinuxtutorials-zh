# GDir-Thief:红队工具，用于通过谷歌的 API，渗透你有权访问的目标组织的谷歌人员目录

> 原文：<https://kalilinuxtutorials.com/gdir-thief/>

[![GDir-Thief : Red Team Tool For Exfiltrating The Target Organization’S Google People Directory That You Have Access To, Via Google’s API](img/1814f6cb5c65fb26b4086b15e00873e8.png "GDir-Thief : Red Team Tool For Exfiltrating The Target Organization’S Google People Directory That You Have Access To, Via Google’s API")](https://1.bp.blogspot.com/-MfKC5uPiwwQ/YObSvaoRb3I/AAAAAAAAJ6o/U8iRUO6INsE2LaSeXl3W8pnnhh_5XB_MQCLcBGAsYHQ/s760/gdir%2B%25281%2529.png)

GDir-Thief 是一个红队工具，用于通过 Google 的 People API，渗透您有权访问的目标组织的 Google People 目录。

**如何**

**创建新的谷歌云平台(GCP)项目**

获取连接到 API 所需的 Google API 访问令牌的步骤

*   创建一次性 gmail/google 帐户
*   登录到所述账户
*   导航至谷歌[云控制台](https://console.cloud.google.com/)
*   点击“谷歌云平台”旁边的`**Down arrow**`。将出现一个列出当前项目的对话框。
*   点击`**New Project**`。将出现“新建项目”屏幕。
*   在`**Project Name field**`中，输入项目的描述性名称。
*   (可选)要编辑`**Project ID**`，点击 **`Edit`** 。项目标识号在项目创建后不能更改，因此请选择一个满足项目生命周期需要的标识号。
*   点击`**Create**`。控制台导航到仪表板页面，您的项目在几分钟内就创建好了。

**启用 Google Workspace API**

*   在“Google Cloud Platform”旁边，点击`**Down arrow**`，从下拉列表中选择您刚刚创建的项目。
*   在左上角，点击`**Menu**` > `**APIs & Services**`。
*   点击`**Enable APIs and Services**`。出现`**Welcome to API Library**`页面。
*   在 **`search field`，**中输入“人”。
*   单击要启用的 API。将出现 API 页面。
*   点击`**Enable**`。将出现“概述”页面。

**配置 OAuth 同意屏幕**

*   在概览页面的左侧，点击`**Credentials**`。将出现项目的“凭据”页面。
*   点击`**Configure Consent Screen**`。出现“OAuth 同意屏幕”屏幕。
*   点击应用程序的`**External**`用户类型。
*   点击 **`Create`。**第二个“OAuth 同意屏幕”出现。
*   填写表格:
    *   在 **`App`** `name`字段中输入应用名称
    *   在`**User support email**`字段中输入您的一次性电子邮件地址。
    *   在`**Developer contact information**`字段中输入您的一次性电子邮件地址。
*   点击 **`Save and Continue`。**出现“范围”页面。
*   点击`**Add or Remove Scopes**`。将出现“更新所选范围”页面。
*   检查所有要在应用程序中使用的`**Google People**`范围。
*   点击`**Update**`。将显示应用程序的范围列表。
*   点击`**Save and Continue**`。将显示“编辑应用程序注册”页面。
*   点击`**Save and Continue**`。出现“OAuth 同意屏幕”。

**创建凭证**

*   点击`**Create Credentials**`，选择`**OAuth client ID**`。将出现“创建 OAuth 客户端 ID”页面。
*   点击应用类型下拉列表，选择`**Desktop Application**`。
*   在`**name**`字段中，输入凭证的名称。此名称仅显示在云控制台中。
*   点击`**Create**`。将出现 OAuth 客户端创建窗口。该屏幕显示了`**Client ID**`和`**Client secret**`。
*   点击`**OK**`。新创建的凭据出现在“OAuth 2.0 客户端 id”下
*   点击新创建的 OAuth 2.0 客户端 ID 右侧的`**download**`按钮。这会将客户端机密 JSON 文件复制到您的桌面上。记下该文件的位置。
*   将客户端机密 JSON 文件重命名为“credentials.json ”,并将其移动到`gdir_thief/credentials`目录。

**将受害者的谷歌账户添加到应用程序的测试用户中**

为了能够针对受害者运行这个脚本，您需要将他们的 Google 帐户添加到您刚刚创建的应用程序的测试用户列表中

*   在屏幕左侧点击`**OAuth consent screen**`。将显示“OAuth 同意屏幕”页面。
*   在`**Test Users**`下点击 **`Add Users`** 按钮。
*   在`**email address**`字段中输入 vicim 的 Gmail 地址。
*   点击`**save**`按钮。

**第一次运行 gdir_thief**

一旦获得目标的谷歌账户，你就可以运行 gdir_thief

*   第一次运行 gdir_thief 时，该脚本会打开一个新窗口，提示您授权访问您的数据:
    *   如果您尚未登录您的 Google 帐户，系统会提示您登录。如果您登录了多个 Google 帐户，系统会要求您选择一个帐户进行授权。确保你选择了受害者的谷歌账户

**依赖关系**

谷歌 API 库:`**pip install --upgrade google-api-python-client google-auth-httplib2 google-auth-oauthlib**`

**用途**

**用法:
python3 gdir_thief.py [-h]
帮助:
该模块将使用一个访问令牌连接到 Google 的 People API，并渗透组织的
人员目录。它将输出一个 CSV 文件到。/loot/directory.csv**

[**Download**](https://github.com/antman1p/GDir-Thief)