# SIPI–用于信誉数据分析的简单知识产权信息工具

> 原文：<https://kalilinuxtutorials.com/sipi-simple-ip-information-tools/>

SIPI 工具是针对事件响应团队和任何人谁想要知道的行为“可疑”的 IP 地址。这些工具从一组开放的威胁情报源中搜索信誉信息。关于此 IP 的信息，如恶意软件活动、恶意活动、黑名单、垃圾邮件和僵尸网络活动。

**也读[Idisagree——用 Discord Bot&Python 3](https://kalilinuxtutorials.com/idisagree-control-remote-computers/)控制远程电脑**

##### **依赖关系**:

*   请求
*   肖丹

##### **安装**:

```
pip install requests & easy_install shodan
git clone "repositori"
config API token into config.json
try: $> python sipi.py any_ip -A
```

## **SIPI 描述**

**简单的知识产权信息工具**

```
sIPi - is a free reconnaissance tool for obtain IP Address Information from**
 **many Open Sources: cymon.io | shoda.io | ipinfo.io
```

朱利安·冈萨雷斯·卡拉库埃尔

它是一个分析 IP 或 IP 列表的工具，可获得以下结果信息:

```
       **- reputación / actividad**
	**- nivel de exposición** 
	**- geolocalización
```

根据以下类别对黑名单中的 IP 进行信誉/检测:

```
 **Source: cymon.io - Cymon is the largest open tracker of malware, phishing, botnets, spam, and more**

          **['malware',
	   'botnet',
	   'spam',
	   'phishing',
	   'malicious activity',
	   'blacklist',
	   'dnsbl']** 
**Nivel de exposición:**

**Source: shodan.io - Shodan is the world's first search engine for Internet-connected devices.**

**Obtiene información toda la dirección IP que tiene SHODAN sobre la dirección IP, dependiendo del nivel** de acceso al motor SHODAN 
**se podra obtener información con mayor cantidad de datos (número de puertos, banner, geolocalización)**

**Geolocalización:**

**Source: ipinfo.io
Obtiene información simple de la dirección IP, geolocalización e información sobre el ASN, permite un ratio de 1000/day
```

## **安装要求**

```
cymon.io  - Necesita token de autenticación - usuario registrado ratio: 1000/days
shodan.io - Necesita token de autenticación - usuario registrado limite 100 resultados, puertos limitados
```

令牌的配置在 File: config.json 中输入，该文件必须位于执行 sipi.py 的目录中<< API token from all service is setting up into a “config.json” filename place in the root directory >

##### 从属关系

**请求**

```
pip install requests 
```

**庄丹**

```
easy_install shodan 
```

**[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/ST2Labs/SIPI)**