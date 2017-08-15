# **Linux下安装Mongodb说明**

## 安装前准备：
* mongodb安装包

>下载网址，记得下载你需要的版本
[https://www.mongodb.com/download-center?jmp=nav#community](https://www.mongodb.com/download-center?jmp=nav#community)

## 安装步骤
> 安装路径默认为`/usr/local/mongodb`
> 安装版本默认为'mongodb-linux-x86_64-ubuntu1604-3.4.7.tgz'

 1. 首先进入你想要安装mongodb的目录下，并创建名为mongodb的文件夹
 
 ```
 cd /usr/local
 mkdir mongodb
 ```
 2. 解压缩安装包文件，并把该文件夹下的所有文件都移动到`mongodb/`路径下，记得替换成自己下载的版本号

 ```
 tar -zxvf mongodb-linux-x86_64-ubuntu1604-3.4.7.tgz
 cd mongodb-linux-x86_64-ubuntu1604-3.4.7.tgz
 mv * /usr/local/mongodb  
 ```
 3. 创建用于存放数据的'data'文件夹
 
 ```
 cd /usr/local/mongodb
 mkdir data
 ```

## 如果使用mongodb
> 当前路径 `/usr/local/mongodb`

 1. 启动mongodb服务
 ```
cd bin
mongod -dbpath=/usr/local/mongodb/data
```
Server端启动成功：
> 2017-08-15T11:02:32.896+0800 I NETWORK  [thread1] waiting for connections on port 27017

 2. **重新开一个Terminal**，在`bin/`路径下连接mongodb数据库，
 ```
 mongo
 ```
 
 
 Server端接受到请求并成功建立连接
 > 2017-08-15T11:08:25.929+0800 I NETWORK  [thread1] connection accepted from 127.0.0.1:59456 #1 (1 connection now open)
2017-08-15T11:08:25.931+0800 I NETWORK  [conn1] received client metadata from 127.0.0.1:59456 conn1: { application: { name: "MongoDB Shell" }, driver: { name: "MongoDB Internal Client", version: "3.4.6" }, os: { type: "Windows", name: "Microsoft Windows 8", architecture: "x86_64", version: "6.2 (build 9200)" } }

 数据库连接成功，进入mongo shell
![](https://github.com/AgentCyrusJr/markdown/raw/master/20170815111428.png)

## Tutorial
[官方文档](https://docs.mongodb.com/tutorials/)
