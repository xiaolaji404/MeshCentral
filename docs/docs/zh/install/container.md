# 🐳 容器 (OCI 规范)

[开放容器倡议](https://opencontainers.org/)

以下部分介绍如何使用 Docker 或 Podman 在本地安装 MeshCentral。
在语法方面，将默认使用 docker。这样做是因为 podman 也支持这种语法。<br>

🔗 参考资料：

- [Docker](https://www.docker.com/)  
- [Podman](https://podman.io/)

!!!warning
    请勿使用 MeshCentral 内置的更新功能（使用容器时）。<br>
    请以"docker 方式"更新容器，即通过更新镜像本身来更新。

### 🏷️ 基础标签：

| 标签名称 | 说明 |
|--------|-----|
| `master` | 此标签属于在每次提交到主分支时构建的镜像，因此包含最新代码。 |
| `latest` | 此标签使用 MeshCentral 的最新发布版本。 |
| `1.1.51` | 您也可以使用特定标签指定具体的 MeshCentral 版本，例如：`ghcr.io/ylianst/meshcentral:1.1.43` |

### 所有标签

以下所有 master 标签跟随 MeshCentral 的 master 分支，latest 和带版本号的标签跟随发布版本。

| 标签名称 | 说明 |
| -------- | ----------- |
| `master-slim` | 不包含数据库包的 Docker 镜像，最为精简。使用 NeDB。 |
| `master-mongodb` | 安装了 MongoDB 包的 Docker 镜像。 |
| `master-postgresql` | 安装了 PostgreSQL 包的 Docker 镜像 |
| `master-mysql` | 安装了 MySQL 包的 Docker 镜像 |
| `1.1.51-slim` 和 `latest-slim` | 不包含数据库包的 Docker 镜像，最为精简。使用 NeDB。 |
| `1.1.51-mongodb` 和 `latest-mongodb` | 安装了 MongoDB 包的 Docker 镜像。 |
| `1.1.51-postgresql` 和 `latest-postgresql` | 安装了 PostgreSQL 包的 Docker 镜像。 |
| `1.1.51-mysql` 和 `latest-mysql` | 安装了 MySQL 包的 Docker 镜像。 |

---
> **📌 注意：**
有关容器状态的更多信息，请参阅[此页面](https://github.com/Ylianst/MeshCentral/pkgs/container/meshcentral)。
---

## 🐋 Docker/Podman

适用于 Docker 和 Podman 等单机部署。

### 拉取镜像：

要拉取容器镜像，请使用以下容器仓库。

```sh
docker pull ghcr.io/ylianst/meshcentral:latest
```

### Docker CLI：

如果您想从终端运行容器，可以使用以下命令：

```sh linenums="1"
docker run -d \
  --name meshcentral \
  --restart unless-stopped \
  -p 80:80 \
  -p 443:443 \
  -v data:/opt/meshcentral/meshcentral-data \
  -v user_files:/opt/meshcentral/meshcentral-files \
  -v backup:/opt/meshcentral/meshcentral-backups \
  -v web:/opt/meshcentral/meshcentral-web \
  ghcr.io/ylianst/meshcentral:latest
```

### Docker Compose：

如果您想使用 docker compose yaml 文件，请参阅以下示例。

```yaml linenums="1"
services:
  meshcentral:
    image: ghcr.io/ylianst/meshcentral:latest
    environment:
      - DYNAMIC_CONFIG=false # 显示该选项但默认禁用它，以确保安全。
    volumes:
      - meshcentral-data:/opt/meshcentral/meshcentral-data
      - meshcentral-files:/opt/meshcentral/meshcentral-files
      - meshcentral-web:/opt/meshcentral/meshcentral-web
      - meshcentral-backups:/opt/meshcentral/meshcentral-backups
    ports:
      - "80:80"
      - "443:443"
volumes:
  meshcentral-data:
  meshcentral-files:
  meshcentral-web:
  meshcentral-backups:
```

有关环境变量，请参阅 [Dockerfile](https://github.com/Ylianst/MeshCentral/blob/5032755c2971955161105922e723461385a6c874/docker/Dockerfile#L70-L123)。

## ☸️ Kubernetes

###

> 使用 YAML 部署文件。

## 📚 额外资源

> [Github Docker 资源](https://github.com/Ylianst/MeshCentral/tree/master/docker)