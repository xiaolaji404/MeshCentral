# 本节将介绍如何配置本地数据库作为后端。

按照[模式](https://github.com/Ylianst/MeshCentral/blob/master/meshcentral-config-schema.json)，我们对 `config.json` 进行以下更改。<br>
为了进一步专注于数据库配置，一些必需的键已被省略。也不要删除这些键。

默认情况下，MeshCentral 使用 NeDB，因此要将其更改为另一种数据库类型，请执行以下操作：

---

### MeshCentral 速查表：

Sqlite3：
```json
{
  "$schema": "https://raw.githubusercontent.com/Ylianst/MeshCentral/master/meshcentral-config-schema.json",
  "__comment__": "为了专注于数据库，省略了这些键",
  "settings": {
    "sqlite3": {
        "name": "meshcentral-db"
    }
  },
  "domains": {
    "": {
      "__comment__": "为了专注于数据库，省略了这些键",
    }
  },
  "_letsencrypt": {
    "__comment__": "为了专注于数据库，省略了这些键",
  }
}
```

Acebase：
```json
{
  "$schema": "https://raw.githubusercontent.com/Ylianst/MeshCentral/master/meshcentral-config-schema.json",
  "__comment__": "为了专注于数据库，省略了这些键",
  "settings": {
    "acebase": {
        "sponsor": false
    }
  },
  "domains": {
    "": {
      "__comment__": "为了专注于数据库，省略了这些键",
    }
  },
  "_letsencrypt": {
    "__comment__": "为了专注于数据库，省略了这些键",
  }
}
```