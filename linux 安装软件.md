

# centos 7 安装 nginx



#### 安装编译工具及库文件

```shell
yum -y install make zlib zlib-devel gcc-c++ libtool  openssl openssl-devel
```

#### 首先要安装 PCRE

PCRE 作用是让 Nginx 支持 Rewrite 功能.

下载 PCRE 安装包，下载地址： http://downloads.sourceforge.net/project/pcre/pcre/8.35/pcre-8.35.tar.gz

```shell
cd /usr/local/src/

wget http://downloads.sourceforge.net/project/pcre/pcre/8.35/pcre-8.35.tar.gz
```

#### 解压安装包 进入安装包目录

```shell
tar zxvf pcre-8.35.tar.gz

cd pcre-8.35
```

#### 编译安装 

```shell
./configure

make && make install
```

#### 查看pcre版本

```shell
pcre-config --version
```

#### 下载 Nginx 并解压

下载地址：https://nginx.org/en/download.html

```shell
cd /usr/local/src/

wget http://nginx.org/download/nginx-1.20.1.tar.gz

tar zxvf nginx-1.20.1.tar.gz
```

#### 进入安装包目录 编译安装

```shell
 cd nginx-1.20.1
 
 ./configure --prefix=/usr/local/webserver/nginx --with-http_stub_status_module --with-http_ssl_module --with-pcre=/usr/local/src/pcre-8.35
 
 make && make install
```

#### 查看nginx版本

```shell
/usr/local/webserver/nginx/sbin/nginx -v
```



# centos 7 安装 mysql5.7.36



#### 下载并安装MySQL官方的 Yum Repository

   ```shell
cd /usr/local/src/

wget -i -c http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm
   ```

#### wget命令安装

```shell
yum install wget
```

#### 使用上面的命令就直接下载了安装用的Yum Repository，大概25KB的样子，然后就可以直接yum安装了

```shell
yum -y install mysql57-community-release-el7-10.noarch.rpm
```

#### 开始安装MySQL服务器

```shell
yum -y install mysql-community-server
```

#### 启动MySQL

```shell
systemctl start mysqld.service
```

#### 查看MySQL运行状态

```shell
systemctl status mysqld.service
```

#### 停止MySQL

```shell
systemctl stop mysqld.service
```

#### 查看文件安装路径

```shell
whereis mysql
```

#### 查询运行文件所在路径

```shell
which mysql
```

#### 查看默认密码

```shell
grep "temporary password" /var/log/mysqld.log
```

#### 用当前密码登录mysql（注：第一次使用mysql必须使用生成的密码，进入后才可进行修改操作）

```shell
mysql -uroot -p
```

#### 进入mysql后，修改密码机制（可忽略此步骤，默认密码设置必须要大小写字母数字和特殊符号）

##### 			查看当前密码机制

```shell
show global variables like '%validate_password%';
```

##### 			关闭密码复杂性策略

```shell
set global validate_password_policy=0;
```

##### 			设置密码最低长度为4

```shell
set global validate_password_length=4;
```

#### 进入mysql后，修改密码

```shell
ALTER USER 'root'@'localhost' IDENTIFIED BY 'new password';
```



# gcc 版本升级

```shell
// 安装环境依赖 
yum -y install bzip2

cd /usr/local/src/

// gcc下载地址http://ftp.gnu.org/gnu/gcc/，可以找到任意版本的.tar.gz
wget http://ftp.gnu.org/gnu/gcc/gcc-8.1.0/gcc-8.1.0.tar.gz

// 解压
tar -zxvf gcc-8.1.0.tar.gz 

// 下载依赖项
cd gcc-8.1.0
// 可能会出错 需要 安装bzip2 看下文
./contrib/download_prerequisites

// 创建文件夹，生成编译文件
mkdir gcc-build-8.1.0

cd gcc-build-8.1.0

../configure --enable-checking=release --enable-languages=c,c++ --disable-multilib

// 编译并安装
make && make install

重启服务器后，验证版本
gcc -v

// 重启后，查找编译 gcc 时生成的最新动态库
cd /usr/local/src/gcc-8.1.0/gcc-build-8.1.0

find / -name "libstdc++.so*"

// 将找到的动态库 libstdc++.so.6.0.24 复制到 /usr/lib64 
cp /usr/local/src/gcc-8.1.0/gcc-build-8.1.0/stage1-x86_64-pc-linux-gnu/libstdc++-v3/src/.libs/libstdc++.so.6.0.25 /usr/lib64

// 切换工作目录至 /usr/lib64，删除原来的软链接， 将默认库的软链接指向最新动态库
cd /usr/lib64
rm -rf libstdc++.so.6
ln -s libstdc++.so.6.0.25 libstdc++.so.6

```



# centos7  安装nodejs



## centos7 通过源码 安装nodejs



#### 安装环境依赖 

```shell
sudo yum install gcc gcc-c++
```

#### 下载资源包，并解压。 nodejs 官网下载地址 https://nodejs.org/en/download/

```shell
cd /usr/local/src/

wget http://nodejs.org/dist/v14.18.0/node-v14.18.0.tar.gz

tar xzvf node-v*
```

#### 进入目录编译安装

```shell
cd node-v*

./configure --prefix=/usr/local/nginx # 检查平台安装环境
# --prefix=/usr/local/nginx  是 nginx 编译安装的目录（推荐），安装完后会在此目录下生成相关文件

// 使用"make -j4"命令代替"make"实现并行编译得到一定程度上缓解。编译比较吃内存和CPU
make -j4 && make install
```

#### ./configure 可能出现错误。原因是gcc版本太老，需要下载新版本





## CentOS 7  通过 NodeSource存储库安装Node.js和npm



#### 添加NodeSource yum存储库

```shell
curl -sL https://rpm.nodesource.com/setup_14.x | sudo bash -
```

当系统提示您导入存储库GPG密钥时，键入`y`，然后按`Enter`。

#### 安装Node.js和npm

```shell
sudo yum install nodejs
```

#### 验证Node.js和npm的安装

要检查安装是否成功，请运行以下命令，以打印Node.js和npm版本

```shell
node --version

npm --version
```





## 使用NVM安装Node.js和npm



#### 安装NVM（Node.js版本管理器）

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash

or 

wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
```

该脚本会将nvm存储库从Github克隆到`~/.nvm`，并将脚本路径添加到您的Bash或ZSH配置文件中

```
=> Close and reopen your terminal to start using nvm or run the following to use it now:

export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

如以上输出所示，您应该关闭然后重新打开终端，或者运行命令以[将路径](https://www.myfreax.com/how-to-add-directory-to-path-in-linux/)至`nvm`脚本添加到当前会话。要验证是否正确安装了nvm，请输入

```shell
nvm --version
```



#### 使用NVM安装Node.js

现在已安装`nvm`工具，我们可以通过键入以下内容来安装Node.js的最新可用版本

```shell
nvm install node
```



```
Downloading and installing node v11.0.0...
Downloading https://nodejs.org/dist/v11.0.0/node-v11.0.0-linux-x64.tar.xz...
######################################################################## 100.0%
Computing checksum with sha256sum
Checksums matched!
Now using node v11.0.0 (npm v6.4.1)
Creating default alias: default -> node (-> v11.0.0)
```

通过键入以下内容来验证Node.js版本

```shell
node --version
```



#### 使用NVM安装多个Node.js版本

让我们再安装两个版本，即最新的LTS版本和8.12.0版

```shell
nvm install --lts
```

一旦安装了LTS版本和8.12.0，就会列出所有已安装的Node.js实例类型

```shell
nvm ls
```



```
->      v8.12.0                         # ACTIVE VERSION
       v10.13.0
        v11.0.0
default -> node (-> v11.0.0)           # DEFAULT VERSION
node -> stable (-> v11.0.0) (default)
stable -> 11.0 (-> v11.0.0) (default)
iojs -> N/A (default)
lts/* -> lts/dubnium (-> v10.13.0)
lts/argon -> v4.9.1 (-> N/A)
lts/boron -> v6.14.4 (-> N/A)
lts/carbon -> v8.12.0
lts/dubnium -> v10.13.0
```

输出告诉我们，左边带有箭头的条目（-> v8.12.0）是当前Shell会话中使用的版本，默认版本设置为v11.0.0。 默认版本是打开新外壳时将激活的版本

要更改当前活动的版本，可以使用以下命令

```shell
nvm use 10.13.0
```

输出看起来像这样

```shell
Now using node v10.13.0 (npm v6.4.1)
```

要更改默认的Node.js版本类型

```
nvm alias default 10.13.0

default -> 10.13.0 (-> v10.13.0)
```



## 安装开发工具

要能够从npm构建本机模块，我们将需要安装开发工具和库

```shell
sudo yum install gcc-c++ make
```





