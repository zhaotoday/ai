#### 宝塔添加反向代理：
- 代理名称：gemini-proxy
- 目标URL：https://generativelanguage.googleapis.com
- 发送域名：generativelanguage.googleapis.com
- 在生成的配置文件添加：proxy_ssl_server_name on;

```
#PROXY-START/

location ^~ /
{
    proxy_pass https://generativelanguage.googleapis.com;
    proxy_set_header Host generativelanguage.googleapis.com;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header REMOTE-HOST $remote_addr;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection $connection_upgrade;
    proxy_http_version 1.1;
    # proxy_hide_header Upgrade;
    proxy_ssl_server_name on;

    add_header X-Cache $upstream_cache_status;
    #Set Nginx Cache

    set $static_fileqWcmOeE1 0;
    if ( $uri ~* "\.(gif|png|jpg|css|js|woff|woff2)$" )
    {
        set $static_fileqWcmOeE1 1;
        expires 1m;
    }
    if ( $static_fileqWcmOeE1 = 0 )
    {
        add_header Cache-Control no-cache;
    }
}
#PROXY-END/
```
