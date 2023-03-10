# 私有集成员(PSM):允许客户端进行私有查询的加密协议

> 原文：<https://kalilinuxtutorials.com/private-set-membership-psm/>

[![](img/9555623710a385783763e0d85c06e110.png)](https://blogger.googleusercontent.com/img/a/AVvXsEhXjJD4ks_DLzCWVZQSDtxX-ROj_M8gy8WLb7fi9QNwXrZ6HjbxOLhbJVfyzPrZ2UmGVTIbtxqJ_sT2Lfsi3x--ely1gd0gt5z9zWAIKcFB0j3P6NWEucPtI9gc_NJAS3ko_ARDcIjtfWmL3DK3z55xwlseGO25DRWUYR0JYpJPbfJiwtyTwtae5t7w=s728)

**私有集合成员关系** (PSM)是一种加密协议，允许客户端以隐私保护的方式秘密查询客户端的标识符是否是服务器保存的标识符集合的成员。

从高层次来看，PSM 提供了以下隐私保证:

*   服务器不会以明文的形式获知客户端查询的标识符。
*   服务器不知道客户机的查询结果是成员资格还是非成员资格的确定。
*   除了查询客户端的标识符是否是服务器持有的标识符集合的成员之外，查询客户端不了解关于服务器存储的标识符集合的任何信息。换句话说，进行查询的客户端了解到最少的信息量，这仅仅是成员资格查询的答案。

**依赖关系**

专用集成员库需要下列依赖关系:

*   C++公共库。
*   巴泽尔建造了图书馆。
*   底层加密操作的 BoringSSL。
*   标志的 GFlag。需要使用 glog。
*   用于记录的 GLog。
*   单元测试库的谷歌测试。
*   用于数据序列化的协议缓冲区。
*   全同态加密的外壳。
*   用于加密程序的 Tink。

**如何建造**

为了运行这个库，你需要安装 Bazel，如果你还没有的话。[遵循 Bazel 网站上针对您的平台的说明。确保您安装的是版本 4.2.1 或更高版本。](https://docs.bazel.build/versions/master/install.htm[l](https://docs.bazel.build/versions/master/install.html)

如果您还没有 Git，您还需要安装它。遵循 Git 网站上针对您的平台的说明。

安装 Bazel 和 Git 后，打开终端，将存储库克隆到本地文件夹中。

导航到刚刚创建的`**private-membership**`文件夹，使用 Bazel 构建库和依赖项。注意，库必须使用 C++17 构建。

**CD private-membership
bazel build…–cxxopt = '-STD = c++ 17 '**

您也可以使用以下命令运行所有测试(递归地):

**基准测试…—cxopt =-STD = c++ 17‘**

[**Download**](https://github.com/google/private-membership)