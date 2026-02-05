# 安全安装

## 🔒 在 Debian/Ubuntu 上提高安全性的安装

为了在基于 Debian 的 Linux 发行版（如 Ubuntu）上增强安全性，最佳实践是在专用的低权限用户账户下运行 **MeshCentral**。这可以防止服务器对系统进行未经授权的更改。

> ⚠️ **重要：** 以受限权限运行会禁用 MeshCentral 的**自更新功能**。更新必须手动执行。此外，此设置**需要使用外部数据库（如 MongoDB）**，因为主数据文件夹将是只读的。

-----

### 1\. 创建低权限用户

首先创建一个名为 `meshcentral` 的系统用户。该用户将被限制无法登录，也无法更改其指定目录之外的文件。

```shell
sudo useradd -r -d /opt/meshcentral -s /sbin/nologin meshcentral
```

### 2\. 安装 MeshCentral

接下来，创建安装目录并使用 NPM 安装软件包。

```shell
# 创建安装文件夹
sudo mkdir /opt/meshcentral

# 切换到安装目录
cd /opt/meshcentral

# 安装 MeshCentral（以创建的用户身份）
sudo -u meshcentral npm install meshcentral
```

### 3\. 初始化数据文件夹

在新的低权限用户下运行一次服务器，以生成必要的数据文件夹并安装任何初始依赖项。

```shell
# 以 meshcentral 用户身份运行一次
sudo -u meshcentral node ./node_modules/meshcentral
```

服务器运行并创建文件夹后，按 **CTRL-C** 停止进程。

### 4\. 限制权限

现在，设置所有权和权限，以确保 `meshcentral` 用户对应用程序代码具有**只读访问权限**，从而增强安全性。

```shell
# 将所有文件的所有权更改为 meshcentral 用户和组
sudo chown -R meshcentral:meshcentral /opt/meshcentral

# 为 meshcentral 用户设置数据文件夹的读取/执行权限
# 注意：meshcentral-* 指的是 meshcentral-data、meshcentral-files 等。
sudo chmod -R 755 /opt/meshcentral/
```

### 5\. 为功能调整写入权限（可选）

在受限环境中，您需要明确授予对服务器在运行期间需要修改的特定子文件夹的写入权限。

#### A. 文件上传/下载

如果您计划使用 MeshCentral 的文件传输功能，服务器需要读取和写入 `meshcentral-files` 文件夹：

```shell
sudo chmod -R 755 /opt/meshcentral/meshcentral-files
```

#### B. Let's Encrypt 支持

如果您计划使用 MeshCentral 内置的 **Let's Encrypt** 支持，您必须使其证书文件夹可写，以避免出现 `ACCES: permission denied` 异常：

```shell
# 如果必要的子文件夹不存在，则创建它们
sudo mkdir -p /opt/meshcentral/meshcentral-data/letsencrypt

# 授予对 letsencrypt 文件夹的写入权限
sudo chmod -R 775 /opt/meshcentral/meshcentral-data/letsencrypt
```

### 6\. 手动服务器更新

由于 `meshcentral` 用户缺少对 `/node_modules` 目录的写入权限，服务器无法自行更新。要执行手动更新：

1.  使用 `systemctl`（或您的服务管理器）**停止** MeshCentral 服务器进程。
2.  运行以下命令：

<!-- end list -->

```shell
cd /opt/meshcentral

# 通过 NPM 更新 MeshCentral 软件包（需要 sudo/root 权限）
sudo npm install meshcentral

# 重新将所有权设置为 meshcentral 用户
sudo chown -R meshcentral:meshcentral /opt/meshcentral
```

3.  使用 `systemctl` **重新启动** MeshCentral 服务器。

此过程将服务器更新到 NPM 上的最新版本，并重新应用严格的权限。