# nextcloud-docker
> Simple private cloud in Docker ! 

## Run 

> git clone https://github.com/13paulmurith/nextcloud-docker.git

> docker-compose up -d & docker-compose stop

#### Using IP to access Nextcloud : 
> Remove the 4430 server part from nextcloud-example.conf and edit it like this : 

server {
  listen 8000;
  server_name {server_ip};
}

#### Using domain name 
> Add DNS host entry to your domain and change server_name (use 'nextcloud-example.conf' it's easier)

server {
  listen 8000;
  server_name nextcloud.domain.tld;
  return 301 https://$host$request_uri;
}

server {
  listen 4430 ssl http2;
  server_name nextcloud.domain.tld;
  ssl_certificate /certs/domain.tld.crt;
  ssl_certificate_key /certs/domain.tld.key;
  location / {
    proxy_pass http://nextcloud:8888;
    include /conf.d/proxy-params.conf;
  }
}

#### Obtain a free certificate
> Navigate to https://certbot.eff.org/lets-encrypt and follow instructions
