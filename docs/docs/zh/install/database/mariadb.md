# 本节将介绍如何将 MySQL/MariaDB 配置为数据库后端。

根据[模式](https://github.com/Ylianst/MeshCentral/blob/master/meshcentral-config-schema.json)，我们对 `config.json` 进行如下更改。<br>
为了更专注于数据库配置，一些必需的键已被省略。但请不要删除这些键。

---

### MeshCentral 速查表：

数据库特定配置：

MariaDB：
```json
{
  "$schema": "https://raw.githubusercontent.com/Ylianst/MeshCentral/master/meshcentral-config-schema.json",
  "__comment__": "为了专注于数据库配置，省略了这些键",
  "settings": {
    "mariaDB": {
        "host": "my-mariadb-hostname",
        "port": "3306",
        "user": "my-mariadb-user",
        "password": "my-mariadb-password",
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

MySQL：
```json
{
  "$schema": "https://raw.githubusercontent.com/Ylianst/MeshCentral/master/meshcentral-config-schema.json",
  "__comment__": "为了专注于数据库配置，省略了这些键",
  "settings": {
    "mySQL": {
        "host": "my-mysql-hostname",
        "port": "3306",
        "user": "my-mysql-user",
        "password": "my-mysql-password",
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

### MariaDB/MySQL 速查表：

```bash
mariadb -u root -p
```
或者
```bash
mysql -u root -p
```

```sql
-- 创建数据库
CREATE DATABASE meshcentral;

-- 创建用户（限制只能从本地登录）
CREATE USER 'meshcentral'@'localhost' IDENTIFIED BY 'my-very-secure-password';

-- 授予权限
GRANT ALL PRIVILEGES ON meshcentral.* TO 'meshcentral'@'localhost';

-- 应用更改
FLUSH PRIVILEGES;
```