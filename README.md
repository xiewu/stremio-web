# Stremio - Freedom to Stream

> 这是 Stremio Web 的 fork 版本，配置了自动部署到 Docker Swarm 集群。

## 🚀 自动部署配置

本项目使用**主机 Webhook 方案**实现自动部署：

- ✅ 完全免费（不需要 Portainer Business）
- ✅ 安全可靠（HMAC 签名验证）
- ✅ 可定制性强（可添加自定义部署逻辑）

### 快速开始

1. **在 Manager 节点安装 Webhook 服务**
   ```bash
   ssh root@<MANAGER_IP>
   bash scripts/setup-webhook.sh
   ```

2. **配置 GitHub Secrets**
   - `DOCKER_USERNAME`: Docker Hub 用户名
   - `DOCKER_PASSWORD`: Docker Hub Token
   - `WEBHOOK_URL`: Webhook 地址
   - `WEBHOOK_SECRET`: 安装脚本生成的密钥

3. **推送代码自动部署**
   ```bash
   git push origin release
   ```

### 部署文档

- [主机 Webhook 配置](./WEBHOOK-SETUP.md) - 详细配置步骤
- [部署方案对比](./DEPLOYMENT-CHOICE.md) - 三种方案对比
- [完整部署指南](./DEPLOYMENT.md) - 部署总览

---

[![Build](https://github.com/Stremio/stremio-web/actions/workflows/build.yml/badge.svg)](https://github.com/Stremio/stremio-web/actions/workflows/build.yml)
[![Github Page](https://img.shields.io/website?label=Page&logo=github&up_message=online&down_message=offline&url=https%3A%2F%2Fstremio.github.io%2Fstremio-web%2F)](https://stremio.github.io/stremio-web/development)

Stremio is a modern media center that's a one-stop solution for your video entertainment. You discover, watch and organize video content from easy to install addons.

## Build

### Prerequisites

* Node.js 12 or higher
* [pnpm](https://pnpm.io/installation) 10 or higher

### Install dependencies

```bash
pnpm install
```

### Start development server

```bash
pnpm start
```

### Production build

```bash
pnpm run build
```

### Run with Docker

```bash
docker build -t stremio-web .
docker run -p 8080:8080 stremio-web
```

## Screenshots

### Board

![Board](/assets/screenshots/board.png)

### Discover

![Discover](/assets/screenshots/discover.png)

### Meta Details

![Meta Details](/assets/screenshots/metadetails.png)

## Deployment

This fork includes automated deployment to Docker Swarm cluster.

### Production Environment

- **URL**: https://live.xlab.host
- **Branch**: `release`
- **Auto-deploy**: Enabled

### Quick Start

**Option 1: Webhook Deployment (Recommended - More Secure)**
```bash
# No GitHub Secrets needed, uses Deploy Keys
./scripts/setup-webhook-deployment.sh
```

**Option 2: GitHub Actions Deployment**
```bash
# Requires GitHub Secrets configuration
export DOCKER_USERNAME=your-dockerhub-username
./scripts/setup-deployment.sh
```

See [Deployment Comparison](./DEPLOYMENT-COMPARISON.md) to choose the right method.

### Documentation

- [Deployment Comparison](./DEPLOYMENT-COMPARISON.md) - Choose the right deployment method
- [Deployment Flow Diagrams](./docs/deployment-flow.md) - Visual comparison of both methods
- [Quick Start Guide](./QUICK-START.md) - Get started in 5 minutes (GitHub Actions)
- [Webhook Deployment](./DEPLOYMENT-WEBHOOK.md) - Secure deployment with Deploy Keys (Recommended)
- [Deployment Guide](./DEPLOYMENT.md) - Complete deployment documentation (GitHub Actions)
- [Deployment Checklist](./.github/DEPLOYMENT_CHECKLIST.md) - Configuration checklist
- [Security Guide](./SECURITY.md) - Security best practices and SSH key management

### Workflow

1. Develop on `development` branch
2. Push changes to `development`
3. Auto-create PR (development → release)
4. Review and merge PR
5. Auto-deploy to production

## License

Stremio is copyright 2017-2023 Smart code and available under GPLv2 license. See the [LICENSE](/LICENSE.md) file in the project for more information.
