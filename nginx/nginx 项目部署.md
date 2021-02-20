# nginx 开启 gzip 压缩
 
 > 需要前端打开 gzip 配合使用

```c
    # 开启 gzip 模式
    gzip on;
    
    # gizp 压缩起点，文件大于25k才进行压缩
    gzip_min_length 25;
    
    # gzip 压缩级别为1-9，数字越大压缩的越好，也越占用 CPU 的资源，自己一般设置 4-6 范围
    gzip_comp_level 4;
    
    # 进行压缩的文件类型
    gzip_types text/plain application/javascript text/css application/xml text/javascript application/json;
    
    # 是否传输 gzip 压缩标志，就是在 http header 中添加 Vary: Accept-Encoding，建议开启
    gzip_vary on;
    
    # 设置 gzip 压缩针对的 http 协议版本，可以不设置，目前几乎都是 1.1
    gzip_http_version 1.1;
```

# nginx  网络代理

###  location 匹配规则

- vue 中 vue.config.js  proxy代理
```javascript
  proxy: {
    "/A": {
      target: "http://www.baidu.com",
      pathRewrite: {
        "^/A": "",
      },
    },
    "/B": {
      target: "http://www.baidu.com",
    }
  }

```

- nginx 中 nginx.config 
```javascript
  serve{
    listen        80;
    server_name  localhost;
    
    location /A/ {
        proxy_set_header Host www.baidu.com;
        proxy_pass http://www.baidu.com/;
    }
    
    location /B {
        proxy_set_header Host www.baidu.com;
        proxy_pass http://www.baidu.com;
    }
  }

```
- 结果
  > `localhost/A/xxx` 最终会匹配到 `http://www.baidu.com/xxx `
  > 
  > `localhost/B/xxx` 最终会匹配到 `http://www.baidu.com/B/xxx`


# nginx 配置 

```c
# 运行用户
#user  nobody;

# 启动进程，通常设置成和 CPU 的数量相等
worker_processes  1;

# 全局错误日志
#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

# PID 文件，记录当前启动的 Nginx 的进程 ID
#pid        logs/nginx.pid;

# 工作模式及连接数上限
events {
    # 单个后台 worker process 进程的最大并发链接数
    worker_connections  1024;
}


# 设定 HTTP 服务器，利用它的反向代理功能提供负载均衡支持
http {
    # 设定 mime 类型（邮件支持类型），类型由 mime.types 文件定义
    include       mime.types;
    default_type  application/octet-stream;

    # 设定日志
    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    # sendfile 指令指定 Nginx 是否调用 sendfile 函数（zero copy 方式）来输出文件，对于普通应用，
    # 必须设为 on，如果用来进行下载等应用磁盘 IO 重负载应用，可设置为 off，以平衡磁盘与网络 I/O 处理速度，降低系统的 uptime.
    sendfile        on;
    #tcp_nopush     on;

    # 连接超时时间
    keepalive_timeout  65;

    # 开启 GZIP 压缩
    gzip  on;
    gzip_buffers 4 16k;
    gzip_min_length 1k;
    gzip_comp_level 9;
    gzip_types text/plain application/javascript text/css application/xml text/javascript application/json;
    gzip_vary on;
    gzip_disable "MSIE [1-6]\.";

    # HTTP 服务器
    server {
        # 监听端口
        listen      80;
        listen      443 ssl;
        # 定义域名
        server_name xxx.cn;

        # 配置 ssl 域名证书
        ssl_certificate ../cert/xxx.pem;  
        ssl_certificate_key ../cert/xxx.key;

        # 配置 ssl
        ssl_session_timeout 5m;
        ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        ssl_prefer_server_ciphers on;

        # Vue 路由模式为 history 需添加的配置
        location / {
            if (!-e $request_filename) {
                rewrite ^(.*)$ /index.html?s=$1 last;
                break;
            }
            root   dist;
            index  index.html;
        }

        location /A/ {
            proxy_set_header Host www.baidu.com;
            proxy_pass http://www.baidu.com/;
        }

        location /B {
            proxy_set_header Host www.baidu.com;
            proxy_pass http://www.baidu.com;
        }

        # 以上为完整版需要加的反向代理转发路径规则

        # 获取真实 IP 以及 Websocket 需添加的配置
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header REMOTE-HOST $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";

        # 客户端 Body 大小限制（文件上传大小限制配置）
        client_max_body_size 8m;

        error_page   500 502 503 504 404  /50x.html;
        location = /50x.html {
            root   html;
        }

    }

}

```
