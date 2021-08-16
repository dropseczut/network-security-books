# 虚拟机

虚拟机允许在一台计算机上同时运行多个不同的操作系统，每个操作系统的运行方式与通常操作系统或应用在主机硬件上使用的运行方式相同，也就说，一台计算机可以虚拟化为多台计算机进行使用。

!> 相关实验和工具要在虚拟机里进行，可以减少宿主机系统感染病毒风险，避免频繁重装系统。

目前流行的桌面虚拟机软件有`VMware`和`VirtualBox`两种。在教程中，我们使用`VMware Workstation Pro`。

## 安装Workstation 16 Pro for Windows

1. 下载[安装包](https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html)
2. 运行安装程序，按照提示完成安装

[官方中文指南](https://docs.vmware.com/cn/VMware-Workstation-Pro/16.0/com.vmware.ws.using.doc/GUID-F5A7B3CB-9141-458B-A256-E0C3EA805AAA.html)

## 快照

!> 合理使用快照功能，可以方便开展工作，避免重复安装系统。

拍摄快照，保留虚拟机状态，可以反复恢复为相同的状态，包括内存、设置和磁盘状态。

比如，初始安装系统，可以拍摄一个快照，以便我们可以随时恢复到初始状态。

## 网络

默认支持3种网络连接配置，分别是桥接模式、NAT模式和仅主机模式。

在创建虚拟机时可以选择网络连接，也可以在`编辑虚拟机设置`中选择`网络适配器`进行修改。

**桥接模式**

连接物理网络。

**NAT模式**

用于共享主机的IP地址。虚拟机在外部网络中不必具有自己的 IP 地址。主机系统上会建立单独的专用网络。在默认配置中，虚拟机会在此专用网络中通过 DHCP 服务器获取地址。虚拟机和主机系统共享一个网络标识，此标识在外部网络中不可见。

!> 建议使用NAT模式！保护虚拟机不被未授权访问。

**仅主机模式**

与主机共享的专用网络。仅主机模式网络连接使用对主机操作系统可见的虚拟网络适配器，在虚拟机和主机系统之间提供网络连接。

## 安装Kali Linux

1. 访问[链接](https://www.kali.org/get-kali/#kali-virtual-machines)，下载对应的虚拟机文件，解压打开即可。默认用户名密码为`kali/kali`。
2. 下载ISO文件，按照提示安装。[官方指南](https://www.kali.org/docs/installation/hard-disk-install/)

## 任务

- 安装VMware Workstation Pro 16
- 安装虚拟机，包括Windows 10和Kali Linux