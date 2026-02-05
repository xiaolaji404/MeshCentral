# 插件 - 安装与使用

!!!note
     插件本身不受 MeshCentral 主要开发人员的**支持**。如果您遇到 MeshCentral 问题，请确保在进一步故障排除之前**禁用所有插件**！

## 用例

某些功能请求可能不适合所有 MeshCentral 用户，因此可作为插件使用。此外，用户可以开发自己的插件 - 如下所述 - 以扩展功能或受益于将 MeshCentral 集成到其现有的应用环境中。

## 公开可用插件列表

<https://github.com/topics/meshcentral-plugin>

## 插件安装

1. 首先，请确保在配置中启用插件
   >"plugins": {
   >    "enabled": true
   >},
2. 如果您需要更改配置，请重新启动 MeshCentral。
2. 以完全管理员身份登录 MeshCentral。
3. 转到 `我的服务器` -> `插件`，然后点击下载插件按钮。
4. 将打开一个对话框，要求输入 URL，例如输入：<https://github.com/ryanblenis/MeshCentral-ScriptTask>
5. 插件将显示在下载按钮下方的插件列表中，您现在可以配置和启用/禁用它。

# 插件 - 开发与钩子

!!!note
     插件本身不受 MeshCentral 主要开发人员的**支持**。如果您遇到 MeshCentral 问题，请确保在进一步故障排除之前**禁用所有插件**！

## 概述

并非所有功能请求都适合所有 MeshCentral 用户，因此无法直接集成到 MeshCentral 中。然而，与其维护 MeshCentral 的完整分支，不如使用钩子并为其编写插件来扩展 MeshCentral 的功能，这要容易得多。

## 插件结构：

    - plugin_name/
    -- config.json
    -- plugin_name.js
    -- modules_meshcore/ // 可选
    --- plugin_name.js 	// 可选

## 插件配置文件

位于项目根文件夹中名为 `config.json` 的文件内的有效 JSON 对象。示例：

    {
      "name": "Plugin Name",
      "shortName": "plugin_name",
      "version": "0.0.0",
      "author": "Author Name",
      "description": "Short Description of the plugin",
      "hasAdminPanel": false,
      "homepage": "https://www.example.com",
      "changelogUrl": "https://raw.githubusercontent.com/User/Project/master/changelog.md",
      "configUrl": "https://raw.githubusercontent.com/User/Project/master/config.json",
      "downloadUrl": "https://github.com/User/Project/archive/master.zip",
      "repository": {
        "type": "git",
        "url": "https://github.com/User/Project.git"
      },
      "versionHistoryUrl": "https://api.github.com/repos/User/Project/tags",
      "meshCentralCompat": ">0.4.3"
    }

## Configuration File Properties

| 字段             | 必需 | 类型        | 说明                                                  |
| ----------------- | -------- | ----------- | ------------------------------------------------------------ |
| name              | 是      | string      | 插件的人类可读名称                         |
| shortName         | Yes      | string      | an alphanumeric, unique short identifier for the plugin (will be used to access your functions throughout the project |
| version           | Yes      | string      | the current version of the plugin                            |
| author            | No       | string      | the author's name                                            |
| description       | Yes      | string      | 插件功能的简短人类可读描述  |
| hasAdminPanel     | Yes      | boolean     | `true` 或 `false`，指示插件是否提供自己的管理界面 |
| homepage          | Yes      | string      | 项目主页的 URL                             |
| changelogUrl      | Yes      | string      | 项目变更日志的 URL                      |
| configUrl         | Yes      | string      | 项目 config.json 的 URL                    |
| downloadUrl       | Yes      | string      | 项目 ZIP 文件的 URL（用于安装/升级） |
| repository        | Yes      | JSON object | 包含以下属性                            |
| repository.type   | Yes      | string      | 有效值为 `git`，将来也将支持 `npm`。 |
| repository.url    | Yes      | string      | 项目仓库的 URL                          |
| versionHistoryUrl | No       | string      | 项目版本/标签的 URL                       |
| meshCentralCompat | Yes      | string      | 与 MeshCentral 服务器兼容性的最低版本字符串，可以格式化为 "0.1.2-c" 或 ">=0.1.2-c"。目前仅支持最低版本，不支持完整的语义检查。 |

## 插件钩子

本质上，钩子是代码中的位置，使开发人员能够接入模块以提供替代行为或响应事件。

这些根据插件应提供的功能类型分为以下类别。

- Web UI，用于修改 MeshCentral 管理界面
- 后端，用于修改服务器的核心功能，并与 Web UI 层以及 Mesh 代理（节点）层通信以发送命令和数据
- Mesh 代理（节点），用于为每个代理引入功能

### Web UI 钩子

- `onDeviceRefreshEnd`：在 MeshCentral Web 界面中选择设备时调用
- `registerPluginTab`：在 MeshCentral Web 界面中选择设备时调用，以注册一个新选项卡用于插件数据（如果需要）。接受一个对象或返回对象的函数，具有以下属性：{ tabId: "yourShortNameHere", tabTitle: "Your Display Name"}。将创建一个具有关联 ID 和标题的选项卡和 div 供您使用
- `onDesktopDisconnect`：在远程桌面会话断开连接时调用
- `onWebUIStartupEnd`：在页面首次加载后（登录/刷新后）调用
- `goPageStart`：在页面更改生效之前调用。传递 2 个参数（<page number> : int, <event> : Event）
- `goPageEnd`：在页面更改生效后调用。传递 2 个参数（<page number> : int, <event> : Event）

#### 导出

任何函数都可以通过将函数名称添加到插件对象中的 `exports` 数组来导出到 Web UI 层。

### 后端钩子

- `server_startup`：服务器启动时调用一次（或首次安装插件时）
- `hook_agentCoreIsStable`：代理首次签入时调用一次
- `hook_processAgentData`：每次代理将数据传输回服务器时调用
- `hook_userLoggedIn`：用户登录到 Web 界面时调用
- `hook_setupHttpHandlers`：在设置所有 HTTP 处理程序之前调用

### Mesh 代理

在可选文件夹 `modules_meshcore` 中使用可选文件 `plugin_name.js` 会将该文件包含在发送到每个端点的默认 meshcore 文件中。这对于在每个端点上添加功能非常有用。

## 结构

MeshCentral 的许多功能都围绕为您的结构返回对象，插件也不例外。在插件中，您可以一直遍历到 Web 服务器和 MeshCentral 服务器类，以访问这些层提供的所有功能。这是通过将当前对象传递给新创建的对象，并将该引用分配给该对象中的 `parent` 变量来完成的。


## Ping-Pong

如果您构建使用 `meshrelay.ashx` 的插件，请记住在控制通道上处理 ping-pong 消息（`serverPing`, `serverPong`），或请求 MeshCentral 通过在连接 URL 中发送 `noping=1` 参数来不发送此类消息。如需更深入的了解，请在 `meshrelay.js` 中搜索 "PING/PONG"。

## 版本控制

正确且一致地对插件进行版本控制对于确保插件用户在可用时被提示升级至关重要。建议使用语义化版本控制。

## 变更日志

强烈建议添加变更日志，以便您的用户知道自上次版本以来发生了什么变化。

## 示例插件

[MeshCentral-Sample](https://github.com/ryanblenis/MeshCentral-Sample) 是一个简单的插件，在从远程桌面断开连接时，提示用户输入手动事件（备注），并预填充日期和时间戳。
