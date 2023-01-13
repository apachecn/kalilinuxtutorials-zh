# COM-Hunter : COM 劫持巫毒教

> 原文：<https://kalilinuxtutorials.com/com-hunter/>

[![](img/380ee88249ca106a6475d3ad2776d3fb.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjBYt0q6fFkeExo40Le23YpEesIl2Vytnx688vGuUM8eihot__CTvFl6cjEY2VVCnpKiSH1U5zr1Xsm0GE7RW0nmldT3JBwa9rUaY8gJOm6dm_FBwLISYuC-BS2bM9ksTWjGlMVuCWyiABZ4qJl7J3qZxY9VT-rjZMHONf4DDx6n-hdaaA8eLm-HAIq/s679/download.png)

**COM-hunter** 是一个用 C#编写的 COM 劫持持久化工具。

## 特征

*   在受害者的机器中找出条目有效的 CLSIDs。
*   通过受害者机器中的任务调度程序找出有效的 CLSIDs。
*   查明是否有人已经使用了这些有效的 CLSIDs 中的任何一个来实现 COM 持久性(LocalServer32/InprocServer32)。
*   查明某人是否已经通过任务计划程序使用任何有效的 CLSID 来进行 COM 持久性(LocalServer32/InprocServer32)。
*   尝试使用通用有效 clsid(local server 32/inprocserver 32)自动进行 COM 劫持持久性。
*   尝试通过任务计划程序自动执行 COM 劫持持久性。
*   尝试使用“TreatAs”键来引用不同的组件。

## 使用

**[+]用法:
。\COM-Hunter.exe
- >通用选项:
-h，–help 显示帮助并退出。
-v，–version 显示当前版本并退出。
-a，–关于显示工具的信息、积分和退出。
- >模式:
Search 搜索模式
Persist 持久模式
- >搜索模式:
Get-Entry 搜索有效的 CLSIDs 条目。
Get-Tasksch 通过任务调度器搜索有效的 CLSIDs 条目。
Find——如果有人已经使用了有效的 CLSID(defense ),则继续搜索。
Find-Tasksch 搜索是否有人已经通过任务调度程序使用了有效的 CLSID(防御)。
- >持久化模式:
General 使用通用方法在注册表中应用 COM 劫持持久化。
Tasksch 尝试通过任务调度器进行 COM 劫持持久化。
TreatAs 使用 TreatAs 注册表项在注册表中应用 COM 劫持持久性。
- >一般用法:
。\ COM-hunter . exe Persist General
->Tasksch 用法:
。\ COM-hunter . exe Persist tasks ch
->TreatAs 用法:
。\ COM-hunter . exe Persist TreatAs**

## 示例用法

*   获取条目(搜索模式):

**。\COM-Hunter.exe 搜索获取条目**

查找-保持(搜索模式):

**。\COM-Hunter.exe 搜索 Find-Persist**

常规(持续模式):

**。\ COM-hunter . exe Persist General ' HKCU:软件\类\ CLSID…' C:\ Users \ nickwourd \ Desktop \ beacon . dll**

## 有效 CLSIDs 的格式示例

**软件\类\CLSID。**..

**HKCU:软件\类\CLSID…**

**HKCU:\软件\类\CLSID…**

**HKCU \软件\类\CLSID…**

**HKEY _ 当前 _ 用户:软件\类\CLSID…**

**HKEY _ 当前 _ 用户:\软件\类\CLSID…**

**HKEY _ 当前 _ 用户\软件\类\CLSID…**

[**Download**](https://github.com/nickvourd/COM-Hunter)