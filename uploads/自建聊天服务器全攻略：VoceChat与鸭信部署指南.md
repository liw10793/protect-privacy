# 自建聊天服务器全攻略：VoceChat与鸭信部署指南

## 前言

在寻找开源可自部署的即时通讯(IM)解决方案时，我发现了VoceChat和鸭信两款优秀工具。本文将详细介绍它们的部署流程，帮助你快速搭建私有聊天服务器。

## 一、服务器准备

### 1.1 云服务器选择

部署聊天服务需要一台性能适中的云服务器：

- **推荐配置**：2核2G内存
- **带宽选择**：根据预期用户量决定
- **机房位置**：国内机房访问更快但需备案
- **操作系统**：CentOS/Ubuntu/Debian均可

👉 [【点击查看】2025年最新雨云优惠码及特价云服务器方案汇总](https://bit.ly/RainYun)

### 1.2 远程连接设置

推荐使用MobaXterm进行SSH连接：

1. 下载安装MobaXterm免费版
2. 创建新Session
3. 输入服务器IP和登录凭证
4. 成功连接后即可操作服务器

## 二、VoceChat部署方案

### 2.1 Docker方式部署

bash
docker run -d --restart=always \
  -p 3009:3000 \
  --name vocechat-server \
  -v ~/.vocechat-server/data:/home/vocechat-server/data \
  privoce/vocechat-server:latest \
  --network.frontend_url "http://服务器IP:3009"

**访问方式**：`http://服务器IP:3009`

### 2.2 Nginx反向代理配置

bash
mkdir -p /etc/nginx/http.d/
nano /etc/nginx/http.d/chat.conf

配置文件示例：
nginx
server{
    listen 80;
    server_name yourdomain.com;
    location / {
        proxy_pass http://服务器IP:3009;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}

启动Nginx容器：
bash
docker run --name nginx -p 80:80 -d -v /etc/nginx/http.d/chat.conf:/etc/nginx/http.d/chat.conf nginx

### 2.3 Shell脚本安装

bash
curl -sSf https://s.voce.chat/install.sh | sh

安装完成后通过`IP:3000`访问

## 三、鸭信部署方案

### 3.1 基础环境准备

bash
git clone https://gitee.com/mirrors/DuckChat.git
cd DuckChat
unzip 1.1.7.zip
cd mirrors-DuckChat-master/DuckChat

### 3.2 脚本安装

bash
bash duckchat.sh

若80端口被占用，可修改端口：
bash
docker run -itd -p 8080:80 -p 2031:2031 -p 2021:2021 --name duckchat -v /DuckChat/mirrors-DuckChat-master/DuckChat:/home/gaga ccr.ccs.tencentyun.com/duckchat/gaga

访问地址：`http://IP:8080`

### 3.3 数据库配置

**MySQL配置**：
text
数据库地址：localhost
端口：3306
数据库名称：自定义
用户名：自定义
密码：自定义

**SQLite配置**：适合轻量级使用，无需额外安装数据库服务

## 四、使用建议

1. **移动端支持**：两款服务均有App支持
2. **性能优化**：根据用户量适当调整服务器配置
3. **安全建议**：
   - 定期备份数据
   - 使用HTTPS加密
   - 设置强密码

通过以上步骤，你可以轻松搭建私有聊天服务器，满足团队或个人的即时通讯需求。