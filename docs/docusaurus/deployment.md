# Deployment

## Deployment to Fly.io

Run `fly launch`, it will generate Dockerfile.

Create `./nginx.conf` file with the content: 

```nginx
user  nginx;
worker_processes  auto;

error_log  /var/log/nginx/error.log notice;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    include /etc/nginx/conf.d/*.conf;

    server {
        root /app;
        listen 8080;
    }
}
```

If you have you own domain the last part of the configuration will be:

```nginx
server {
    if ($host = <app-name>.fly.dev) {
        return 301 $scheme://<your-domain.com>.$request_uri;
    }
    root /app;
    listen 8080;
    location / {
        try_files $uri /index.html;
    }
}
```

Open `./Dockerfile` and replace the last image with:

```Docker
FROM nginx

COPY --from=builder /app/build /app
COPY nginx.conf /etc/nginx/nginx.conf
```

Run `fly deploy`

