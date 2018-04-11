# 安装redis

## 1. 下载
到[redis官网下载页](https://redis.io/download),复制下载地址
1. 打开终端进入Downloads目录下执行`wget http://download.redis.io/releases/redis-4.0.2.tar.gz`

2. 解压到当前目录 `tar -zxv -f redis-4.0.2.tar.gz`

3. 复制到`/opt/redis`目录
`sudo mkdir -p /opt/redis`
`sudo cp -R -n redis-4.0.2/* /opt/redis`

## 2. 编译
进入到`/opt/redis`执行`sudo make`
编译完后执行`sudo make test`


## 3 修改配置文件
进入redis目录
`sudo vim redis.conf`
找到requirepass，后面添加密码

## 4. 启动
`sudo ./src/redis-server redis.conf`



## 5. 常见问题

1. WARNING: The TCP backlog setting of 511 cannot be enforced because /proc/sys/net/core/somaxconn is set to the lower value of 128.

`echo 511 > /proc/sys/net/core/somaxcoon`
`vim /etc/sysctl.conf` 添加**net.core.somaxconn = 1024**后
执行`sysctl -p`

2. WARNING you have Transparent Huge Pages (THP) support enabled in your kernel.   
    This will create latency and memory usage issues with Redis.   
    To fix this issue run the command 'echo never > /sys/kernel/mm/transparent_hugepage/enabled' as root,   
    and add it to your /etc/rc.local in order to retain the setting after a reboot. Redis must be restarted after THP is disabled.

`vim /etc/rc.local` 添加
`echo never > /sys/kernel/mm/transparent_hugepage/enabled`
重启后执行`sudo ./src/redis-server redis.conf`





