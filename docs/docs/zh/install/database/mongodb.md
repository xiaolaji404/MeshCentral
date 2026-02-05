# 本节将介绍如何将 MongoDB 配置为数据库后端。

根据[模式](https://github.com/Ylianst/MeshCentral/blob/master/meshcentral-config-schema.json)，我们对 `config.json` 进行如下更改。<br>
为了更专注于数据库配置，一些必需的键已被省略。但请不要删除这些键。

---

### MeshCentral 速查表：

MongoDB 使用 MongoDB 连接字符串进行配置。

```json
{
  "$schema": "https://raw.githubusercontent.com/Ylianst/MeshCentral/master/meshcentral-config-schema.json",
  "__comment__": "为了专注于数据库配置，省略了这些键",
  "settings": {
    "mongoDb": "mongodb://localhost:27017/meshcentral"
  },
  "domains": {
    "": {
      "__comment__": "为了专注于数据库配置，省略了这些键",
    }
  },
  "_letsencrypt": {
    "__comment__": "为了专注于数据库配置，省略了这些键",
  }
}
```