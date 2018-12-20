# MongoDB

## 用户权限控制

### MongoDB 3.6

#### 创建root用户

```mong
use admin
db.createUser({
    user: "root",
    pwd: "123456",
    roles: [{
        role: "root",
        db: "admin"
    }]
})
```

#### 创建admin用户

```
use admin
db.createUser({
    user: "admin",
    pwd: "123456",
    roles: [{
        role: "userAdminAnyDatabase",
        db: "admin"
    }]
})
```

#### 创建普通用户

创建的用户可以在admin数据库中看到相关信息

```
use my_database
db.createUser({
    user: "my_username",
    pwd: "my_password",
    roles: [{
        role: "readWrite",  # 读写权限
        db: "my_database"
    }]
})
```

#### 查看用户

不需要进入用户具体所在的服务器，只需要在admin数据库中查看即可

`db.system.users.find()`

#### 删除用户

删除单个用户：`db.system.users.remove({user:"XXXXXX"})`

删除多个用户：`db.system.users.remove({})`