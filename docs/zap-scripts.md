# Zap-Scripts : Zed 攻击代理脚本，用于查找 CVE 和秘密

> 原文：<https://kalilinuxtutorials.com/zap-scripts/>

[![](img/a09afe448518cb0aff47e0837e7b9e34.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgXBrlth-S3xLgd7d6m6D7P2bdbb5rlgoC5QpsI5i-qysXztfbTP7wltfj-Kei01ON9X4fZvXmb9hpHPWzPGy0D9S-vL9i_gTN99GhNzxmVfwftuNAuIXtvmWKbLv_JP4TBpOEgPjSOhwrBmaPOKSr4Wjnsm78Rj_Ya1NeP1Vpo8-NHDCAGDKZR2_Ah/s728/Zed%20Attack%20(1).png)

Zap-Scripts 是一个 Zed 攻击代理脚本，用于查找 CVE 和秘密。

## 建筑

这个项目使用 Gradle 来构建 ZAP 插件，只需运行:

。 **/gradlew 构建**

在项目的主目录中，附加组件将被放置在目录`**build/zapAddOn/bin/**`中。

## 用法

在 ZAP 中使用这个 repo 最简单的方法是将目录添加到 ZAP 中的 scripts 目录中(在 Options -> Scripts 下)。

然而，你也可以构建插件并安装它(在文件->加载插件文件下…)。

[**Download**](https://github.com/sepehrdaddev/zap-scripts)