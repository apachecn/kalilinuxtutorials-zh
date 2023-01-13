# 得到回应:检测 NBT-NS 和 LLMNR 欺骗的工具

> 原文：<https://kalilinuxtutorials.com/got-responded/>

得到回应是一个简单的工具，以检测 NBT 和 LLMNR 的欺骗和搞乱他们一点。Pentesters，Redteamers，甚至真正的攻击者都喜欢使用 Responder 这样的工具来欺骗 LLMNR 和/或 NBT-NS 响应。

还有一些很棒的工具可以帮助检测，比如[responder](https://github.com/codeexpress/respounder)。但我想自己弄清楚，同时添加一种方法，向使用这些欺骗工具的人推送“蜜糖”令牌(虚假广告凭据)。

**也读作-[FIR:快速事件响应](https://kalilinuxtutorials.com/fir-fast-incident-response/)**

**如何安装**

**git 克隆 https://github.com/joda32/got-responded.git
CD get-responsed
python 3-m venv responsed-env
source responsed-env/bin/activate
pip install-r requirements . txt**

**如何使用**

**简单模式**

这将启动它在默认模式下，将检查 LLMNR 和 NBT-NS 欺骗，但不会发送伪造的中小企业信用

**python get-responded . py**

[**Download**](https://github.com/joda32/got-responded)