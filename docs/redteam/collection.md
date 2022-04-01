# 信息搜集

在[ATT&CK](https://attack.mitre.org/)模型中，称为侦查阶段（Reconnaissance）。包括以下10个方面，

- 主动扫描
  - IP块扫描
  - 漏洞扫描
- 搜集受害者主机信息
  - 硬件
  - 软件
  - 固件
  - 客户端信息
- 搜集受害者身份信息
  - 凭据
  - 电子邮箱
  - 员工姓名
- 搜集受害者网络信息
  - 域名属性
  - DNS
  - 网络可信依赖
  - 网络拓扑
  - IP地址
  - 网络安全设备
- 搜集受害者组织信息
  - 确定物理位置
  - 业务关系
  - 确定业务周期
  - 确定角色
- 通过网络钓鱼搜集信息
  - 鱼叉式钓鱼攻击
  - 鱼叉式钓鱼链接
- 从非公开源搜集信息
- 从公开技术数据库搜集信息
- 搜集公开网站/域
- 搜集受害者自有网站

?> 在渗透测试中，信息搜集（特指外部信息搜集）是一个非常重要的环节。”知己知彼，百战不殆“，搜集足够的信息，可以提高渗透测试成功的概率。

| 技巧                     | 子内容                 | 示例工具 |
| ------------------------ | ---------------------- | -------- |
   | 主动扫描                 | IP块扫描<br />漏洞扫描 |          |
   | 搜集受害者主机信息       |                        |          |
   | 搜集受害者身份信息       |                        |          |
   | 搜集受害者网络信息       |                        |          |
   | 搜集受害者组织信息       |                        |          |
   | 通过网络钓鱼搜集信息     |                        |          |
   | 从非公开源搜集信息       |                        |          |
   | 从公开技术数据库搜集信息 |                        |          |
   | 搜集公开网站/域          |                        |          |
   | 搜集受害者自有网站       |                        |          |

## 主动扫描

### IP块扫描

`nmap`

[masscan](https://github.com/robertdavidgraham/masscan)

### 漏洞扫描

masscan -p1-65535 

## 搜集受害者身份信息

- Google hacking
- github

## 搜集受害者网络信息

### 域名信息查询（WHOIS）
HWOIS原始数据包含联系数据（包括注册人联系方式、管理人联系方式、技术人员联系方式）和有关注册商、域名状态和重要日期等信息。
### 子域名

收集子域名的方法主要有

- 暴力枚举
- DNS历史解析
- SSL证书
  - https://crt.sh/
  - https://search.censys.io/certificates?q=
- 搜索引擎
  - site:example.com
  - [ZoomEye](https://www.zoomeye.org/)
  - [Fofa](https://fofa.so/)
  - [Shodan](https://www.shodan.io/)
  - [Censys](https://search.censys.io/)
- 文本分析（HTML、JavaScript）
- 域传送漏洞

- 



PENTESTER LAND，[Subdomains Enumeration Cheat Sheet](https://pentester.land/cheatsheets/2018/11/14/subdomains-enumeration-cheatsheet.html)

## 搜集受害者组织信息

- 天眼查
- 企查查

## 从公开技术数据库搜集信息

## 搜集公开网站/域

## 搜索受害者自有网站

- 通过SSL证书
- 通过图标
- 子域名

[WHOIS](https://whois.icann.org/zh/%E5%85%B3%E4%BA%8E-whois)

- [站长之家Whois查询](https://whois.chinaz.com/)



