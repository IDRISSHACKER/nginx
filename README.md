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

## react-js server

```
server{

        listen 80;
        listen [::]:80;

        root /var/www/cdn.guihon.cm;

        index index.html;
        server_name cdn.guihon.cm www.cdn.guihon.cm;

        location / {
                try_files $uri $uri/ = 404;
        }
}




```
