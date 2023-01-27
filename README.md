# nginx
my nginx sites-availables config default file

## node server
```nginx
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

```nginx
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

## floralux.guihon.cm

```nginx
server{

        root /var/www/floralux.guihon.cm;

        index index.html;
        server_name floralux.guihon.cm www.floralux.guihon.cm;

        location / {
                try_files $uri $uri/ = 404;
        }


    listen [::]:443 ssl; # managed by Certbot
    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/floralux.guihon.cm/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/floralux.guihon.cm/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

}
server{
    if ($host = floralux.guihon.cm) {
        return 301 https://$host$request_uri;
    } # managed by Certbot


        listen 80;
        listen [::]:80;
        server_name floralux.guihon.cm www.floralux.guihon.cm;
    return 404; # managed by Certbot


}

```

## Activate certificate tls/ssl
``` cmd
sudo certbot --nginx -d example.com -d www.example.com
```

## Delete Certificate
``` sh
sudo certbot delete domain.com
```



