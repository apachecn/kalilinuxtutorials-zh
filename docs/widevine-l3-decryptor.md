# Widevine L3 解密器:一个演示绕过 Widevine L3 DRM 的 Chrome 扩展

> 原文：<https://kalilinuxtutorials.com/widevine-l3-decryptor/>

[![Widevine L3 Decryptor : A Chrome Extension That Demonstrates Bypassing Widevine L3 DRM](img/198b64811675a313b81a0f74d438f771.png "Widevine L3 Decryptor : A Chrome Extension That Demonstrates Bypassing Widevine L3 DRM")](https://1.bp.blogspot.com/-AqaV94EDOOY/X6Cb4g5Hs-I/AAAAAAAAH6w/TWJGRePsXR4WJb-yI3GXtRHIsl7CD7BvgCLcBGAsYHQ/s728/Widevine.png)

Widevine 是谷歌拥有的 DRM 系统，被许多流行的流媒体服务(网飞、Spotify 等)使用。)来防止媒体内容被下载。

但是 Widevine 最不安全的安全级别 L3，正如在大多数浏览器和个人电脑中使用的，是 100%在软件中实现的(即没有硬件 TEEs)，从而使它可逆和可绕过。

这个 Chrome 扩展演示了如何通过劫持对浏览器的加密媒体扩展(EME)的调用并解密所有传输的 Widevine 内容密钥来绕过 Widevine DRM，从而有效地将其转变为 clearkey DRM。

**用途**

要看到这个概念的实际应用，只需在开发者模式下加载扩展，浏览任何播放 Widevine 保护内容的网站，比如 https://bitmovin.com/demos/drm[更新:链接断了？].

密钥将以明文形式记录到 javascript 控制台。

*   **例子**

**widevinedecrypter:找到密钥:100 B6 c 20940 f 779 a 4589152 b 57d 2 dacb(KID = EB 676 abbb CB 345 e 96 bbcf 616630 f1 a3 da)**

解密媒体本身只需要使用一个可以解密 MPEG-CENC 流的工具，比如 ffmpeg。

*   **例子**

**ffmpeg-decryption _ key 100 B6 c 20940 f 779 a 4589152 b 57 D2 dacb-I encrypted _ media . MP4-codec copy decrypted _ media . MP4**

**注意:**该扩展目前仅支持 Windows 平台。

**如何？**

在浏览器的环境中，媒体的实际解密通常是在专有二进制文件(widevinecdm.dll，称为内容解密模块或 cdm)中完成的，只有在从许可证服务器接收到带有加密密钥的许可证之后。

这种二进制文件通常被严重混淆，并利用声称提供软件“保护”的第三方解决方案，如 Arxan 或 Whitecryption。

然后，可以对二进制文件进行一些反向操作，从许可证响应中提取密钥并模仿密钥解密算法。

**为什么**

这个概念验证是为了进一步表明代码混淆、反调试技巧、白盒加密算法和其他通过模糊实现安全性的方法最终都会被击败，并且在某种程度上是毫无意义的。

**法律免责声明**

这只是出于教育目的。从流媒体服务下载受版权保护的材料可能违反其服务条款。使用风险自担。

[**Download**](https://github.com/tomer8007/widevine-l3-decryptor)