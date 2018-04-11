# 安装与配置mongodb

## 1. 安装 mongodb

1. 到mongodb官网下载中心: **https://www.mongodb.com/download-center#community**
找到自己对应的版本，比如linux下的: **Ubuntu 16.04 Linux 64-bit x64**
获取对应的下载地址:
**https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-ubuntu1604-3.4.10.tgz**

2. 打开终端，进入Downloads目录下执行
`wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-ubuntu1604-3.4.10.tgz`

3. 解压到Downloads/mongodb目录下
`tar -zxv -f mongodb-linux-x86_64-ubuntu1604-3.4.10.tgz`

4. 在`/opt`目录下创建mongodb文件夹
`sudo mkdir -p /opt/mongodb`
复制解压后的文件到此目录下
`sudo cp -R -n mongodb-linux-x86_64-ubuntu1604-3.4.10/* /opt/mongodb`

5. 创建数据库存放目录
`sudo mkdir -p /data/db`
并修改权限，使当前用户能够进入此目录读写文件

6. 加入环境变量
1) 仅当前终端环境可用
`export PATH=$PATH:/opt/mongodb/bin`


2) 当前用户可用，在.bashrc最后一行添加如下代码
`export PATH=$PATH:/opt/mongodb/bin`
保存后执行`source .bashrc`.不需要重新登录即可生效
打开一个新终端可以直接执行`mongod` `mongo`等命令

3) 所有用户可用
将2）中添加的代码添加到文件/etc/profile中

## 2. 以配置文件启动mongodb

在`/etc`下创建mongodb配置文件,并写入如下内容
`sudo vim mongod.conf`

```sh
port=27029                      # 默认27017
bind_ip=127.0.0.1               # 只能通过此ip访问
dbpath=/data/db                 # 默认路径即是此路径
logpath=/data/mongod.log        # 日志写入文件
pidfilepath=/data/mongod.pid    # pid
auth=true                       # 启用认证登录
logappend=true                  # 写日志模式
fork=true                       # 后台运行
nohttpinterface=false           # 禁止http接口，默认false

```

## 3. mongodb添加用户

进入mongo环境
`mongo 127.0.0.1:27029`

切换到admin数据库
`use admin`

创建管理员账号
`db.createUser({user: "weels", pwd: "123456", roles: ["root"]})`

创建普通用户
`db.createUser({user: "yoo", pwd: "123456", roles: [{role: "readWrite", db: "yoosen"}]})`


## 4. 启动与管理mongodb服务

1. 启动
`mongod -f /etc/mongod.conf`
如果配置文件内设置`fork=true`,则会在后台运行，此时就不能通过ctrl+c停止

2. 停止
```sh
use admin
db.auth("weels", "123456")      # 如果已经添加用户权限，需要先验证
db.shutdownServer()             # 执行后退出即可
```

通过进程id关闭
查看进程id
`cat /data/mongod.pid`
或
`ps -ef | grep mongod`

`kill -2 13456`
每次启动后pid都相同