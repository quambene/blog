<!-- markdownlint-disable MD001 -->

# Nginx

- [Port](#port)
- [Host](#host)
- [Static assets](#static-assets)
- [Redirection](#redirection)
- [Reverse proxy](#reverse-proxy)
- [Load balancing](#load-balancing)
- [SSL](#ssl)

### Port

```nginx
server {
    # http (IPv4)
    listen 80;

    # https (IPv4)
    listen 443 ssl;

    # http/2
    listen 443 ssl http2;

    # http (IPv6)
    listen [::]:80;

    # http (IPv6 only)
    listen [::]:80 ipv6only=on;

    # https (IPv6)
    listen [::]:443 ssl http2;
}
```

### Host

```nginx
# default
server {
    listen 443 ssl http2;
    server_name my-domain.com www.my-domain.com;
}

server {
    listen 443 ssl http2;
    server_name my-domain.net www.my-domain.net;
}

server {
    listen 443 ssl http2;
    server_name my-domain.org www.my-domain.org;
}
```

### Static assets

```nginx
server {
    listen 443 ssl http2;
    server_name my-domain.com www.my-domain.com;
    root /var/www/my-website;
    index index.html;
}
```

### Redirection

```nginx
# Redirection from my-domain.com to my-other-domain.com
server {
    listen 443 ssl http2;
    server_name my-domain.com www.my-domain.com;
    return 301 https://my-other-domain.com$request_uri;
}

# Redirection from http to https
server {
    listen 80;
    server_name my-domain.com www.my-domain.com;
    return 301 https://$host$request_uri;
}
```

### Reverse proxy

```nginx
server {
    listen 443 ssl http2;
    server_name my-domain.com www.my-domain.com;
    
    location / {
        proxy_pass http://0.0.0.0:3000;
    }
}
```

### Load balancing

```nginx
upstream my-backend {
    # default load balancing method: round-robin
    server backend1.example.com;
    server backend2.example.com;
    server backend3.example.com;
}

server {
    listen 443 ssl http2;
    server_name my-domain.com www.my-domain.com;
    
    location / {
        proxy_pass https://my-backend;
    }
}
```

### SSL

```nginx
server {
    listen 443 ssl http2;
    server_name my-domain.com www.my-domain.com;

    ssl_certificate /my-path/my-cert.pem;
    ssl_certificate_key /my-path/my-private-key.pem;

    # OSCP stapling
    ssl_stapling on;
    ssl_stapling_verify on;

    # optimizations
    keepalive 70;
    ssl_session_cache shared:SSL:10m;
    ssl_session_timeout 10m;
}
```
