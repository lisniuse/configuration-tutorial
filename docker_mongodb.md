# docker 配置 mongodb

## 第一步：拉去官方镜像

``` bash
$ docker pull mongo
```

## 第二步：创建容器

请事先创建好 ``d:/data/mongodb/configdb/`` 和 ``d:/data/mongodb/db/`` 目录。**非windows系统同理**。

``` bash
$ docker run --name mongodb -p 27017:27017 -v d:/data/mongodb/configdb/:/data/configdb/ -v d:/data/mongodb/db/:/data/db/ -d mongo --auth
```

## 第三步：进入容器创建账号密码

``` bash
> db.createUser({ user: 'root', pwd: 'root', roles: [ { role: "userAdminAnyDatabase", db: "admin" } ] });
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

## 第六步：填写数据库uri

如下所示：

``mongodb://root:root@127.0.0.1``
