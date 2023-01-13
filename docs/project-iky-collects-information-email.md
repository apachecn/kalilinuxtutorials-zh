# iKy 项目-从电子邮件中收集信息的工具

> 原文：<https://kalilinuxtutorials.com/project-iky-collects-information-email/>

[![Project iKy – Tool To Collects Information From An Email](img/f93bff6cc78b49542b5622e61eced750.png "Project iKy – Tool To Collects Information From An Email")](https://1.bp.blogspot.com/-_AFYMhdglm8/XRT0b54d0MI/AAAAAAAABD8/WM3kEyxpdeoBjUw5KVzd9wY02LiPJAIPQCLcBGAs/s1600/Project%2BiKy%25281%2529.png)

项目 iKy 是一个从电子邮件中收集信息并在一个漂亮的可视化界面中显示结果的工具。

![](img/cce14ca32e84436ce7a55ece6d42d9c8.png)

**注意:**我们要警告你，我们已经把前端从 AngularJS 改为 Angular 7。为此，我们将 AngularJS 作为 iKy-v1 分支的前端。

改变前端的原因是为了更新技术和获得更容易的安装方式。

**也可阅读-[LiveHiddenCamera:从 Android 设备录制实时视频&音频而不显示预览](https://kalilinuxtutorials.com/livehiddencamera/)的库**

**安装**

**克隆存储库**

**git 克隆 https://gitlab.com/kennbroorg/iKy.git**

**安装后端**

**再说一遍**

您必须安装 Redis

**wget http://download . redis . io/redis-stability . tar . gz
tar xvzf redis-stability . tar . gz
CD redis-stability
make
sudo make install**

并在终端中打开服务器

重定向服务器

**蟒蛇的东西&芹菜**

您必须在 requirements.txt 中安装这些库

**pip install-r requirements . txt**

并在另一个终端打开目录**后端**中的芹菜

**。/celery.sh**

最后，再次，在另一个终端从目录**后端**打开后端应用

**python app.py**

**安装前端**

**节点**

首先安装 [nodejs](https://nodejs.org/en/) 。

从属关系

在目录**中前端**安装依赖项

**npm 安装**

**打开前端服务器**

最后，要运行前端服务器，请执行:

**npm 开始**

**浏览器**

在这个 [url](http://127.0.0.1:4200) 中打开浏览器

**配置 API 键**

一旦应用程序加载到浏览器中，您应该转到 Api Keys 选项并加载所需的 Api 值。

*   Fullcontact:从这里的[生成 APIs】](https://support.fullcontact.com/hc/en-us/articles/115003415888-Getting-Started-FullContact-v2-APIs)
*   Twitter:从这里的[生成 APIs】](https://developer.twitter.com/en/docs/basics/authentication/guides/access-tokens.html)
*   Linkedin:只有你的账户的用户名和密码必须被加载

[**Download**](https://gitlab.com/kennbroorg/iKy)