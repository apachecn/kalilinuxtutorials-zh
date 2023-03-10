# LambdaGuard : AWS 无服务器安全

> 原文：<https://kalilinuxtutorials.com/lambdaguard/>

[![](img/0972a1bcfcb95466ea10daf2bd899176.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhs6B88McU0LkcyVCdLLAOgqKogoLYOqnGq3Z5l7k82Awsd0M3m-K5wvG2ej4m8hSecirdaPOPiH9ehBWWyqU-d-JspauWVGPY0UdpRaccxAUxiVauN0oV62nPxqkhErXq7Lr_Xg-CZ-SFdV_EfDuQ9ss-XDuK5onL6Q-BPZrLKrOc6hC_IP2T_J1hi/s380/download%20(3)%20(1).png)

**LambdaGuard** 是由亚马逊网络服务提供的事件驱动的无服务器计算平台。它是一种计算服务，运行代码以响应事件，并自动管理该代码所需的计算资源。

LambdaGuard 是一个 AWS Lambda 审计工具，旨在创建资产可见性并提供可操作的结果。它从安全角度提供了关于统计分析、AWS 服务依赖性和配置检查的有意义的概述。

## 要求

*   Python 3.6 以上版本
*   Java 11(对于 SonarQube 是可选的)

## 安装

### 来自 PyPI

**pip3 安装 lambdaguard**

**来自 Github**

**git 克隆 https://github.com/Skyscanner/lambdaguard
CD lambda guard
sudo make install**

### AWS 访问

运行 LambdaGuard 需要一组 AWS 访问密钥和权限。

**制作 aws**

## 奔跑

*   `**lambdaguard --help**`
*   **T2`lambdaguard --function arn:aws:lambda:function`**
*   **T2`lambdaguard --input function-arns.txt`**
*   **T2`lambdaguard --output /tmp/lambdaguard`**
*   **T2`lambdaguard --profile LambdaGuardProfile`**
*   **T2`lambdaguard --keys ACCESS_KEY_ID SECRET_ACCESS_KEY`**
*   **T2`lambdaguard --region eu-west-1`**
*   **T2`lambdaguard --verbose`**

## SonarQube:静态代码分析

### 下载声纳扫描仪命令行界面

*   https://github.com/SonarSource/sonar-scanner-cli

### 建造 SonarQube

*   `**make sonarqube**`

### 使用 SonarQube 立方体

*   `**lambdaguard --sonarqube config.json**`

Config 应该具有以下格式:

{ **“命令”:“声纳-扫描仪-X”，
“URL”:“http://localhost:9000”，
“登录”:“admin”，
“密码”:“admin”
}**

## 发展

使-B 干净
使开发
。开发/bin/激活
制作安装-开发
制作测试

[**Download**](https://github.com/Skyscanner/LambdaGuard)