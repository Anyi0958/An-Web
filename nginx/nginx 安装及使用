
## windows 使用 nginx

> [官方下载地址](https://nginx.org/en/download.html)
> 
> windows 官方下载安装包 双击自行安装


## linux 使用 nginx

### 安装依赖包
```
  yum -y install gcc-c++ libtool zlib zlib-devel pcre-devel openssl openssl-devel 
```
### 下载并解压安装包

```
切换到 /usr/local 文件夹
  cd /usr/local
  
创建 nginx 文件夹
  mkdir nginx
  
切换到 nginx 文件夹
  cd nginx
    
下载 nginx tar包
  wget http://nginx.org/download/nginx-1.18.0.tar.gz
  
解压
  tar -xvf nginx-1.18.0.tar.gz
```

### 安装 nginx

```
进入nginx目录
  cd /usr/local/nginx

进入目录
  cd nginx-1.18.0

执行命令
  ./configure

编译
  make

编译安装
  make install
  
```
### 启动 nginx
```
启动
  /usr/local/nginx/sbin/nginx -s reload

如果出现报错：
  nginx: [error] open() ＂/usr/local/nginx/logs/nginx.pid＂ failed

则运行：
  /usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf

再次启动
  /usr/local/nginx/sbin/nginx -s reload

查看nginx进程是否启动
  ps -ef | grep nginx

进入安装目录命令： 
  cd /usr/local/nginx/sbin

常用命令 启动，关闭，重启命令：
  ./nginx 
  ./nginx -s stop 
  ./nginx -s reload 

```

### 查看 nginx 状态

-  查看 nginx 进程
    >   ps -ef | grep nginx
  
- 访问 nginx 服务
  >  curl 127.0.0.1:80


### 关闭防火墙
  
- centOS6 及以前版本使用命令： 
  >  systemctl stop iptables.service

- centOS7 关闭防火墙命令： 
  >  systemctl stop firewalld.service

- firewalld 开放指定端口 （Centos7默认安装 firewalld）
  > firewall-cmd --zone=public --add-port=80/tcp --permanent
  >  
  > firewall-cmd --reload
 
- firewalld 关闭指定端口
  > firewall-cmd --zone=public --remove-port=80/tcp --permanent
  >  
  > firewall-cmd --reload

- firewalld 查看端口列表
  > firewall-cmd --permanent --list-port

### 常见错误

> 配置 ssl 证书时 ` nginx:[emerg]unknown directive ssl错误 `

-  原因 

    nginx 中缺少 SSL 模块
    
-  解决方案

    在原有的基础上添加 ssl 模块

```
步骤一

    切换到下载 nginx 的包压缩的解压目录

      cd /usr/local/nginx/nginx-1.18.0

步骤二

    添加这个ssl模块

      ./configure --with-http_ssl_module


    如果出现错误（./configure：错误：SSL模块需要OpenSSL库）
    原因是因为缺少了OpenSSL，执行

      yum -y install openssl openssl-devel


    等待OpenSSL的安装完成后，再执行

      ./configure
      ./configure --with-http_ssl_module 

步骤三

    进行编译

      make

    执行make命令，但是不要执行make install
    因为make是用来编译的，而make install是安装，不然你整个nginx会重新覆盖的。

步骤四

    可以查看到在nginx解压目录下，
    objs文件夹中多了一个nginx的文件，这个就是新版本的程序了。
    首先我们把之前的nginx先备份一下，然后把新的程序复制过去覆盖之前的即可。

      cp /usr/local/nginx/sbin/nginx /usr/local/nginx/sbin/nginx.bak
      cp objs/nginx /usr/local/nginx/sbin/nginx

步骤五

    检验是否有安装ssl模块成功
    Nginx安装目录下 执行./sbin/nginx -V

      cd /usr/local/nginx
      ./sbin/nginx -V
         
如下 说明安装成功 （TLS SNI support enabled ...）
[root@izuf6btw0rx08p19g1qo5sz nginx]# ./sbin/nginx -V
nginx version: nginx/1.18.0
built by gcc 4.8.5 20150623 (Red Hat 4.8.5-39) (GCC) 
built with OpenSSL 1.0.2k-fips  26 Jan 2017
TLS SNI support enabled
configure arguments: --prefix=/usr/local/nginx --with-http_ssl_module
```



# nginx 常用命令

> window   [nginx注册服务]( http://r6d.cn/WRVL ) 


### 通用命令

```javascript
   
  nginx -v  ->  显示 nginx 的版本
  
  start nginx  ->  启动 nginx
 
  nginx -t  ->  nginx 将检查配置文件的语法的正确性

  nginx -s reload  ->  重启，因改变了 Nginx 相关配置，需要重新加载配置而重载

  nginx -s stop  ->  快速关闭 Nginx，可能不保存相关信息，并迅速终止 Web 服务

  nginx -s quit  ->  平稳关闭 Nginx，保存相关信息，有安排的结束 Web 服务
  
```


### windows:

```javascript

  查询 nginx 所有进程  ->  tasklist /fi  "imagename eq nginx.exe"

  杀掉 nginx 所有进程  ->  taskkill /f /t /im nginx.exe

  杀掉 nginx 指定PID进程  >  taskkill  /f  /pid 4900  /pid  28808

```

 

### linux:

```javascript

  启动   ->  nginx -c /usr/local/nginx/conf/nginx.conf
   
  查看状态   ->  ps -ef | grep nginx
  
  查找文件   ->  find / -name nginx.conf
  
  删除文件夹 sss   ->  rm -rf sss/ 

  查看占用端口进程   ->  netstat -anp | grep :80
  
  杀掉 nginx 所有进程  ->  killall nginx

```

