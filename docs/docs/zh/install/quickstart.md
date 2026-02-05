# 快速开始

## 🚀 快速开始指南：使用NPM进行最基本的安装

MeshCentral 是跨平台的，由于主要使用 JavaScript 编写，几乎可以在任何地方运行。本指南介绍使用 **NPM** 入门的最简单方法。

### 🛠️ 基础设置

唯一的先决条件是 **Node.js** 和 **npm**。

-----

#### 1\. 安装 Node.js

  * **Linux:** 在[这里](https://nodejs.org/en/download/package-manager/all)找到适合您发行版的安装说明。
  * **Windows:** 从官方网站[这里](https://nodejs.org/en)下载安装程序。

> 🪟 **Windows 用户：** 如果您更喜欢自动化的安装方式，可以跳过手动安装，直接下载 **Windows MeshCentral 安装程序**。不过，这**不推荐高级用户使用**。
> [下载 Windows MeshCentral 安装程序](https://meshcentral.com/tools/MeshCentralInstaller.exe)

-----

#### 2\. 安装并启动 MeshCentral

创建一个专用目录（例如 `/opt/meshcentral`），然后在终端中运行以下命令。

> ⚠️ 使用 `npm install meshcentral` 命令时**不要**使用 `sudo`。

```shell
# 示例：创建并进入目录
mkdir -p /opt/meshcentral
cd /opt/meshcentral

# 安装 MeshCentral 包
npm install meshcentral

# 启动服务器
node node_modules/meshcentral
```

就这样！MeshCentral 现在将自动完成设置，并开始管理**本地网络**中安装了 MeshAgent 的计算机。

#### 作为服务运行

要将 MeshCentral 作为持久化的后台服务运行（推荐用于生产环境），请在启动服务器时使用 --install 参数。有关操作系统特定的服务设置详情，请参阅 MeshCentral 文档。

-----

### ⚙️ 配置与自定义

#### 默认模式和初始访问

默认情况下，MeshCentral 以**仅局域网模式**启动。代理使用本地网络多播来查找服务器。

  * 您访问服务器时创建的第一个用户账户将自动成为**服务器管理员**。在网页浏览器中访问登录页面并立即创建您的账户。
  * 安装完成后，服务器设置存储在 **`config.json`** 文件中，该文件位于 **`meshcentral-data`** 文件夹内。

#### 高级配置

**`config.json`** 文件包含数百个用于深度自定义的选项，包括：

  * 通过设置已知的 DNS 名称，将服务器从仅局域网模式切换到 **WAN/混合模式**。
  * 使用您自己的**品牌**自定义服务器。
  * 设置 **SMTP 邮件服务器**或**短信服务**。

配置文件必须是有效的 **JSON**。您可以使用在线工具或 `jq` 等工具验证其格式。

您可以在 GitHub 仓库中找到示例配置文件作为参考：

  * [简单示例配置](https://github.com/Ylianst/MeshCentral/blob/master/sample-config.json)
  * [高级示例配置](https://github.com/Ylianst/MeshCentral/blob/master/sample-config-advanced.json)
  * [完整配置模式](https://github.com/Ylianst/MeshCentral/blob/master/meshcentral-config-schema.json)

-----

### 数据库和扩展说明

  * **数据库：** 默认情况下，MeshCentral 使用 **NeDB**，其内置数据库。对于高级用例和更好的性能，建议切换到 **MongoDB** 或基于 SQL 的解决方案，如 **Postgresql**。
  * **硬件：** MeshCentral 非常轻量级。您可以在小型平台上运行能够管理数百台设备的服务器，如 **Raspberry Pi** 或运行 Linux 的 **AWS t3.nano** 实例。
  * **服务模式：** 要将服务器作为后台服务运行，请使用 `--help` 参数启动以查看后台安装选项。

如需视觉指南，请查看官方 [YouTube 教程视频](https://www.youtube.com/@MeshCentral/videos)。

\<div class="video-wrapper"\>
  \<iframe src="[https://www.youtube.com/embed/LSiWuu71k\_U](https://www.youtube.com/embed/LSiWuu71k_U)" frameborder="0" allowfullscreen\>\</iframe\>
\</div\>

-----

想要了解更多关于配置服务器以进行 WAN 访问或切换到不同数据库的信息吗？