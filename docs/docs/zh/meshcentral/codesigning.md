# 代码签名

## Authenticode-JS 视频

Nodejs 代码签名模块

<div class="video-wrapper">
  <iframe width="320" height="180" src="https://www.youtube.com/embed/xteKscs_Jgo" frameborder="0" allowfullscreen></iframe>
</div>

MeshCentral 自带 authenticode.js，您可以这样运行：

```bash
node node_modules/meshcentral/authenticode-js
```

and you will get

```
MeshCentral Authenticode Tool.
Usage:
  node authenticode.js [command] [options]
Commands:
  info: Show information about an executable.
        --exe [file]             Required executable to view information.
        --json                   Show information in JSON format.
  sign: Sign an executable.
        --exe [file]             Required executable to sign.
        --out [file]             Resulting signed executable.
        --pem [pemfile]          Certificate & private key to sign the executable with.
        --desc [description]     Description string to embbed into signature.
        --url [url]              URL to embbed into signature.
        --hash [method]          Default is SHA384, possible value: MD5, SHA224, SHA256, SHA384 or SHA512.
        --time [url]             The time signing server URL.
        --proxy [url]            The HTTP proxy to use to contact the time signing server, must start with http://
  unsign: Remove the signature from the executable.
        --exe [file]             Required executable to un-sign.
        --out [file]             Resulting executable with signature removed.
  createcert: Create a code signging self-signed certificate and key.
        --out [pemfile]          Required certificate file to create.
        --cn [value]             Required certificate common name.
        --country [value]        Certificate country name.
        --state [value]          Certificate state name.
        --locality [value]       Certificate locality name.
        --org [value]            Certificate organization name.
        --ou [value]             Certificate organization unit name.
        --serial [value]         Certificate serial number.
  timestamp: Add a signed timestamp to an already signed executable.
        --exe [file]             Required executable to sign.
        --out [file]             Resulting signed executable.
        --time [url]             The time signing server URL.
        --proxy [url]            The HTTP proxy to use to contact the time signing server, must start with http://
  icons: Show the icon resources in the executable.
        --exe [file]               Input executable.
  saveicons: Save an icon group to a .ico file.
        --exe [file]               Input executable.
        --out [file]               Resulting .ico file.
        --icongroup [groupNumber]  Icon groupnumber to save to file.
        --removeicongroup [number]
        --icon [groupNumber],[filename.ico]

Note that certificate PEM files must first have the signing certificate,
followed by all certificates that form the trust chain.

When doing sign/unsign, you can also change resource properties of the generated file.

          --filedescription [value]
          --fileversion [value]
          --internalname [value]
          --legalcopyright [value]
          --originalfilename [value]
          --productname [value]
          --productversion [value]
```

## 自动代理代码签名

如果您想对 mesh 代理进行自签名，以便在您的防病毒软件中将其列入白名单，并将其锁定到您的服务器和组织：

<div class="video-wrapper">
  <iframe width="320" height="180" src="https://www.youtube.com/embed/qMAestNgCwc" frameborder="0" allowfullscreen></iframe>
</div>

!!!note
    如果您在 Windows 上使用 `BEGIN PRIVATE KEY` 生成私钥，而 openssl 需要 `BEGIN RSA PRIVATE KEY`，您可以使用 `openssl rsa -in server.key -out server_new.key` 将您的私钥转换为 rsa 私钥

## 设置代理文件信息

现在 MeshCentral 自定义并签名代理，您可以将该值设置为您喜欢的任何内容。

```json
"domains": {
      "agentFileInfo": {
            "filedescription": "sample_filedescription",
            "fileversion": "0.1.2.3",
            "internalname": "sample_internalname",
            "legalcopyright": "sample_legalcopyright",
            "originalfilename": "sample_originalfilename",
            "productname": "sample_productname",
            "productversion": "v0.1.2.3"
      }
}
```

## 外部签名作业

externalsignjob 功能允许您在 MeshCentral 完成其代码签名过程后对代理执行额外的操作。这对于以下情况特别有用：

1. 使用硬件安全令牌进行签名
2. 在单独的服务器或云主机上执行签名
3. 归档签名代理
4. 添加额外的安全措施

externalsignjob 在 MeshCentral 完成其整个代码签名过程后调用，包括：
- 资源修改
- 数字签名应用
- 时间戳应用（如果已配置）

要使用此功能，请将以下内容添加到您的 config.json：

```json
"settings": {
    "externalsignjob": "path/to/your/script.bat"
}
```

脚本将接收代理的路径作为其第一个参数。以下是示例脚本：

### 批处理文件示例
```batch
@echo off
Echo External Signing Job
signtool sign /tr http://timestamp.sectigo.com /td SHA256 /fd SHA256 /a /v /f path/to/your/signing.cer /csp "eToken Base Cryptographic Provider" /k "[{{MyPassword}}]=PrivateKeyContainerName" "%~1"
```

### PowerShell 示例
```powershell
$file = $args[0]
signtool sign /tr http://timestamp.sectigo.com /td SHA256 /fd SHA256 /a /v /f path/to/your/signing.cer /csp "eToken Base Cryptographic Provider" /k "[{{MyPassword}}]=PrivateKeyContainerName" $file
```

externalsignjob 不仅可以用于签名。例如，您可以：

1. 将签名代理归档到安全位置
2. 将签名代理上传到分发服务器
3. 执行额外的安全检查
4. 添加自定义元数据或水印
5. 与您组织的构建管道集成

注意：脚本必须返回成功退出代码 (0) 才能被视为成功。任何非零退出代码都将被视为失败并被记录。
