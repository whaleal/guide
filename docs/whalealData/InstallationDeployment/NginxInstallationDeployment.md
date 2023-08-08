## Nginx 安装部署
### 开放指定端口或关闭防火墙
#### 1． 查看已经开放的端口
    firewall-cmd --list-ports
#### 2.开放指定端口 
    firewall-cmd --zone=public --add-port=80/tcp --permanent
#### 3.重新加载防火墙配置
       firewall-cmd --reload
#### 4.确认端口开放
       firewall-cmd --list-ports
#### 5.关闭防火墙
       systemctl stop firewalld
#### 6.确认防火墙状态
       systemctl status firewalld
### 安装部署
#### 1. 解压安装包
     tar -zxvf nginx-1.16.1.tar.gz -C /usr/local/
#### 2. 安装依赖
     yum install -y pcre pcre-devel
     yum install -y zlib zlib-devel
#### 3. 配置路径
     ./configure --prefix=/usr/local/nginx
#### 4. 编译
     make && make install
#### 5. 配置本地主机访问域名解析
     vi /etc/hosts
     ip cloud.whalealMG.com
#### 6. 编辑配置文件
```
server {
 listen 80;
 server_name cloud.whalealmg.com; #本地域名解析
#charset koi8-r;
#access_log logs/host.access.log main;
location / {
root /usr/local/nginx/html/dist/; #前端介质包路径
index index.html index.htm;
try_files $uri $uri/ /index.html;
}
location /filingAdmin/{
proxy_pass http://127.0.0.1:8000/;
proxy_set_header X-Forwarded-Proto $scheme;
proxy_set_header X-Forwarded-Port $server_port;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection "upgrade";
}
location ~ .*\.(js|css|jpg|jpeg|gif|png|ico|pdf|txt)$ {
root /usr/local/nginx/html/dist/;
index index.html index.htm;
}
#error_page 404 /404.html;
# redirect server error pages to the static page /50x.html
#
error_page 500 502 503 504 /50x.html;
location = /50x.html {
root html;
}
}
```
#### 7. 启动服务
      /usr/local/nginx/sbin/nginx  