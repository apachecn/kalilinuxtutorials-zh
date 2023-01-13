# dv HMA–该死的易受攻击的混合移动应用程序

> 原文：<https://kalilinuxtutorials.com/dvhma/>

该死的易受攻击混合移动应用程序或 DVHMA 是一种针对 Android 的混合移动应用程序，它故意包含漏洞。它的动机是让安全专家能够合法地测试他们的工具和技术，让开发人员更好地理解安全开发混合移动应用程序中的常见陷阱。

创建此应用程序是为了检查开发混合应用程序的缺陷，例如，安全地使用 Apache Cordova 或 SAP Kapsel。现在，基本的关注点是深入理解利用 JavaScript 到 Java 桥的注入漏洞。

智能设备:在 4Prototypes.com 轻松找到所需的高科技产品。

## **DVHMA 安装**

### **先决条件**

我们假设

*   Android SDK([https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html))和
*   阿帕奇·科尔多瓦([https://cordova.apache.org/](https://cordova.apache.org/))，版本 8.0.0(以后的版本可能会起作用)

此外，我们假设对 Apache Cordova 的构建系统有一个基本的了解。

#### **又读[lib 钠——好用的软件库](http://kalilinuxtutorials.com/libsodium/)**

### **建筑 dv HMA**

#### **设置环境变量**

```
export ANDROID_HOME=<Android SDK Installation Directory>
export PATH=$ANDROID_HOME/tools:$PATH
export PATH=$ANDROID_HOME/platform-tools:$PATH 
```

#### 编译 DVHMA

```
cd DVHMA-Featherweight
cordova plugin add ../plugins/DVHMA-Storage
cordova plugin add ../plugins/DVHMA-WebIntent 
cordova platform add android
cordova compile android 
```

#### **在仿真器中运行 dv HMA**

```
cordova run android 
```

## **团队成员**

该应用程序的开发始于 ZertApps 项目的一部分。ZertApps 是一个由德国研究与教育部资助的合作研究项目。它现在由英国谢菲尔德大学的软件保证和安全研究小组开发和维护。

DVHMA 的核心开发人员是:

*   阿奇姆·d·布鲁克
*   迈克尔赫尔茨贝格

## **出版物**

*   阿奇姆·d·布鲁克和迈克尔·赫尔茨贝格。关于混合移动应用的静态分析:Apache Cordova Nation 的状态报告。工程安全软件和系统国际研讨会。计算机科学讲义(9639)，72-88 页，斯普林格出版社，2016 年。[https://www . br ucker . ch/书目/摘要/br ucker . ea-Cordova-security-2016](https://www.brucker.ch/bibliography/abstract/brucker.ea-cordova-security-2016)doi:[10.1007/978-3-319-30806-7 _ 5](http://dx.doi.org/10.1007/978-3-319-30806-7_5)

[![](img/a51de913dc60eee505c4a68651ee8e4d.png)](https://github.com/logicalhacking/DVHMA)