# Docker commands

### Pull nginx image

```docker pull nginx```

### To run a nginx container:

```docker run -it -d -p 8000:80 --name website nginx```

### Acessing page content

```curl localhost:8000```

### Stop container

```docker stop website```

### Acess internal container shell

```docker exec -it website /bin/bash```

### All processes in localhost:

```docker top website```

## Basic Service Management - Inside the container

### Terminate container (On container shell)

```service nginx stop```

### Remove container image

```docker rm website```

## Building custom nginx image

* Create Dockerfile locally:

```
FROM nginx:latest

COPY ./html/index.html /usr/share/nginx/html/index.html
```

* Create docker-compose.yml

```
version: '3'

services:
  nginx:
    build:
      context: .
    ports:
      - 8000:80
    volumes:
      - ./html/:/usr/share/nginx/html/
```

* Build the image

```
docker build -t webserver
```

* Run the container

```
docker run
```

## Container Processes

* update Dockerfile to:

```
FROM nginx:latest

COPY ./html/index.html /usr/share/nginx/html/index.html

RUN apt-get update && apt-get install -y procps
```

* Inside the container shell:

```
ps -C nginx -f
```

* To reload nginx service:

```
nginx -s reload
```

## Serving STATIC content