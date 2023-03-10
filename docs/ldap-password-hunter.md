# LDAP-Password-Hunter:LDAP 臭名昭著的数据库中的密码猎人

> 原文：<https://kalilinuxtutorials.com/ldap-password-hunter/>

[![](img/7361676f0785e1a875e0bd1210819e3b.png)](https://blogger.googleusercontent.com/img/a/AVvXsEhhp5eStJkuMj9ofd0N6FBgUjQ3ZVKKP5ApSwImjEMcYg1MrZWPTx7QdsaRRov2Xw6L8mQDg2itZ_3iPGybugtXKtZh8dOxRoMz7vV9KXe_w0XjipboK0hmCidl0kgl9dVxS79722vZoY7CLvl9Io9CH3K-IUGnee0uQjAVacMlyNFwPcl2okVZ2GWx=s811)

**LDAP Password Hunter** 是一个工具，它包装了 getTGT.py (Impacket)和 ldapsearch 的特性，以便查找存储在 LDAP 数据库中的密码。Impacket getTGT.py 脚本用于验证用于枚举的域帐户，并保存其 TGT kerberos 票证。然后，TGT 票证被导出到 KRB5CCNAME 变量中，ldapsearch 脚本使用该变量来验证和获取运行 LDAP-Password-Hunter 的每个域/DC 的 TGS kerberos 票证。基于 CN=Schema，CN=Configuration 导出结果，构建并过滤自定义属性列表，以便识别可能包含感兴趣的结果的大查询。结果显示并保存在 sqlite3 数据库中。数据库由一个包含以下列的表组成:

*   DistinguishedName
*   AttributeName
*   价值
*   领域

结果比以前的版本更加清晰，并且组织在 SQL DB 中。输出只显示不在 DB 中的条目，因此会弹出新的条目，但是分析的总体结果仍然保存在带有时间戳的文件中。

# 要求

*   LDAP 搜索
*   冲击
*   Sqlite

## 用法

确保您的 krb5.conf 文件是干净的，并且 domains.txt 和 conf.txt 已正确填充。

从项目文件夹中:

**。/run.sh**

[**Download**](https://github.com/oldboy21/LDAP-Password-Hunter)