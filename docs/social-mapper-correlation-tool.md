# 社交地图——一个社交媒体列举和关联工具

> 原文：<https://kalilinuxtutorials.com/social-mapper-correlation-tool/>

社交地图(Social Mapper)是一款社交媒体地图工具，由 Jacob Wilkin(Greenwolf)通过面部识别将个人资料关联起来。

Social Mapper 是一款开源智能工具，它使用面部识别来大规模关联不同网站的社交媒体档案。

它采用自动化方法在流行的社交媒体网站上搜索目标名称和图片，以准确检测和分组一个人的存在，并将结果输出到一份报告中，人工操作员可以快速查看。

Social Mapper 在安全行业有多种用途，例如，自动收集大量社交媒体资料，用于有针对性的网络钓鱼活动。

面部识别通过消除搜索结果中的假阳性来帮助这一过程，以便人类操作员更快地查看这些数据。

社交地图支持以下社交媒体平台:

*   [LinkedIn](https://www.linkedin.com/)
*   [脸书](https://www.facebook.com/)
*   [推特](https://twitter.com/)
*   [GooglePlus](https://plus.google.com/)
*   [Instagram](https://www.instagram.com/)
*   [VKontakte](https://vk.com/)
*   [微博](https://www.weibo.com/login.php)
*   [洗澡](https://www.douban.com/)

社交地图采用多种输入类型，例如:

*   组织名称，通过 LinkedIn 搜索
*   一个装满命名图像的文件夹
*   一个 CSV 文件，包含在线图像的名称和 URL。

**也读作[SIP:基于 SIP 的审计和攻击工具](https://kalilinuxtutorials.com/mr-sip-based-audit-attack-tool/)**

## **为什么要运行社交映射器？**

Social Mapper 主要针对渗透测试人员和 Red Teamers，他们将使用它来扩展他们的目标列表并找到他们的社交媒体资料。从这里开始，你所做的仅仅受到你的想象力的限制，但是这里有一些开始的想法:

(注意:Social Mapper 不会执行这些攻击，它会收集您大规模执行这些攻击所需的数据。)

*   创建虚假的社交媒体资料，将目标“加为好友”，并向他们发送链接或恶意软件。最近的统计数据显示，社交媒体用户点击链接和打开文档的可能性是通过电子邮件发送的两倍多。
*   用优惠券和优惠诱使用户透露他们的电子邮件和电话号码，从而转向网络钓鱼、访问或微笑。
*   在知道目标有账户的情况下，为每个社交媒体网站创建定制的网络钓鱼活动。在电子邮件中附上他们的个人资料照片，让这些照片更加真实。捕获密码以供重复使用。
*   查看目标照片，寻找员工出入卡徽章，并熟悉建筑内部。

## **入门**

这些说明将向您展示社交地图的要求以及如何使用社交地图。

### **先决条件**

由于这是一个基于 python 的工具，理论上它应该可以在 Linux、ChromeOS ( [开发者模式](https://www.chromium.org/chromium-os/developer-information-for-chrome-os-devices/generic))、Mac 和 Windows 上运行。主要需求是 Firefox，Selenium，和 Geckodriver。要安装该工具，请按照以下 4 个步骤进行设置:

在此安装最新版本的 Mozilla Firefox:

```
https://www.mozilla.org/en-GB/firefox/new/
```

为你的操作系统安装 Geckodriver，确保它在你的路径下，在 Mac 上你可以把它放在， **`/usr/local/bin`** 在 ChromeOS 上你可以把它放在，`**/usr/local/bin**`在 Linux 上你可以把它放在`**/usr/bin**`。

在这里下载 **Geckodriver** 的最新版本:

```
https://github.com/mozilla/geckodriver/releases
```

安装所需的 python 2.7 库:

```
git clone https://github.com/SpiderLabs/social_mapper
cd social_mapper/setup
python -m pip install --no-cache-dir -r requirements.txt
```

为社交映射器提供登录社交媒体服务的凭据:

```
Open social_mapper.py and enter social media credentials into global variables at the top of the file
```

## **使用社交地图**

社交映射器通过混合使用必需和可选参数从命令行运行。您可以指定选项，如输入类型和要检查的站点，以及许多影响速度和准确性的其他参数。

### **必需参数**

要启动工具，必须提供 4 个参数，即输入格式、输入文件或文件夹以及基本运行模式:

```
-f, --format	: Specify if the -i, --input is a 'name', 'csv', 'imagefolder' or 'socialmapper' resume file
-i, --input 	: The company name, a csv file, imagefolder or social mapper html file to feed into social mapper
-m, --mode		: Fast or Accurate allows you to choose to skip potential targets after a first likely match is found, in some cases potentially speeding up the program x20
```

此外，必须选择至少一个要检查的社交媒体网站，包括以下一项或多项:

```
**-a, --all 		: Selects all of the options below and checks every site that social mapper has credentials for
-fb, --facebook 	: Check Facebook
-tw, --twitter 		: Check Twitter
-ig, --instagram 	: Check Instagram
-li, --linkedin 	: Check LinkedIn
-gp, --googleplus 	: Check GooglePlus
-vk, --vkontakte 	: Check VKontakte
-wb, --weibo 		: Check Weibo
-db, --douban 		: Check Douban**
```

### **可选参数**

还可以设置额外的可选参数，以向社交映射程序的运行方式添加额外的自定义:

```
-t, --threshold 	: Customises the faceial recognition threshold for matches, this can be seen as the match accuracy. Default is 'standard', but can be set to loose, standard, strict or superstrict. For example loose will find more matches, but some may be incorrect. While strict may find less matches but also contain less false positives in the final report. 
-cid, --companyid 	: Additional parameter to add in a LinkedIn Company ID for if name searches are not picking the correct company.
-s, --showbrowser	: Makes the Firefox browser visable so you can see the searches performed. Useful for debugging. 
-v, --version		: Display current version
```

### **例文**

下面是几个针对不同用例的运行示例:

```
A quick run for facebook and twitter on some targets you have in an imagefolder, that you plan to manually review and don't mind some false positives:
python social_mapper.py -f imagefolder -i ./mytargets -m fast -fb -tw**

**A exhaustive run on a large company where false positives must be kept to a minimum:
python social_mapper.py -f company -i "SpiderLabs" -m accurate -a -t strict**

**A large run that needs to be split over multiple sessions due to time, the first run doing LinkedIn and Facebook, with the second resuming and filling in Twitter, Google Plus and Instagram:
python social_mapper.py -f company -i "SpiderLabs" -m accurate -li -fb
python social_mapper.py -f socialmapper -i ./SpiderLabs-social-mapper-linkedin-facebook.html -m accurate -tw -gp -ig
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/SpiderLabs/social_mapper)

**作者鸣谢:蜘蛛实验室**