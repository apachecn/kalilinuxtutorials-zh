# Lunar:一个轻量级原生 DLL 映射库

> 原文：<https://kalilinuxtutorials.com/lunar/>

[![Lunar : A Lightweight Native DLL Mapping Library](img/c7daf6392eb4e3f1166c37e2d71fbd31.png "Lunar : A Lightweight Native DLL Mapping Library")](https://1.bp.blogspot.com/-wmeCCj7YGXc/XpNTvOZ9evI/AAAAAAAAF5Y/BlADF3tI_SoG0QgirMShum4zoap56XZ4wCLcBGAsYHQ/s1600/DLL%25281%2529.png)

**Lunar** 是一个轻量级原生 DLL 映射库，支持直接从内存映射。

**特性**

*   导入和延迟导入问题得到解决
*   执行重新定位
*   图像部分使用正确的页面保护进行映射
*   初始化异常处理程序
*   生成并初始化安全 cookie
*   调用 DLL 入口点和 TLS 回调

**入门**

下面的例子演示了该库的一个简单实现

var library mapper = new library mapper(进程，dll bytes)；
**//将 DLL 映射到进程**
libraryMapper 中。map library()；
**//从进程**
libraryMapper 中取消 DLL 映射。unamplibrary()；

**也可阅读-[sand castle:AWS S3 桶枚举的 Python 脚本](https://kalilinuxtutorials.com/sandcastle/)**

**构造函数**

**LibraryMapper(进程，内存<字节> )**

*   提供将 DLL 从内存映射到远程进程的功能

**LibraryMapper(进程，字符串)**

*   提供将 DLL 从磁盘映射到远程进程的功能。

**属性**

dllbaseaddress

远程进程中 DLL 映射后的基址。

**方法**

**地图库()**

*   将 DLL 映射到远程进程

**取消磁带库()**

*   从远程进程取消 DLL 映射

**注意事项**

*   制图需要存在 ntdll.dll 的 PDB，因此，该库将自动从微软符号服务器下载该 PDB 的最新版本，并将其缓存在**% appdata %/Lunar/Dependencies**中

[**Download**](https://github.com/Dewera/Lunar)