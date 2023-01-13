# 军械库—获取大量外部和发现数据的工具

> 原文：<https://kalilinuxtutorials.com/armory/>

Armory 是一个工具，用于从许多工具中获取大量外部和发现数据，将其添加到数据库中，并将所有相关信息关联起来。它并不意味着取代任何特定的工具。这意味着从各种工具获取输出，并使用它来为其他工具提供信息。

此外，它还应该易于扩展。没有看到您最喜欢的工具的模块？写一个上去！想要为您的报告导出正确格式的数据吗？创建新报告！

**也读作[Delta–SDN 安全评估&渗透测试框架](https://kalilinuxtutorials.com/delta-framework/)**

## **我**安斯塔军械库

**克隆回购:**

`**git clone https://github.com/depthsecurity/armory**`

**安装依赖项:**

`**pip install -r requirements**`

**现在设置配置:**

```
cd config
copy settings.ini.sample settings.ini
```

接下来编辑 **settings.ini** 并修改 **base_path** 选项。这应该指向您当前项目所使用的根路径。您应该在每个项目中更改这一点，这样您将始终使用一个干净的数据库。模块生成的所有文件都将在这里创建，sqlite3 数据库也是如此。

## **军械库的用法**

使用被分成**模块**和**报告**。

### **模块**

模块运行工具，接收输出，并将其写入数据库。要查看可用模块的列表，请键入:

`**./armory.py -lm**`

要查看模块选项列表，请键入:

**`./armory.py -m <module> -M`**

## **报道**

报告类似于模块，只是它们意味着从数据库中提取数据，并以可用的格式显示数据。要查看所有可用的报告:

`**./armory.py -lr**`

要查看可用的报告选项:

`./armory.py -r <report> -R`

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/depthsecurity/armory)