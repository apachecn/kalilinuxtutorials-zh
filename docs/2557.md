# Graphql-Threat-Matrix:安全专家使用的 Graphql 威胁框架

> 原文：<https://kalilinuxtutorials.com/graphql-threat-matrix/>

[![](img/7fc93a63a9bc78b687f1782071dd06de.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjCZTAHfhXMrX7PnW5oBNGKY2jdwm3TKhMHTuQwOhTKubEVdfn5v0zWYXazjmNqgJLmjZtfuFTWEpG-BG2NAAn0Jh3ujwKaGxsTootA2Tni8Ge0hXM7NNX9JxSFJrWTEDAGVZTU5f4IdEWHT3ihuDqsvYoz2M0fdqrBXqyxcf0RiA7TTlQERBf71HLr/s728/graphql-threat-matrix%20(1).png)

graphql-threat-matrix 是为 bug 赏金猎人、安全研究人员和黑客构建的，用于帮助发现多个 graphql 实现中的漏洞。

GraphQL 实现如何解释和符合 GraphQL 规范的差异可能会导致安全漏洞和独特的攻击媒介。通过分析和比较不同实现中驱动安全风险的因素，GraphQL 生态系统可以做出更安全的部署决策，并共同提高所有实现的安全成熟度。

**图例**✅–默认启用
⚠️–默认禁用
❌–不支持

| 履行 | 确认 | 现场建议 | 查询深度限制 | 查询成本分析 | 自动持久化查询 | 反省 | 调试方式 | 批量请求 |
| wp-graphql | Thirty-eight | 981 号房 | ⚠️ | -好的 | -好的 | ⚠️ | ⚠️ | 981 号房 |
| graphql-php | Thirty-seven | 981 号房 | ⚠️ | ⚠️ | -好的 | 981 号房 | ⚠️ | ⚠️ |
| 阿波罗 | Thirty-four | 981 号房 | ⚠️ | ⚠️ | 981 号房 | 981 号房 | 981 号房 | 981 号房 |
| graph QL-瑜伽 | Thirty-four | 981 号房 | ⚠️ | -好的 | -好的 | ⚠️ | ⚠️ | ⚠️ |
| 石墨烯 | Thirty-four | 981 号房 | -好的 | -好的 | -好的 | 981 号房 | -好的 | ⚠️ |
| 阿里阿德涅 | Thirty-four | 981 号房 | ⚠️ | ⚠️ | -好的 | 981 号房 | ⚠️ | -好的 |
| 草莓 | Thirty-four | 981 号房 | ⚠️ | -好的 | -好的 | 981 号房 | -好的 | -好的 |
| graphql-ruby | Twenty-eight | 981 号房 | -好的 | ⚠️ | ⚠️ | 981 号房 | -好的 | 981 号房 |
| 桑格利亚汽酒 | Twenty-seven | 981 号房 | ⚠️ | ⚠️ | -好的 | 981 号房 | -好的 | ⚠️ |
| 塔尔提夫莱特 | Twenty-six | -好的 | -好的 | -好的 | -好的 | 981 号房 | -好的 | -好的 |
| java 语言 | Twenty-six | 981 号房 | ⚠️ | ⚠️ | -好的 | 981 号房 | -好的 | ⚠️ |
| 戈尔根 | Twenty-five | 981 号房 | -好的 | ⚠️ | ⚠️ | 981 号房 | ⚠️ | ⚠️ |
| 数据图表 | Twenty-five | 981 号房 | -好的 | -好的 | ⚠️ | 981 号房 | -好的 | -好的 |
| graphql-go | Twenty-four | 981 号房 | -好的 | -好的 | -好的 | 981 号房 | ⚠️ | -好的 |
| 杜松 | Twenty-four | -好的 | -好的 | -好的 | -好的 | 981 号房 | -好的 | ⚠️ |
| 戴安娜. jl | Ten | 981 号房 | -好的 | -好的 | -好的 | 981 号房 | -好的 | -好的 |
| gql-dart/gql | nine | 981 号房 | -好的 | -好的 | -好的 | 981 号房 | -好的 | -好的 |
| Agoo | one | -好的 | -好的 | -好的 | -好的 | 981 号房 | ⚠️ | -好的 |

## 用于渗透测试仪

使用 graphw00f 对目标 GraphQL API 进行指纹识别，并确定后端实现。

[**Download**](https://github.com/nicholasaleks/graphql-threat-matrix/)