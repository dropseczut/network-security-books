# Cobalt Strike

[Cobalt Strike](https://www.cobaltstrike.com/)是一款商业化渗透测试工具，人们称之为CS。其基于Java语言开发，采用C/S架构，具备GUI，适合团队协作。

![Features Screenshot](https://static.helpsystems.com/cobalt-strike/img/features-screenshot-1.png)

## 主要功能

## 安装和设置

### 系统要求

系统配置最低要求：

- 处理器：2GHz+
- 内存：2GB
- 硬盘：500MB

推荐Java环境

- OpenJDK 11
- Oracle Java 11
- Oracle Java 1.8

配置OpenJDK环境

### 安装

### 启动

Cobalt Strike分为客户端和服务端。

启动teamserver

```
./teamserver 
```

第一个参数为必选参数，指定可访问的IP地址。

第二个参数为客户端连接团队服务器的密码。

第三个参数是可选的，指定C2文件。

第四个参数是可选的，以YYYY-MM-DD的格式指定终止执行日期。团队服务器将日期设置到生成的Beacon中。

#### 客户端

![img](https://www.cobaltstrike.com/images/connect.png)