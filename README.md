# nginx
my nginx sites-availables config default file

## node server
```
upstream mondomaine_fr {
    server localhost:4000;
}

server {

    listen 80;
    listen [::]:80; 
    server_name mondomaine.fr;

    location / {
        proxy_pass http://mondomaine_fr;
    }

    location /websocket/ {
        proxy_pass http://mondomaine_fr;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }

}
```

