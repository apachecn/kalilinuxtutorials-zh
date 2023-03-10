# Osmedeus:用于攻击性安全的工作流引擎

> 原文：<https://kalilinuxtutorials.com/osmedeus/>

[![](img/b53a9cd548eca39f4c08724b4f19f7f7.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhQw9Qac2dCiXcv7KrvoyLxGJSBC4LZnT5ni48wrfcm9_-oUXRbLlVzxV9D3zMXy5tT2FnSOszrbDgphg_o2AJpnKlu36AA1SDbEjdky3FetEYCMKyYYeamznar7idEaTD25vszKIsc9zYcrARI7_UuJI39WXar3oVI3BnihuvOpDw_iaQESGe2tsTY/s728/logo-transparent%20(1).png)

Osmedeus 是一个用于攻击性安全的工作流引擎。

**安装**

注意，你需要一些必要的工具，比如`**curl, wget, git, zip**`和作为**根**登录来开始

**bash-c " $(curl-fsSL https://raw . githubusercontent . com/osme deus/osme deus-base/master/install . sh)"**

**从源头制造引擎**

确保您安装了`**golang >= v1.17**`

**mkdir-p $ go path/src/github . com/j3ssi
git clone–depth = 1 https://github . com/j3ssi/osmedus $ go path/src/github . com/j3ssi/osmedus
CD $ go path/src/github . com/j3ssi/osmedus
制作**

**用途**

**扫描用法:
osmedeus Scan-f[流名]-T[目标]
osmedeus Scan-m[module path]-T[targets file]
osmedeus Scan-f/path/to/flow . YAML-T[目标]
osmedeus Scan-m/path/to/module . YAML-T[目标]–params ' port = 9200 '
osmedeus Scan-m/path/to/module . YAML-T[目标]-l/tmlosme deus/core/workflow/test/dirbscan . YAML-T list _ of _ URLs . txt
osme deus scan–wf folder ~/custom-workflow/-f your-custom-workflow-T list _ of _ URLs . txt
提供程序用法:
osmedeus 提供程序构建
osmedeus 提供程序构建–令牌 XXX–rebuild–IC
osme deus 提供程序创建–name ' sample '
osme deus 提供程序运行状况–调试
云用法:“
osme deus cloud–chunk-c 10-f[flow name]-t[targets file]
实用程序用法:
osme deus health
osme deus version–JSON
osme deus utils tmux ls
osme deus utils tmux logs-A-l 10
osme deus utils PS
osme deus utils PS–proc ' jaeles '
osme deus utils cron–cmd ' osme deus**

[**Download**](https://github.com/j3ssie/osmedeus)