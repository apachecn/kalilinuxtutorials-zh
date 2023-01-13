# SWF Finder:SWF 潜在参数查找器

> 原文：<https://kalilinuxtutorials.com/swfpfinder-swf-potential-parameters-finder/>

[![SWFPFinder : SWF Potential Parameters Finder](img/d6928e5e3cc84c416ac08a7d550603cc.png "SWFPFinder : SWF Potential Parameters Finder")](https://1.bp.blogspot.com/-f46oyYRuAVI/Xh4qpPIt6kI/AAAAAAAAEcc/4jZvmhHY2NYUntrTvlS5N8Pau9Ru9vcVQCLcBGAsYHQ/s1600/SWF_Icon.png)

SWFPFinder 是一个简单的开源 bash 脚本，旨在通过分析 swf 文件来发现 webapp 上潜在的 swf(文件)参数。

它使用 **`swfmill`** 工具， [swfmill](https://github.com/djcsdy/swfmill) 是一个处理 Adobe Flash (SWF)文件的工具。它可以将 SWF 与一种称为“swfml”的 XML 方言相互转换，这种方言与 SWF 文件格式非常相似。

**也读作-[熔岩:大规模自动化漏洞添加](https://kalilinuxtutorials.com/lava-large-scale-automated-vulnerability-addition/)**

**安装**

**$ wget https://raw . githubusercontent . com/M4 ll0k/swfp finder/master/swfp finder . sh

或

$ git 克隆 https://github.com/m4ll0k/SWFPFinder.git swfp finder
$ CD swfp finder**

**支撑平台**

*   MacOSx
*   Linux 操作系统
*   窗口(Cygwin)

**要求**

*   [swfmill](https://github.com/djcsdy/swfmill)
    *   对于 linux `**apt-get install swfmill**`
    *   对于 macosx **`brew install swfmill`**

**用途**

$ bash swfpfinder . sh https://raw . githubusercontent . com/EVI lcos/XSS . swf/master/XSS . swf
事件
安全错误事件
xss_fla
主时间轴
MovieClip
param
对象
动作
字符串
cmd
攻击
get _ COMPLETE
get _ sec _ ERROR
frame 1
URL loader

[**Download**](https://www.kitploit.com/2020/01/swfpfinder-swf-potential-parameters.html)