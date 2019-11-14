# docker 配置 mongodb

## 第一步：拉取官方镜像

``` bash
$ docker pull mongo
```

## 第二步：创建容器

**无需映射目录**

``` bash
$ docker run -itd --name mongo -p 27017:27017 mongo --auth
```

## 第三步：进入容器创建账号密码

``` bash
$ docker exec -it mongo mongo admin
```

创建root用户

``` bash
> db.createUser({ user: 'root', pwd: 'root', roles: [{role: 'root', db: 'admin'}] })
```

创建普通用户，并指定数据库。

``` bash
> db.createUser({ user: "dbuser", pwd: "dbpass", roles: [{ role: "dbOwner", db: "yourdb" }]})
```

给普通用户授权

``` bash
> db.grantRolesToUser("dbuser", [{role: "dbOwner", db: "yourdb"}])
```

## 第四步：安装adminMongo

``` bash
$ git clone git@github.com:mrvautin/adminMongo.git
```

## 第五步：启动adminMongo

``` bash
$ cd adminMongo
$ npm install / yarn
$ npm start
```

## 第六步：填写连接uri

root 用户：

``mongodb://root:root@localhost:27017``

普通用户：

``mongodb://dbuser:dbpass@localhost:27017/yourdb?authSource=admin``
