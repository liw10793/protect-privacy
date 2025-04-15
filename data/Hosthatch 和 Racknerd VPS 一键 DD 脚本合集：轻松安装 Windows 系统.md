# Hosthatch 和 Racknerd VPS 一键 DD 脚本合集：轻松安装 Windows 系统

本文将详细介绍如何在 Hosthatch 和 Racknerd VPS 上使用 DD 脚本一键安装 Windows 系统，包含多种系统版本和实用技巧。

## 系统重装前的准备工作

在开始 DD 安装前，需要先安装必要的组件：

### Debian/Ubuntu 系统：
1. `apt-get install -y xz-utils openssl gawk file wget screen && screen -S os`

### RedHat/CentOS 系统：
1. `yum install -y xz openssl gawk file glibc-common wget screen && screen -S os`

如果安装过程中出现异常，建议刷新镜像缓存或更换镜像源：

- RedHat/CentOS：
  `yum makecache && yum update -y`

- Debian/Ubuntu：
  `apt update -y && apt dist-upgrade -y`

👉 [【点击查看】2025年最新 Racknerd 优惠码及特价云服务器方案汇总](https://bit.ly/Rack_Nerd)

## 智能一键安装脚本

这款 DD 脚本具有以下优势：
- 支持国内外各种 VPS 重装
- 特别优化了国内访问国外资源慢的情况
- 完美支持 Debian 11
- 专门针对甲骨文云服务器添加了 3 个 UEFI 支持选项（23-25）

安装命令：
1. `wget --no-check-certificate -O AutoReinstall.sh https://d.02es.com/AutoReinstall.sh && chmod a+x AutoReinstall.sh && bash AutoReinstall.sh`

安装过程说明：
- 输入 Y 确认 DD 后主机会自动获取 IP
- 输入 N 则需要自行设置 IP
- 系统会自动检测当前 IP，确认正确后按 Y，否则按 N 手动输入

## 25 合 1 系统选择及默认密码

脚本提供 25 种系统选择，输入对应数字即可安装：

1. CentOS 7.7 (密码: Pwd@CentOS)
2. CentOS 7 (密码: cxthhhhh.com)
3. CentOS 8 (密码: cxthhhhh.com)
...
12. Windows Server 2019 (密码: cxthhhhh.com)
...
23. Windows 7 Ent Lite (UEFI支持甲骨文)(密码: nat.ee)
24. Windows Server 2008 Lite (UEFI支持甲骨文)(密码: nat.ee)
25. Windows Server 2012 Lite (UEFI支持甲骨文)(密码: nat.ee)
99. 自定义镜像

## 重要注意事项

1. 在谷歌云原版系统上 DD 时，可能会出现子网掩码自动获取为 255.255.255.255 的情况，需要手动修改为正确的值（如 255.255.255.0），否则安装完成后主机可能离线。

2. Oracle Cloud（甲骨文云）建议选择 23-25 选项进行 DD，基础系统最好选择 Ubuntu，CentOS 系统可能无法成功安装。

## 自定义 DD 包安装方法

如果需要使用自定义 DD 包，可以使用以下脚本（需补全 DD 包直连地址）：

1. `wget --no-check-certificate -qO InstallNET.sh 'https://d.02es.com/InstallNET.sh' && bash InstallNET.sh -dd '[Windows DD包直链地址]'`

## 精简版 DD 包推荐

如果没有自己的 DD 包，可以使用博主提供的精简版 DD 包，选择需要的系统版本后输入一键脚本即可安装。

小技巧：Windows 服务器开启 Ping 功能的方法：
1. 按下 `Win+R` 打开运行窗口
2. 输入相应命令即可