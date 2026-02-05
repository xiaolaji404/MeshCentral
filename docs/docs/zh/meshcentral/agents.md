# Mesh 代理

## Windows

默认安装路径：`c:\Program Files\Mesh Agent`

应用程序路径：`c:\Program Files\Mesh Agent\meshagent.exe`

应用程序数据库路径：`c:\Program Files\Mesh Agent\meshagent.db`

应用程序日志路径：`c:\Program Files\Mesh Agent\meshagent.log`

xxx 路径：`c:\Program Files\Mesh Agent\meshagent.msh`

=== ":material-console-line: 状态"

    - 启动：`net start "mesh agent"`
    - 停止：`net stop "mesh agent"`
    - 重启：`net restart "mesh agent"`
    - 状态：需要信息

=== ":material-console-line: 故障排除"

    故障排除步骤：需要信息

## Linux / BSD

卸载：`sudo /usr/local/mesh_services/meshagent/[agent-name]/meshagent -fulluninstall`

## Apple macOS 二进制安装程序

默认安装路径：`/usr/local/mesh_services/meshagent/meshagent`

从 `/Library/LaunchAgents/meshagent.plist` 启动

控制代理

```bash
launchctl stop meshagent
launchctl start meshagent
```

安装：

卸载：`sudo /usr/local/mesh_services/meshagent/[agent-name]/meshagent -fulluninstall`

## Apple macOS 通用版

适用于 OSx 11+，包括 Big Sur、Monterey 及更高版本

## Apple macOS

适用于 macOS 10.x，包括 Catalina、Mojave、High Sierra、Sierra、El Capitan、Yosemite、Mavericks、Mountain Lion 及更早版本。

## 移动设备（Android）

## MeshCentral 助手

参见[助手](assistant.md)

## Apple MacOS 二进制安装程序

## 代理命令

**agentmsg**
：向设备的 Web UI 添加/删除带徽章的消息
```
  agentmsg add "[message]" [iconIndex]
  agentmsg remove [index]
  agentmsg list
```
**agentsize**
：返回代理的二进制大小

**agentupdate**
：手动触发代理自更新

**alert**
：在登录会话上显示警报对话框
```
alert TITLE, CAPTION [, TIMEOUT]
```

**amt**

**amtconfig**

**amtevents**

**apf**

**args**

**av**
：显示防病毒状态

**coredump**

**coreinfo**

**cpuinfo**

**cs**
：显示 Windows 连接待机状态

**dbcompact**
：压缩代理数据库

**dbget**

**dbkeys**

**dbset**

**dnsinfo**
：显示 DNS 服务器信息

**domain**
：显示域元数据

**errorlog**

**eval**
：在代理上执行 JavaScript
```
eval [code]
```

**fdcount**
：返回事件循环中活动描述符的数量

**fdsnapshot**
：返回详细的描述符/句柄/定时器元数据

**getclip**
：从代理获取剪贴板数据

**getscript**

**help**
：返回支持的控制台命令列表

**httpget**

**info**
：返回有关代理的一般信息，例如连接状态、加载的模块、LMS 状态等

**kill**
: Sends a SIGKILL signal to the specified PID
```
kill [pid]
```

**kvmmode**
: Displays the KVM Message Format

**location**
: Displays saves location information about the connected agent

**lock**

**log**
: Writes a message to the logfile
```
log [message]
```

**ls**
：枚举代理安装文件夹中的文件

**mousetrails**
：在 Windows 上启用/禁用鼠标轨迹辅助功能。要更改设置，请指定一个正整数，表示潜在光标的数量，其中 0 为禁用
```
mousetrails [n]
```

**msh**
：显示加载的 msh 设置文件

**netinfo**
：显示网络接口信息

**notify**
：在 Web 界面上显示通知

**openurl**

**osinfo**
：显示操作系统信息

**parseuri**
：解析指定的 URI，并显示解析后的输出
``` 
parseuri [uri]
```

**plugin**
: Invokes a plugin
```
plugin [pluginName] [args]
```

**power**
: Performs the specified power action
```
power [action]
  LOGOFF = 1
  SHUTDOWN = 2
  REBOOT = 3
  SLEEP = 4
  HIBERNATE = 5
  DISPLAYON = 6
  KEEPAWAKE = 7
  BEEP = 8
  CTRLALTDEL = 9
  VIBRATE = 13
  FLASH = 14
```

**print**

**privacybar**
: Sets/Gets the default pinned state of the Privacy Bar on windows
```
privacybar [PINNED|UNPINNED]
```

**ps**
: Enumerates processes on the agent

**rawsmbios**
: Fetches the raw smbios table

**safemode**
: Sets/Gets the SAFEMODE configuration of the agent, as well as the next boot state.
```
safemode (ON|OFF|STATUS)
```

**scanwifi**
: Scans the available Wifi access points, and displays the SSID and Signal Strength

**service**
: Shortcut to be able to restart the agent service
```
service status|restart
```

**setclip**
: Sets clipboard data to the agent
```
setclip [text]
```

**setdebug**
: Sets the location target for debug messages
```
setdebug [target]
0 = Disabled
1 = StdOut
2 = This Console
* = All Consoles
4 = WebLog
8 = Logfile
```

**smbios**
：显示解析后的 SMBIOS 元数据

**startupoptions**
：显示代理启动时使用的命令行选项

**sysinfo**
：收集并显示平台的遥测数据

**task**

**taskbar**
：隐藏或显示 Windows 系统任务栏，可选在指定的终端服务器会话 ID 上
```
taskbar HIDE|SHOW [TSID]
```

**timerinfo**
: Displays metadata about any configured timers on the event loop

**toast**
: Displays a toast message on the logged in user's session
```
toast [message]
```

**translations**
: Shows the currently configured translations

**type**
```
type (filepath) [maxlength]
```

**uac**
: Get/Sets the Windows UAC mode
```
uac [get|interactive|secure]
```

**unzip**
```
unzip input, destination
```
: Unzips the specified file

**users**
: Enumerates the logged in users on the system

**versions**
: Displays version information about the agent

**vm**
: Detects if the system is a Virtual Machine

**volumes**
: Displays volume information reported by the OS

**wakeonlan**
: Sends wake-on-lan packets to the specified MAC address
```
wakeonlan [mac]
```

**wallpaper**
: Gets/Toggles the logged in user's desktop background image
```
wallpaper (GET|TOGGLE)
```

**wpfhwacceleration**
: Enable/Disable WPF HW Acceleration on Windows
```
wpfhwacceleration (ON|OFF|STATUS)
```

**wsclose**

**wsconnect**

**wslist**

**wssend**

**zip**
```
zip (output file name), input1 [, input n]
```

## Agent msh options

You can find a full list of options for the agent [here](https://github.com/Ylianst/MeshAgent?tab=readme-ov-file#msh-format)

`skipmaccheck=1`: Will not regenerate the agents nodeid and cause duplication of the agent when the MAC address changes.

You can add options to your .msh on agent install with [this](https://github.com/Ylianst/MeshCentral/blob/15ff7d12a1e4e5d78936b473ea207b7e02b8ff26/meshcentral-config-schema.json#L2504)
