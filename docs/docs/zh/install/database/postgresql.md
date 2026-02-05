# 本节将介绍如何将 PostgreSQL 配置为数据库后端。

根据[模式](https://github.com/Ylianst/MeshCentral/blob/master/meshcentral-config-schema.json)，我们对 `config.json` 进行如下更改。<br>
为了更专注于数据库配置，一些必需的键已被省略。但请不要删除这些键。

---

### MeshCentral 速查表：

如果您熟悉 MeshCentral 方面的 postgres 安装，`settings` 中的 postgres 配置相当简单。

```json
{
  "$schema": "https://raw.githubusercontent.com/Ylianst/MeshCentral/master/meshcentral-config-schema.json",
  "__comment__": "为了专注于数据库配置，省略了这些键",
  "settings": {
    "postgres": {
        "host": "my-postgresql-hostname",
        "port": "5432",
        "user": "my-postgresql-user",
        "password": "my-postgresql-password",
        "database": "meshcentral-database"
    }
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

> 如有需要，可以使用更多选项。请参阅上面的模式。

### Postgres 速查表

```bash
# 登录到服务器
psql -U postgres
```

```sql

-- 创建数据库用户
postgres=# CREATE USER meshcentral WITH PASSWORD 'your-very-strong-password';
CREATE ROLE

-- 创建数据库并将上述用户设置为所有者
postgres=# CREATE DATABASE meshcentral OWNER meshcentral;
CREATE DATABASE

-- 退出数据库
postgres=# exit
```