# Redis安装

1. ### **下载源码包并放入 /opt 目录**

```
sudo wget -P /opt http://download.redis.io/releases/redis-7.0.0.tar.gz
```

2.  **在 /opt 目录下解压 Redis**

```
sudo tar -zxvf /opt/redis-7.0.0.tar.gz -C /opt
```

3. ###  **进入解压后的目录**

```
cd /opt/redis-7.0.0
```

4. ### **在 redis-7.0.0 目录下执行 make 命令（开始编译）**

   - 先装make

   ```
   sudo apt install make -y
   ```

   - 执行编译安装

   ```
   sudo make && sudo make install
   ```

   

Redis默认安装路径`usr/local/bin`

- redis-benchmark:性能测试工具，服务启动后运行该命令，看看自己本子性能如何
- redis-check-aof：修复有问题的AOF文件，rdb和aof后面讲
- redis-check-dump：修复有问题的dump.rdb文件
- **redis-cli：客户端，操作入口**
- redis-sentinel：redis集群使用
- **redis-server：Redis服务器启动命令**

拷贝Redis配置文件

在根路径下创建一个myredis文件 

```
sudo mkdir /myredis
```

找到redis配置文件

```
cd /opt/redis-7.0.0
```

**将配置文件拷贝到我们刚才建好的 /myredis 目录**

```
sudo cp redis.conf /myreids/
```

---

### 修改/myredis目录下rediş.conf配置文件做初始化设置

redis.conf配置文件，改完后确保生效，记得重启，记得重启

1. 默认daemonize no      改为 daemonize yes

2.  默认protected-mode yes改为 protected-mode no

3. 默认bind 127.0.0.1      改为 直接注释掉(默认bind127.0.0.1只能本机访问)或改成本机IP地址，否则影响远程IP连接

4. 添加redis密码             改为 requirepass 你自己设置的密码

   ![PixPin_2026-10-07_15-32-33](C:\Users\22591\Desktop\编程\Redis\img\PixPin_2026-10-07_15-32-33.png)

# mirco编辑器

### 装 micro，更像 Windows 习惯进行修改

```
sudo apt install micro
```

打开文件

```
sudo micro /myredis/redis.conf
```

- 退出`ctr + q`

### 启动redis

```
./src/redis-server /myredis/redis.conf
```

**在后台进程中查找 Redis 服务，并过滤掉查找命令本身**

```
ps -ef|grep redis|grep -v grep
```

### 连接redis服务器

```
redis-cli -a 12345678 -p 6379
```

### 关闭

在Redis中执行`shutdown`

![PixPin_2026-10-07_16-35-02](C:\Users\22591\Desktop\编程\Redis\img\PixPin_2026-10-07_16-35-02.png)

在Redis外面关闭

- 单实例关闭：`redis-cli -a 111111 shutdown`

- 多实例关闭，指定端口关闭:`redis-cli -p 6379 shutdown`

![PixPin_2026-10-07_16-38-44](C:\Users\22591\Desktop\编程\Redis\img\PixPin_2026-10-07_16-38-44.png)

## 卸载

- 停止redis-server服务
- 删除/usr/local/lib目录下与redis相关的文件

```
#查看
ls -l /usr/local/bin/redis-*
#卸载
rm -rf/usr/local/bin/redis-*
```

# vim编辑器

## 退出编辑器

- 按下`Ese`键
- 放弃修改不保存`:q`然后按回车键（强制退出`:q!`回车）
- 保存修改退出：输入`:wq`然后按回车键（`w`代表写入/保存，`q`代表退出）

## 查找关键字

- 先按`Ese`，确保处于命令模式
- 按下`/`键
- 输出查找的关键字
- 按回车

​	**查找下一个关键字**： 回车后按`N`键：跳转到下一个匹配结果；按 `N`键(Shift + n) ：跳转到上一个匹配结果。

# set

#### mset、mget 设置/取多个值

![PixPin_2026-10-09_13-40-41.png](<https://img.remit.ee/i/uwZmNBYnfh4P>)

#### MSETNX——批量设置键值对

只有当所有的键都不存在时才会设置成功，只要有一个键存在，Redis就会拒绝执行所有操作

![8FIFO1qWCfgw.png](https://img.remit.ee/i/8FIFO1qWCfgw)

#### GETRANGE ——截取字符串指定范围的内容

#### **SETRANGE 是用来“覆盖替换”字符串中指定位置的内容的**

![](https://img.remit.ee/i/g58klVpKVLig)

# 分布式锁





---

# List

![PixPin_2026-10-09_14-30-28.png](<https://img.remit.ee/i/7g66QtnfduhH>)
