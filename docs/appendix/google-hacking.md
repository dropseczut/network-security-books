# Google Hacking

Google hacking，也称之为Google dorking，是攻击者利用谷歌搜索引擎的高级语法进行信息搜集的一种技术。

谷歌黑客数据库[Google Hacking Database，GHDB](https://www.exploit-db.com/google-hacking-database)汇总了大量的搜索技巧。

## 逻辑

| 逻辑操作符 | 描述                   | 示例                       |
| ---------- | ---------------------- | -------------------------- |
| `+`        | 包含关键字             | web +application +security |
| `-`        | 排除包含关键字的页面   | web application –security  |
| `\|`       | 包含其中任何一个关键字 | web application \|security |
| `""`       | 完全匹配字符串         | "web application security" |
| `.`        | 单字符匹配             | .eb application security   |
| `*`        | 单个单词匹配           | web * security             |

## 高级搜索语法

| 高级搜索运算符   | 描述                       | 示例               |
| ---------------- | -------------------------- | ------------------ |
| site:            | 搜索范围限制为指定域或站点 | site:example.com   |
| inurl:           | 在URL中搜索字符串          | inurl:password.txt |
| intitle:         | 在页面标题中搜索字符串     | intitle:"index of" |
| intext:          | 在页面正文中搜索字符串     | intext:passwd      |
| ext: / filetype: | 搜索指定类型的文件         | ext:pdf            |

