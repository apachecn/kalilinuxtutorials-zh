# OSSEM:开源安全事件元数据

> 原文：<https://kalilinuxtutorials.com/ossem-open-source-security-events-metadata/>

[![OSSEM : Open Source Security Events Metadata](img/b43ccd31210eb43a1f70c6632f0779dc.png "OSSEM : Open Source Security Events Metadata")](https://1.bp.blogspot.com/-dwiWdk4CECw/XpMjfP6wMvI/AAAAAAAAF3w/f7wpHM649UQDyiedSS-iZOBtcYCx9PovACLcBGAsYHQ/s1600/OSSEM%25281%2529.png)

**开源安全事件元数据(OSSEM)** 是一个由社区主导的项目，主要关注来自不同数据源和操作系统的安全事件日志的文档化和标准化。

安全事件以字典格式记录，可用作 ThreatHunter-Playbook 等项目的参考，同时将数据源映射到用于验证敌对技术检测的数据分析。

此外，该项目提供了一个公共信息模型(CIM ),数据工程师可以在数据标准化过程中使用该模型，以允许安全分析师跨不同数据源查询和分析数据。

最后，该项目还提供了关于特定数据源中确定的结构和关系的文档，以促进数据分析的发展。

**目标**

*   定义和共享通用信息模型，以提高安全事件日志的数据标准化和转换
*   定义和共享安全事件日志中确定的数据结构和关系
*   以字典格式向社区提供关于几个安全事件日志的详细信息
*   了解有关安全事件日志的更多信息(Windows、Linux 和 MacOS)
*   玩得开心点，当涉及到检测时，多想想 SIEM 中的数据结构！！

**项目结构**

有四个主要文件夹:

*   [**【通用信息模型】**](https://github.com/hunters-forge/OSSEM/blob/master/common_information_model)**:

    *   通过提供一种解析安全事件日志的标准方法，促进数据集的规范化
    *   它由与事件日志相关联的特定实体组织，并由[数据字典](https://github.com/hunters-forge/OSSEM/blob/master/data_dictionaries)更详细地定义
    *   每个实体的定义及其各自的字段名称大多是一般性的描述，可以帮助和加快事件日志解析过程。** 
*   **[**数据字典**](https://github.com/hunters-forge/OSSEM/blob/master/data_dictionaries) :

    *   包含按操作系统组织的几个安全事件日志及其各自数据集的特定信息
    *   每个字典描述一个事件日志及其相应的事件字段名
    *   [公共信息模型](https://github.com/hunters-forge/OSSEM/blob/master/common_information_model)文件夹和数据字典之间的区别在于，在 CIM 中，字段定义更加通用，而在数据字典中，每个字段名定义对于特定事件日志是唯一的。** 
*   **[**检测数据模型**](https://github.com/hunters-forge/OSSEM/blob/master/detection_data_model) :

    *   侧重于以数据对象的形式定义所需的数据以及数据对象之间的关系，以便于创建数据分析并验证对手技术的检测
    *   这是受到 MITRE 在他们的项目[汽车分析](https://car.mitre.org/wiki/Main_Page)中出色工作的启发
    *   每个数据对象所需的信息来自于[公共信息模型](https://github.com/hunters-forge/OSSEM/blob/master/common_information_model)中定义的实体** 
*   **[**攻击数据来源**](https://github.com/hunters-forge/OSSEM/blob/master/attack_data_sources) :

    *   侧重于建议的数据源或与[企业矩阵](https://attack.mitre.org/wiki/Technique_Matrix)中定义的技术相关的数据源的文档
    *   此外，在这里，数据源将与项目的[检测数据模型](https://github.com/hunters-forge/OSSEM/blob/master/detection_data_model)部分中定义的特定数据对象进行映射，主要目标是在技术、数据源和数据分析之间建立联系** 

 ****当前状态:Alpha**

该项目目前处于 alpha 阶段，这意味着内容仍在变化。我们欢迎任何改进项目的反馈和建议。

**使用 OSSEM 的项目**

*   [HELK](https://github.com/Cyb3rWard0g/HELK) 当前正在更新其管道配置

**鸣谢:** [@Cyb3rWard0g](https://twitter.com/Cyb3rWard0g)

[**Download**](https://github.com/hunters-forge/OSSEM)**