# LocCheck:简化 IOC 研究过程的工具

> 原文：<https://kalilinuxtutorials.com/ioccheck/>

[![LocCheck : A Tool For Simplifying The Process Of Researching IOCs](img/19039d64e14585ff2372b69f959dacfe.png "LocCheck : A Tool For Simplifying The Process Of Researching IOCs")](https://1.bp.blogspot.com/-1W58FcPmuAg/YNrvjRD_p8I/AAAAAAAAJtw/mbtvn19ZCQAjM2Ys5bhAQMsnNwiGMO3SgCLcBGAsYHQ/s728/LocCheck%25281%2529.png)

**LocCheck** 是一个工具，用于简化研究文件哈希、IP 地址和其他危害指示器(IOCs)的过程。

**特性**

*   从一个命令或几行 Python 代码中跨多个威胁情报服务查找散列。
*   Currenty 支持以下服务:
    *   [VirusTotal](https://virustotal.com/)
    *   [MalwareBazaar](https://bazaar.abuse.ch/)
    *   [Shodan.io](https://shodan.io/)
*   计划支持:
    *   [尖叫屋](https://urlhaus.abuse.ch/)
    *   [OTX](https://otx.alienvault.com/)
    *   [勘验实验室](https://labs.inquest.net/)
    *   [不做](https://www.malshare.com/)
    *   [马尔佩迪亚](https://malpedia.caad.fkie.fraunhofer.de/)
    *   虐待

**快速入门**

**pip 安装 io check**

您也可以直接运行代码

**git 克隆 https://github.com/ranguli/ioccheck&&CD io check
诗歌安装**

**用途**

**ioccheck 27a 021 bbfb 644 d479 d477 d169 d169 d635 ecfe2a38aabf 651 fdf
检核 hash 275 a021 bbfb 649 d47519 d477 d639 d636 f2f 2 a38aabf 651 fdf。
*哈希算法:sha256[*病毒标题 URL:
https://病毒标题. com/GUI/file/275 AABB bb 2009 d4d4d479d7d 169 d63f2f 2 fea4538aabf/
我是一个很好的人，我是一个很好的人，我是一个很好的人，我是一个很好的人，我是一个很好的人，我是一个很好的人，我是一个很好的人，我是一个很好的人，我是一个很好的人，我是一个很好的人，我是一个很好的人我的天啊！我的天啊！──可以───可以─可以─可以─可以我的天啊！我的天啊！我是一个很好的人，我是一个很好的人，我是一个很好的人，我是一个很好的人，我是一个很好的人，我是一个很好的人，我是一个很好的人，我是一个很好的人，我是一个很好的人，我是一个很好的人，我是一个很好的人**

**使用 API**

创建散列

**> > > from ioccheck 导入 Hash
>>>from IOC check . services 导入 virus total
>>>eicar = Hash(" 275 a 021 bbfb 6489 e 54d 471899 F7 db 9d 1663 fc 695 EC 2 Fe 2 a2 2c 4538 aabf 651 FD 0f ")
>>>#这是什么散列？
> > >打印(eicar.hash_type)
SHA256**

查找哈希

**> > > #不带参数，check()尝试所有支持的服务。从~/中抓取 API 密钥。默认情况下是 ioccheck。
>>>eicar . check()
>>>#或者:
>>>eicar . check(services = virus total，config_path=/foo/bar/。ioccheck)**

研究杂凑

> > >**检查 VirusTotal 报告，查看 Sophos 是否检测到我们的哈希
>>>eicar . reports . virus total . get _ detections(engines =[" Sophos "])
{ ' Sophos ':{ ' category ':'恶意'，' engine_name': 'Sophos '，' engine_version': '1.0.2.0 '，' result': 'EICAR-AV-Test '，' method ':'黑名单'，' engine _ update ':' 2021 0314 ' } }
>
>>>print(eicar . reports . virus total . name)
' eicar . com-2224 '
>>>#有多少反病毒引擎在检测这个 hash？
>>>eicar . reports . virus total . detection _ count
60**

**> > > #只显示 VirusTotal API 响应！
>>>eicar . reports . virus total . API _ response
<vt . object . object file 275 a 021 bbfb 6489 e 54d 471899 F7 db 9d 1663 fc 695 EC 2 Fe 2 a2 c 4538 aabf 651 FD 0f>**

[**Download**](https://github.com/ranguli/ioccheck)