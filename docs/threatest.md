# Threatest : Threatest 是一个端到端测试威胁检测规则的 Go 框架

> 原文：<https://kalilinuxtutorials.com/threatest/>

[![](img/ff670f9208a35eda778d7d1d10ce5f05.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjW9tWFWC41GIZ5kt7Qc2R4o9s7NHLIevuf2mm2z2Fw5T0bo_h4h_7D6xU9QbFjC5LY0IcWtjZkYJJIxcGVuGmmOToqeAYsrWRrNUrRI5gsvnORFYM2h68iWK0PP99tmV88TT09A-BdEiAm59J0vZW27r6NaPiUs3BH1hqxmaNDNi7Z1FDXespEzyyR/s728/go_threat.png)

**Threatest** 是一个用于端到端测试威胁检测的 Go 框架。**威胁**允许你**引爆**一种攻击技术，并验证你期望的警报是在你最喜欢的安全平台上生成的。

## 概念

### 雷管

一个**引爆器**描述了一个攻击技术如何以及在哪里被执行。

支持的雷管:

*   本地命令执行
*   SSH 命令执行
*   层云红队
*   AWS 雷管

### 警报匹配器

**警报匹配器**是一个特定于平台的集成，可以检查是否触发了预期的警报。

支持的警报匹配器:

*   数据狗安全信号

### 引爆和警报关联

每一次爆炸都有一个 UUID。该 UUID 反映在爆炸中，并用于确保匹配的警报与该爆炸完全对应。

这样做的方式取决于雷管；例如，Stratus 红队和 AWS 雷管在用户代理中注入它；SSH 雷管使用包含 UUID 的父进程。

## 样本用法

完整的使用示例见[示例](https://github.com/DataDog/threatest/blob/main/examples)。

### 测试 Stratus 红队触发的 Datadog 云 SIEM 信号

```
threatest := Threatest()

threatest.Scenario("AWS console login").
  WhenDetonating(StratusRedTeamTechnique("aws.initial-access.console-login-without-mfa")).
  Expect(DatadogSecuritySignal("AWS Console login without MFA").WithSeverity("medium")).
  WithTimeout(15 * time.Minute)

assert.NoError(t, threatest.Run())
```

### 测试通过 SSH 运行命令触发的 Datadog 云工作负载安全信号

```
ssh, _ := NewSSHCommandExecutor("test-box", "", "")

threatest := Threatest()

threatest.Scenario("curl to metadata service").
  WhenDetonating(NewCommandDetonator(ssh, "curl http://169.254.169.254 --connect-timeout 1")).
  Expect(DatadogSecuritySignal("EC2 Instance Metadata Service Accessed via Network Utility"))

assert.NoError(t, threatest.Run())
```

[Click Here To Download](https://github.com/DataDog/threatest)