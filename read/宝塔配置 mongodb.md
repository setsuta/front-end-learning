> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [juejin.cn](https://juejin.cn/post/7064135651431546916)

#### 1. 在宝塔的软件商店中安装 mongodb

![](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5df044b4c0384d90888baad4e9704427~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp?)

##### 2. 修改 mongodb 配置连接外网

`bindIp` 由 127.0.0.1 改为 0.0.0.0，放开 ip 限制  
`authorization` 默认 disabled，如需要权限验证改为 enabled（注意保留空格） ![](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/22fe69d3e8c040cc9a22fc593d8db2ab~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp?) ![](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c5a866b6d54e4485b96763faf5f3b938~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp?)

##### 3. 宝塔放开 27017 端口

![](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fcf1aea0e9ad447b81925b4955d99cb5~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp?)

##### 4. 阿里云服务器，网络与安全 - 安全组 - 配置规则，放开 27017 端口出入

![](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6349cad0e8e34df49c73288e4cdb20eb~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp?)

##### 5. 配置用户名密码

1.  通过宝塔终端链接 mongodb

```
cd /www/server/mongodb/bin
mongo
复制代码

```

2.  切换到 admin 数据库，设置管理员账号密码

```
use admin 
db.createUser({user:'root',pwd:'123456',roles:['root']})
复制代码

```

验证是否添加成功，db.auth(用户名，用户密码)

```
db.auth('root', '123456')
复制代码

```

3.  为某个数据库，创建角色

```
use mydata 
db.createUser({user:'username',pwd:'123456',roles:['readWrite']})
复制代码

```

验证

```
db.auth('username', '123456')
复制代码

```

##### 6. 修改后台项目连接数据库配置

![](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/49d5113e263a4705acee83013f381052~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp?)

##### 7. 上传后端项目

进入`www/wwwroot` 目录下，上传到你自己喜欢的位置 ![](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f7c1ea066b7b484d8cddaa057d2ea51e~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp?)

##### 8. 安装 PM2 管理器，启动项目

![](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6f22044a80d64d17951b61a9e7b25a27~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp?) 添加项目，在启动文件里选择你后台项目的启动文件路径。其它项会自动填写 ![](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2ae33e6920cb4e5e9ef67b87e2d62319~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp?)

##### 9. 验证接口

去 postman 验证一下，接口是否能请求成功。  
如果请求失败，试着重启 pm2，查看项目运行日志是否有报错。

> 如果遇到 mongoDB 启动失败

```
//方案一：
mongod -f /www/server/mongodb/config.conf\
或者修改MongoDB的启动文件\
/etc/init.d/mongodb
复制代码

```

![](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ec555cc92b9546fdb3b70146358fedc3~tplv-k3u1fbpfcp-zoom-in-crop-mark:3024:0:0:0.awebp?)

```
//方案二：
改了配置文件，用更高的权限运行这条命令启动服务：
sudo mongod -f /www/server/mongodb/config.conf      
把-f后面的路径改成你配置文件的路径即可
复制代码

```

```
//方案三：
cd /www/server/mongodb/bin
输入命令：`mongod`
复制代码

```