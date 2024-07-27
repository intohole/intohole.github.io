---
layout: post
title: Centos 安装 mongodb
tags: [tech]
city: 南京
---


在 CentOS 系统上安装 MongoDB 可以通过多种方式进行，包括使用包管理器（如 yum）或直接从 MongoDB 官方仓库安装。以下是使用官方 MongoDB 仓库在 CentOS 上安装 MongoDB 的步骤：
### 1. 配置 MongoDB 仓库
首先，您需要配置 MongoDB 的 Yum 仓库。
1. 创建一个 `/etc/yum.repos.d/mongodb-org-6.0.repo` 文件，以便您可以从 MongoDB 仓库安装软件包。这个文件将包含 MongoDB 仓库的详细信息。
   ```bash
   [mongodb-org-6.0]
   name=MongoDB Repository
   baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/$version/x86_64/
   gpgcheck=1
   enabled=1
   gpgkey=https://www.mongodb.org/static/pgp/server-$version.asc
   ```
   请确保将 `$releasever` 替换为您的 CentOS 版本号。

   (mongodb 版本号)[https://repo.mongodb.org/yum/redhat/]
3. 导入 MongoDB 公钥：
   ```bash
   rpm --import https://www.mongodb.org/static/pgp/server-6.0.asc
   ```
### 2. 安装 MongoDB 包
1. 使用 `yum` 命令安装 MongoDB：
   ```bash
   sudo yum install -y mongodb-org
   ```
   这将安装 MongoDB 服务及其所有依赖项。
### 3. 启动 MongoDB 服务
1. 启动 MongoDB 服务：
   ```bash
   sudo systemctl start mongod
   ```
2. 检查 MongoDB 服务的状态：
   ```bash
   sudo systemctl status mongod
   ```
3. 设置 MongoDB 服务在系统启动时自动启动：
   ```bash
   sudo systemctl enable mongod
   ```
### 4. 验证安装
1. 连接到 MongoDB 服务器：
   ```bash
   mongo --eval 'db.runCommand({ connectionStatus: 1 })'
   ```
   如果一切正常，这将显示有关 MongoDB 实例的信息。
### 注意事项
- 确保您的防火墙设置允许 MongoDB 的默认端口（27017）。
- MongoDB 的配置文件通常位于 `/etc/mongod.conf`。您可以在这里调整各种设置，例如数据目录和网络配置。
- 如果您计划将 MongoDB 用于生产环境，建议阅读 MongoDB 官方文档以了解更多关于配置和优化的信息。
以上步骤适用于安装 MongoDB 6.0 版本。如果您需要安装不同版本的 MongoDB，请相应地调整仓库配置文件中的版本号。
