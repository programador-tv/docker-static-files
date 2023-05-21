# docker-static-files
Forma simples de servir arquivos estáticos na web com docker


### Inicializando
```shell
    docker-compose up -d

```
- http://localhost:8080/index.html
- http://localhost:8080/videos/chrome.webm


### Configurando
```
    # Caso queira apontar para qualquer pasta no host
    # defina o caminho relativo à onde está o docker-compose.yml

     volumes:
     - ./files/:/usr/share/nginx/html/
 >>> - ../app2/wwwroot/:/usr/share/nginx/html/
```


### Configurações nginx
```
server {
    server_name   mediaserver.programador.tv;
    location / {
        proxy_pass         http://your.com:8080;
        proxy_http_version 1.1;
        proxy_set_header   Upgrade $http_upgrade;
        proxy_set_header   Connection keep-alive;
        proxy_set_header   Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header   X-Forwarded-Proto $scheme;
    	add_header Access-Control-Allow-Origin *;
	}

}

```