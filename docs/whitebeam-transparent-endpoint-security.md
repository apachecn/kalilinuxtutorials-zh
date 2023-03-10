# 白色光束:透明终端安全

> 原文：<https://kalilinuxtutorials.com/whitebeam-transparent-endpoint-security/>

[![](img/42021f6549662c6393d5cb233a3c613f.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh1YWXhRryFIHw_bVSEbOAwkNl4dq-1EMMXQETTdChI4ONDqKvRfQFxiDxTHqZjDHFUAxFR9G4MTP5mIGMhISyBeZhJirOQfDgD60BvozkFTe_ylGtr9fq5YXHFcADCytfr-9Bx3mK9el7QWpAtrNjxNkB8v8lU92hKgj84kXE5rwXV0nqV5yjMWj39/s728/WhiteBeamShield-svg.png)

**WhiteBeam** 是一个透明的安全端点

## 特征

*   阻止和检测高级攻击
*   现代审计密码学:用于哈希和加密的 RustCrypto
*   高度兼容:开发集中于所有平台(包括遗留系统)和架构
*   可用来源:欢迎审计
*   由拥有 100 多年经验的安全研究人员审查

## 装置

由于 0.3 的向后不兼容的安全增强，WhiteBeam 目前不可安装。请稍后再来查看！

### 从软件包(Linux)

针对 WhiteBeam 的特定于发行版的包尚未发布，请尽快再次查看！

### 来自版本(Linux)

1.  下载最新版本
2.  确保发布文件哈希与官方哈希匹配(操作方法)
3.  安装:
    *   `**./whitebeam-installer install**`

### 来源(Linux)

1.  运行测试(*可选*):
    *   `**cargo run test**`
2.  编译:
    *   `**cargo run build**`
3.  安装白色光束:
    *   `**cargo run install**`

## 快速启动

1.  成为根( **`sudo su` / `su root`** )
2.  设置恢复密码:`**whitebeam --setting RecoverySecret mask**`。设置恢复密码后，您可以运行`**whitebeam --auth**`对系统进行更改。

### 如何检测白光束攻击

根据您的喜好提供多种指南。请联系我们，以便我们可以帮助您将 WhiteBeam 与您的环境相集成。

1.  无服务器指南，用于被动审查
2.  osquery 车队设置指南，用于被动审查
3.  主动响应的 WhiteBeam 服务器设置指南

### 如何防范白光束攻击

ℹ️白束是实验软件。联系我们以获得安全实施的帮助。

1.  成为根( **`sudo su` / `su root`** )
2.  安装 WhiteBeam 至少 24 小时后，检查基线:
    *   `**whitebeam --baseline**`
3.  按照白名单指南将可信行为添加到白名单中
4.  启用白光束预防:
    *   `**whitebeam --setting Prevention true**`

[**Download**](https://github.com/WhiteBeamSec/WhiteBeam)