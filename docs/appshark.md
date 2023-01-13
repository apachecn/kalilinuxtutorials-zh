# Appshark:静态污点分析平台，用于扫描 Android 应用程序中的漏洞

> 原文：<https://kalilinuxtutorials.com/appshark/>

[![](img/0f4bc41e534bf8defb5c3d502971cb88.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgrCbVvedNvAwhuhODyKpF-o88mn_SHiD5IByvqzgMrSIxxxmOp2gJBut2DqNI4sD1dLYjYXdg-__Ka2OsjXIdIS1wOIMY9gTV0Pm4IiixbAYcdrB-TrKrk5l6yxqt8D9QaIALmLgZu4sNLoc5BWRFdb3mtLIfZ1sbKNdz85VKCL3l7w19rv8DvONuS/s728/Appshark.png)

Appshark 是一个静态污点分析平台，用于扫描 Android 应用程序中的漏洞。

## 先决条件

Appshark 需要 JDK 的特定版本— [JDK 11](https://www.oracle.com/java/technologies/javase/jdk11-archive-downloads.html) 。经过测试，由于依赖兼容性问题，它无法在其他 LTS 版本，JDK 8 和 JDK 16 上工作。

## 构建/编译 AppShark

我们假设您正在项目 repo 的根目录中工作。你可以用 [gradle](https://gradle.org/) 工具构建整个项目。

```
$ ./gradlew build  -x test 
```

执行上面的命令后，您会在目录`build/libs`中看到一个工件文件`AppShark-0.1.1-all.jar`。

## 运行 AppShark

像上一步一样，我们假设您仍然在项目的根文件夹中。您可以使用以下命令运行该工具

```
$ java -jar build/libs/AppShark-0.1.1-all.jar  config/config.json5
```

`config.json5`有以下配置内容。

```
{
  "apkPath": "/Users/apks/app1.apk",
  "out": "out",
  "rules": "unZipSlip.json",
  "maxPointerAnalyzeTime": 600
} 
```

下面解释了每个 JSON 字段。

*   apkPath:要分析的 apk 文件的路径
*   out:输出目录的路径
*   规则:规则文件的路径，可以是多个规则
*   maxPointerAnalyzeTime:为从入口点开始的分析设置的超时持续时间(秒)
*   debugRule:指定启用调试日志记录的规则名称

如果您提供一个配置 JSON 文件，它将输出路径设置为项目根目录中的`out`,那么您将在运行分析后找到结果文件`out/results.json`。

## 解读结果

下面是一个`results.json`的例子。

```
{
  "AppInfo": {
    "AppName": "test",
    "PackageName": "net.bytedance.security.app",
    "min_sdk": 17,
    "target_sdk": 28,
    "versionCode": 1000,
    "versionName": "1.0.0"
  },
  "SecurityInfo": {
    "FileRisk": {
      "unZipSlip": {
        "category": "FileRisk",
        "detail": "",
        "model": "2",
        "name": "unZipSlip",
        "possibility": "4",
        "vulners": [
          {
            "details": {
              "position": "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolderFix1(java.lang.String,java.lang.String)>",
              "Sink": "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolderFix1(java.lang.String,java.lang.String)>->$r31",
              "entryMethod": "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void f()>",
              "Source": "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolderFix1(java.lang.String,java.lang.String)>->$r3",
              "url": "/Volumes/dev/zijie/appshark-opensource/out/vuln/1-unZipSlip.html",
              "target": [
                "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolderFix1(java.lang.String,java.lang.String)>->$r3",
                "pf{obj{<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolderFix1(java.lang.String,java.lang.String)>:35=>java.lang.StringBuilder}(unknown)->@data}",
                "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolderFix1(java.lang.String,java.lang.String)>->$r11",
                "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolderFix1(java.lang.String,java.lang.String)>->$r31"
              ]
            },
            "hash": "ec57a2a3190677ffe78a0c8aaf58ba5aee4d2247",
            "possibility": "4"
          },
          {
            "details": {
              "position": "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolder(java.lang.String,java.lang.String)>",
              "Sink": "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolder(java.lang.String,java.lang.String)>->$r34",
              "entryMethod": "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void f()>",
              "Source": "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolder(java.lang.String,java.lang.String)>->$r3",
              "url": "/Volumes/dev/zijie/appshark-opensource/out/vuln/2-unZipSlip.html",
              "target": [
                "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolder(java.lang.String,java.lang.String)>->$r3",
                "pf{obj{<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolder(java.lang.String,java.lang.String)>:33=>java.lang.StringBuilder}(unknown)->@data}",
                "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolder(java.lang.String,java.lang.String)>->$r14",
                "<net.bytedance.security.app.pathfinder.testdata.ZipSlip: void UnZipFolder(java.lang.String,java.lang.String)>->$r34"
              ]
            },
            "hash": "26c6d6ee704c59949cfef78350a1d9aef04c29ad",
            "possibility": "4"
          }
        ],
        "wiki": "",
        "deobfApk": "/Volumes/dev/zijie/appshark-opensource/app.apk"
      }
    }
  },
  "DeepLinkInfo": {
  },
  "HTTP_API": [
  ],
  "JsBridgeInfo": [
  ],
  "BasicInfo": {
    "ComponentsInfo": {
    },
    "JSNativeInterface": [
    ]
  },
  "UsePermissions": [
  ],
  "DefinePermissions": {
  },
  "Profile": "/Volumes/dev/zijie/appshark-opensource/out/vuln/3-profiler.json"
}

```

[Click Here To Download](https://github.com/bytedance/appshark)