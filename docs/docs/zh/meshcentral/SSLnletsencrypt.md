# SSL/Letsencrypt

## MeshCentral 支持使用自生成证书、您自己的证书或 Letsencrypt 的 SSL

### 启用 letsencrypt

确保在 config.json 文件中正确匹配和/或调整以下所有设置：

```json
{
    "settings": {
        "redirPort"
        "cert": "yourdomain.com"
    },
    "domains": {
        "letsencrypt": {
        "__comment__": "需要 NodeJS 8.x 或更高版本，在尝试 Let's Encrypt 之前先访问 https://letsdebug.net/。",
        "email": "myemail@myserver.com",
        "names": "myserver.com,customer1.myserver.com",
        "skipChallengeVerification": false,
        "production": true
        },
    }
}
```

如果您需要进一步了解这些设置的含义，请查看[配置模式](https://github.com/Ylianst/MeshCentral/blob/master/meshcentral-config-schema.json)。

然后重新启动 meshcentral，它将为您获取证书，该过程需要重新启动以应用证书。

### 有用的资源/故障排除

要检查 letsencrypt 是否正常工作，请使用 https://letsdebug.net/。我们使用这些说明中的 [HTTP-O1 挑战](https://letsencrypt.org/docs/challenge-types/#http-01-challenge) 方法。

还要确保您已打开端口 80 并指向您的 meshcentral 服务器，**如果端口 80 未打开，它将无法工作**，并且**必须**是端口 80。

您可以[在这里](https://ylianst.github.io/MeshCentral/meshcentral/#lets-encrypt-support)阅读更多关于 Letsencrypt 和 meshcentral 的信息。 
