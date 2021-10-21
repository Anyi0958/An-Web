
## 常用操作
- 清屏  `clear`

- 控制台输出 `echo "test info"`

- 输入内容到指定文件 `echo "test info" > test.txt`


## 文件夹操作

  - 查看当前目录下的文件夹详细信息 `ll`

  - 查看当前目录下的文件夹 `ls`

  - 查看当前目录下子目录的文件夹 `find 目录名 -type f`

  - 创建文件夹 `mkdir 文件夹名`
  

## 文件操作

  - 创建文件 `touch 文件名`

  - 删除文件 `rm 文件名`

  - 文件重命名 `mv 当前文件名 新文件名`

  - 查看文件 `cat 文件`

  - 查看并编辑文件 `vim 文件`

    - 按 `esc` 和 `:` 进行命令执行
      - `i` 进入 插入模式 进行文件的编辑
      - `q!` 强制退出(不保存)
      - `wq` 保存退出
      - `set nu` 设置行号



## find 命令搜索文件

```shell
find [options] [path...] [expression]
```

- 该`options`属性控制符号链接，调试选项和优化方法的处理。
- 该`path...`属性定义了find将搜索文件的起始目录。
- 该`expression`属性由选项，搜索模式和由运算符分隔的操作组成。

我们来看看下面的例子：

```shell
find  -L /home/projects/ -name "*.js" -exec chmod 644 {} \;
```

此命令包含一个参数`-L`（options），它允许find命令跟随符号链接，搜索`/home/projects/`（path ...）下面的整个目录树，查找以`.js`（expression）结尾的所有文件，并将所有匹配文件的权限设置为644



## **du 获取目录的大小**

```shell
sudo du -shc /var/*
```



- 该命令首先是`sudo`因为目录中的大多数文件和目录`/var`都由root用户拥有，并且常规用户无法读取。如果省略[`sudo`](https://linuxize.com/post/sudo-command-in-linux/)该`du`命令将打印“du：无法读取目录”。
- `s` - 仅显示指定目录的总大小，不显示子目录的文件大小总计。
- `h`- 以人类可读的格式打印（`h`）。
- `/var` - 要获取大小的目录的路径



## free 查看内存状态

```shell
free -h
```

```shell
              total        used        free      shared  buff/cache   available
Mem:           3936        1087         252         130        2596        2427
Swap:             0           0           0

以下是各栏的意思：

total-序可以使用的内存总量。
used-已使用的内存。 计算公式为：used = total - free - buffers - cache
free -可用/未使用的内存。
shared -可以忽略此列；
buff/cache -内核缓冲区以及页面缓存和slab使用的组合内存。 如果应用程序需要，可以随时回收此内存。
available-可用于启动新应用程序而无需交换内存估计数。
free命令显示物理内存和系统交换的信息。
```

### 清理缓存的脚本

```shell
vim /home/script/clear_buff_cache.sh
```

```shell
#!/bin/bash
 
#开始清理缓存
echo "开始清除缓存"
 
#写入硬盘，防止数据丢失
sync;sync;sync
 
#延迟10秒
sleep 10
 
#清理缓存
echo 3 > /proc/sys/vm/drop_caches
```

### 设置定时任务（每天凌晨2:30清理一次)

```shell
crontab -e
```

```shell
# clear buff/cache
30 2 * * * /home/script/clear_buff_cache.sh
```

## 命令重启Linux

- ### **用systemctl命令**

  `sudo systemctl reboot`

  要阻止重新启动命令，请使用`--no-wall`选项运行命令发送消息：

  ```shell
  sudo systemctl --no-wall reboot
  ```

- ### **使用shutdown命令**

  ```shell
  sudo shutdown -r
  ```

  默认情况下，系统将在1分钟后重新启动，但是您可以指定希望系统重新启动的确切时间.

  时间参数可以具有两种不同的格式。它可以是格式中的绝对时间，也可以是格式中的`hh:mm`相对时间，`+m`其中m是从现在开始的分钟数。

  

  以下示例将计划在上午10点重新启动系统:

  ```shell
  sudo shutdown -r 10:00
  ```

  要立即关闭系统，请使用`+0`或其别名`now`：

  ```shell
  sudo shutdown -r now
  ```

  取消重新启动

  ```shell
  sudo shutdown -c
  ```

  

## Linux中检查端口占用情况

    显示tcp，udp的端口和进程等相关情况
    
    ```shell
    netstat -tunlp
    ```
    
    查看指定端口号的进程情况
    
    ```shell
    netstat -tunlp|grep 端口号
    ```



## 防火墙

#### 		开启端口3306

```shell
firewall-cmd --zone=public --add-port=3306/tcp --permanent
```

#### 		重启防火墙

```shell
firewall-cmd --reload
```

#### 		查看已经开放的端口

```shell
firewall-cmd --list-ports
```



## 查找运行程序主目录

#### 		查看程序所在PID

```shell
netstat -lntup
```

#### 		根据PID查找程序所在目录

```shell
ll /proc/PID/exe
```

#### 		查找程序配置路径

```shell
/proc/PID/exe -t
```


