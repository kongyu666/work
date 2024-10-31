# 使用Nginx

## 简单的示例

创建一个简单的示例，来测试Nginx是否正常

```
sudo tee /etc/nginx/conf.d/demo.conf <<EOF
server {
  listen 8000;
  server_name _;
  root /data/service/frontend/demo;
  index index.html;
}
EOF
```

创建文件

```
mkdir -p /data/service/frontend/demo
echo "hello world" > /data/service/frontend/demo/index.html
```

重新读取配置

```
sudo systemctl reload nginx
```

访问服务

```
curl localhost:8000
```

## 反向代理

配置Nginx作为反向代理，将请求转发到指定地址，如：`http://localhost:9000`

创建一个简单的示例，来测试Nginx是否正常

```
sudo tee /etc/nginx/conf.d/demo.conf <<EOF
upstream backend_servers {
    server 192.168.1.101:9000;
    server 192.168.1.102:9000;
    server 192.168.1.103:9000;
}
server {
    listen 19000;
    server_name _;

    location / {
        proxy_pass http://backend_servers;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
EOF
```

重新读取配置

```
sudo systemctl reload nginx
```

访问服务

```
curl localhost:19000
```

## 配置Vue资源服务

创建配置文件

```nginx
sudo tee /etc/nginx/conf.d/8001-vue-demo.conf <<"EOF"
server {
    listen       8001;
    server_name  _;

    location / {
        if ($request_method = 'OPTIONS') {
            add_header 'Access-Control-Allow-Origin' '*';
            add_header 'Access-Control-Allow-Methods' 'GET, POST, PUT, DELETE, OPTIONS, HEAD';
            add_header 'Access-Control-Allow-Headers' 'Origin, X-Requested-With, Content-Type, Accept, Authorization, token';
            add_header 'Access-Control-Max-Age' 1728000;
            add_header 'Content-Length' 0;
            return 204;
        }

        add_header 'Access-Control-Allow-Origin' '*';
        add_header 'Access-Control-Allow-Methods' 'GET, POST, PUT, DELETE, OPTIONS, HEAD';
        add_header 'Access-Control-Allow-Headers' 'Origin, X-Requested-With, Content-Type, Accept, Authorization, token';
        add_header 'Access-Control-Allow-Credentials' 'true';
        add_header 'Access-Control-Max-Age' 1728000;

        proxy_set_header Host               $host;
        proxy_set_header X-Real-IP          $remote_addr;
        proxy_set_header X-Forwarded-For    $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto  $scheme;
        proxy_redirect                      off;

        root   /data/service/frontend/vue-demo/dist;
        index  index.html;
        try_files $uri $uri/ /index.html;
    }
}
EOF
```

配置解释

- `listen 8001;`: 指定服务器监听的端口。
- `server_name _;`: 设定服务器名称为 `_`，通常用于匹配所有请求。
- `location / { ... }`: 处理所有以 `/` 开头的请求。
    - `if ($request_method = 'OPTIONS') { ... }`: 处理 CORS 预检请求（`OPTIONS` 方法）。设置适当的 CORS 头部，并返回 204 状态码。

    - `add_header 'Access-Control-Allow-Origin' '*';`: 设置允许所有来源访问的 CORS 头部。
    - `add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS';`: 允许的请求方法。
    - `add_header 'Access-Control-Allow-Headers' 'Origin, X-Requested-With, Content-Type, Accept';`: 允许的请求头。
    - `add_header 'Access-Control-Allow-Credentials' 'true';`: 允许发送凭证（如 cookies）。
    - `add_header 'Access-Control-Max-Age' 1728000;`: 预检请求的缓存时间。

    - `proxy_set_header` 指令: 设置传递到后端服务器的请求头部，确保获取客户端真实 IP 等信息。

    - `root /data/service/frontend/vue-html/dist;`: 设置根目录为构建后的文件位置。
    - `index index.html;`: 指定默认首页文件。
    - `try_files $uri $uri/ /index.html;`: 尝试匹配请求的 URI 或目录，如果都不存在，则返回 `index.html`，通常用于前端路由。

创建数据目录并解压文件

```shell
mkdir -p /data/service/frontend/vue-demo/
cd /data/service/frontend/vue-demo/
unzip dist.zip
```

重新读取配置

```
sudo systemctl reload nginx
```

访问服务

```
http://192.168.1.112:8001
```



## 配置HTTPS

### 1. 使用 OpenSSL 创建自签名证书

首先，我们需要生成 SSL 证书和私钥。以下是使用 OpenSSL 创建自签名证书的步骤和命令：

详细的生成证书参考：https://kongyu666.github.io/work/#/work/service/tls/tls-openssl/

```bash
# 创建目录
sudo mkdir -p /etc/nginx/ssl

# 生成私钥
sudo openssl genrsa -out /etc/nginx/ssl/private.key 2048

# 生成自签名证书
sudo openssl req -new -x509 -key /etc/nginx/ssl/private.key -out /etc/nginx/ssl/certificate.crt -days 365 -utf8 \
    -subj "/C=CN/ST=重庆市/L=重庆市/O=阿腾集团/OU=研发中心/CN=nginx.ateng.local"
```

这些命令将生成一个私钥文件 `private.key` 和一个自签名证书文件 `certificate.crt`，有效期为 365 天。

- `openssl genrsa`：生成一个 RSA 私钥。

- `openssl req -new -x509`：创建一个新的 X.509 证书请求，并使用私钥签名生成自签名证书。

    - `/C=AU`: 国家代码（2 个字母），例如 AU 表示澳大利亚。

    - `/ST=Some-State`: 州或省的名称。

    - `/L=Some-City`: 城市名称。

    - `/O=My-Company`: 组织名称（公司名）。

    - `/OU=My-Department`: 组织单位名称（部门）。

    - `/CN=your_domain.com`: 通用名称（通常是服务器的 FQDN 或者域名），替换为你的域名。

### 2. 配置 Nginx 使用 HTTPS

以下是一个简单的 Nginx 配置文件，启用 HTTPS 并使用刚刚创建的 SSL 证书：

```nginx
sudo tee /etc/nginx/conf.d/demo-https.conf <<"EOF"
server {
    listen 80;
    server_name nginx.ateng.local;
    return 301 https://$host$request_uri;
}
server {
    listen 443 ssl;  # 监听 443 端口并启用 SSL

    server_name nginx.ateng.local;  # 替换为你的域名

    ssl_certificate /etc/nginx/ssl/certificate.crt;  # SSL 证书路径
    ssl_certificate_key /etc/nginx/ssl/private.key;  # SSL 私钥路径

    ssl_protocols TLSv1.2 TLSv1.3;  # 启用的 SSL 协议
    ssl_ciphers HIGH:!aNULL:!MD5;   # 安全加密算法配置

    location / {
        root /data/service/frontend/demo-https;  # 网站根目录
        index index.html;
    }
}
EOF
```

配置说明

- **`listen 443 ssl;`**: Nginx 监听 443 端口并启用 SSL（HTTPS）。
- **`server_name your_domain.com;`**: 替换为你自己的域名。
- **`ssl_certificate`**: 指定 SSL 证书的路径。
- **`ssl_certificate_key`**: 指定 SSL 私钥的路径。
- **`ssl_protocols`**: 启用的 SSL/TLS 协议版本，这里使用 TLS 1.2 和 TLS 1.3。
- **`ssl_ciphers`**: 指定允许的加密算法，用于增强安全性。
- **`location /`**: 定义网站的根目录。
- **`if ($scheme = http)`**: 将 HTTP 请求重定向到 HTTPS，确保所有流量使用加密连接。

### 3. 创建文件

```
mkdir -p /data/service/frontend/demo-https
echo "hello world https" > /data/service/frontend/demo-https/index.html
```

### 4. 启动或重新加载 Nginx

在配置完 Nginx 后，启动或重新加载服务以使更改生效：

```bash
sudo systemctl reload nginx
```

通过上述配置，Nginx 将启用 HTTPS 并使用生成的自签名证书。请注意，自签名证书通常用于开发和测试环境，而不是生产环境。在生产环境中，建议使用受信任的证书颁发机构（CA）签发的证书。

### 5. 访问服务

```
curl --cacert /etc/nginx/ssl/certificate.crt https://nginx.ateng.local
```
