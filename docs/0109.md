# CGPwn–Ubuntu 虚拟机，用于硬件黑客、re 和战争游戏

> 原文：<https://kalilinuxtutorials.com/cgpwn-hardware-hacking-re-wargaming/>

CGPwn 是一个轻量级的虚拟机，用于硬件入侵、RE (fuzzing、symEx、exploiting 等)和战争游戏任务。包含在 CGPwn 中的工具；

## **启动虚拟机**

```
git clone https://github.com/0xM3R/cgPwn
cd cgPwn
vagrant up
... Grab a beer and relax until everything is getting setup for you ;)
vagrant ssh
```

## **CGPwn 默认设置**

默认情况下，个人点文件安装在虚拟机上。如果不想要我的设置，只需在 cgPwn.sh 中注释掉下面几行。

**又读[Ua-tester——用户代理 WAF、IDS/IPS、重定向测试的工具](https://kalilinuxtutorials.com/ua-tester/)**

```
# Personal config
sudo apt-get -y install stow
cd ~
rm .bashrc
git clone https://github.com/0xM3R/dotfiles
cd dotfiles
chmod a+x ./install.sh
./install.sh
```

### **共享文件夹**

将文件放到主机上的`**sharedFolder**`文件夹中，以便在`**/home/vagrant/sharedFolder**`时在虚拟机上找到它们

[![](img/d861a9096555aeb1980fc054015933d7.png)](https://github.com/0xM3R/cgPwn/)