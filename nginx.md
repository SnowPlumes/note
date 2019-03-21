### 全局变量
- **$args** 请求行中的参数
- **$host** 请求主机头字段,否则为服务器名称
- **$request_method** 客户端请求方法 GET,POST等
- **$remote_addr** 客户端ip
- **remote_port** 客户端端口
- **$scheme** http方法 http,https
- **$server_addr** 服务器地址
- **$server_name** 服务器名称
- **$server_port** 服务器端口
- **$request_uri** 包含请求参数的原始uri,不包含主机名
- **$uri** 不带请求参数的uri,不包含主机名

### 主机名匹配
- 从上到下优先级从高到低
   > 1. 明确的server_name名称
   > 2. 前缀通配符
   > 3. 后缀通配符
   > 4. 正则表达式

### location查找规则
- 从上到下优先级从高到低
    > 1. 等号类型,精确匹配,如 location - / {}
    > 2. `^~`类型,前缀匹配,不支持正则, location ^~ /user {}
    > 3. `~`和`~*`类型,正则匹配,`~`区分大小写,`~*`不区分大小写
    > 4. 常规字符串匹配类型

### try_file规则
> try_files $uri $uri/ /index.html
> 假设请求为http://www.me.com/test,则 **$uri** 为 `test`
    > 1. 查找 `/$root/test` 文件
    > 2. 查找 `/$root/test/` 目录
    > 3. 发起 `/index.html` 的内部子请求

### rewrite 规则
> rewrite ^/images/(.*).(png|jpg|gif)$ /images?name=$1.$4 last;
    > 1. last : 表示完成rewrite
    > 2. break: 停止执行当前虚拟主机的后续rewrite指令集
    > 3. redirect : 返回302临时重定向，地址栏会显示跳转后的地址
    > 4. permanent : 返回301永久重定向，地址栏会显示跳转后的地址

### 负载均衡
```
upstream backend1 {
    server backend1.qq.com weight=5;
    server 127.0.0.1:8080 max_fails=3 fail_timeout=30s;
    server unix:/tmp/backend3 backup;
}

upstream backend2 {
    ip_hash;
    server backend1.qq.com;
    server backend2.qq.com;
    server backend3.qq.com down;
    server backend4.qq.com;
}

server {
    location / {
        proxy_pass http://backend1;
    }

    location /api {
        proxy_pass http://backend2;
    }
}
```