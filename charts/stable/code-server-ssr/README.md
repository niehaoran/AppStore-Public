# code-server-ssr

## 介绍

支持 SSR 代理的在线 VSCode 开发环境

## 主要功能

- Kubernetes 应用部署
- 资源限制和请求配置
- 环境变量配置
- 服务暴露配置

## 配置参数说明

| 参数名称                  | 描述            | 类型    | 默认值                    |
| ------------------------- | --------------- | ------- | ------------------------- |
| `replicaCount`            | 副本数量        | integer | 1                         |
| `image.repository`        | 应用名称        | string  | nidexiong/code-server-ssr |
| `image.tag`               | 应用标签        | string  | latest                    |
| `image.pullPolicy`        | 应用拉取策略    | string  | Always                    |
| `resources.limits.cpu`    | CPU 限制        | string  | 1000m                     |
| `resources.limits.memory` | 内存限制        | string  | 2000Mi                    |
| `env.PASSWORD.value`      | VSCode 登录密码 | string  | "changeme"                |

## 部署步骤

1. 输入配置参数
2. 选择拥有足够配置应用空间
3. 立即部署

# Proxy Manager

一个简单但功能强大的代理管理工具，支持 Shadowsocks 节点管理和 Git 自动代理配置。

## 功能特性

- 多节点管理
- Git 自动代理配置
- 代理状态检测
- 连接测试
- 交互式菜单界面

## 快速开始

### 交互式菜单

在终端中输入以下命令启动交互式菜单：

```bash
proxy-manager
```

菜单选项：

```
SS 代理管理
1. 显示可用节点
2. 启用节点
3. 禁用代理
4. 检查代理状态
5. 测试代理连接
6. 退出
```

### 命令行使用

```bash
# 启用指定节点
proxy-manager enable <node_id>

# 禁用代理
proxy-manager disable

# 查看状态
proxy-manager status

# 测试连接
proxy-manager test
```

## 代理使用说明

### 默认配置

Git 命令已默认配置为使用代理，无需额外设置。

### 访问外网

对于其他需要使用代理的命令，需要加上 proxychains4 前缀：

```bash
# 示例：使用 curl 访问 Google
proxychains4 curl www.google.com

# 示例：使用 wget 下载文件
proxychains4 wget https://example.com/file

# 示例：使用 npm 安装包
proxychains4 npm install package-name
```

## 常用编程环境安装指南

### 基本工具

```bash
# 更新系统
apt update
apt upgrade -y

# 安装基本开发工具
apt install -y build-essential git curl wget
```

### Node.js 环境

```bash
# 使用 淘宝镜像源 安装 nvm
curl -o- https://gitee.com/mirrors/nvm/raw/v0.39.0/install.sh | bash
source ~/.bashrc

# 设置 npm 淘宝镜像
npm config set registry https://registry.npmmirror.com

# 安装 Node.js
nvm install --lts  # 安装 LTS 版本
# 或者安装最新版
nvm install node

# 安装 yarn
npm install -g yarn
# 设置 yarn 淘宝镜像
yarn config set registry https://registry.npmmirror.com
```

### Python 环境

```bash
# Python 3
apt install -y python3 python3-pip python3-dev

# 设置 pip 清华源
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

# 安装虚拟环境工具
pip3 install virtualenv

# Poetry（Python 依赖管理工具）
curl -sSL https://install.python-poetry.org | python3 -
# 配置国内源
poetry config repositories.tuna https://pypi.tuna.tsinghua.edu.cn/simple
```

### Java 环境

```bash
# OpenJDK 17
apt install -y openjdk-17-jdk

# Maven
apt install -y maven
# 配置 Maven 阿里云镜像，需要编辑 /etc/maven/settings.xml

# Gradle
apt install -y gradle
# Gradle 国内镜像配置，需要编辑 ~/.gradle/init.gradle
```

### Go 环境

```bash
# 安装 Go
apt install -y golang-go

# 设置 GOPROXY 国内源
go env -w GOPROXY=https://goproxy.cn,direct

# 设置 GOPATH（需要添加到 ~/.bashrc）
echo 'export GOPATH=$HOME/go' >> ~/.bashrc
echo 'export PATH=$PATH:$GOPATH/bin' >> ~/.bashrc
source ~/.bashrc
```

### Rust 环境

```bash
# 安装 Rust（使用国内镜像）
export RUSTUP_DIST_SERVER=https://mirrors.ustc.edu.cn/rust-static
export RUSTUP_UPDATE_ROOT=https://mirrors.ustc.edu.cn/rust-static/rustup
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# 配置 Cargo 国内镜像，编辑 ~/.cargo/config
source $HOME/.cargo/env
```

## 常见问题

### 1. 代理无法连接？

检查步骤：

1. 使用 `proxy-manager status` 检查代理状态
2. 使用 `proxy-manager test` 测试连接
3. 如果测试失败，尝试更换其他节点

### 2. Git 提示连接超时？

可能原因：

- 代理节点不稳定
- 代理未正确启动

解决方案：

1. 检查代理状态
2. 禁用后重新启用代理
3. 尝试其他节点

## 注意事项

- 首次使用建议先测试代理连接
- 定期检查代理状态
- 如遇连接问题，可尝试重启代理服务

## 技术支持

如有问题，请提交 Issue 或通过邮箱联系：

- 邮箱：179866495@qq.com

## 作者说明

本工具由 [179866495@qq.com](mailto:179866495@qq.com) 开发和维护。

如果您觉得这个工具对您有帮助，欢迎打赏支持后续开发：

<div align="center">
  <img src="https://assets.yunna.net/i/2025/01/28/zh3gj5.jpg" alt="打赏二维码" width="200">
</div>

您的支持是我持续改进这个工具的动力！

## 故障排除

1. Pod 无法启动

- 检查资源限制是否合理
- 检查应用是否存在且可访问

2. 服务无法访问

- 检查服务端口配置
- 检查 Pod 运行状态
