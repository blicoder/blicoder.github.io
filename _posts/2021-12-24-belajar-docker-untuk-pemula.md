---
layout: post
title: Belajar Docker Untuk Pemula
---

### Download image
```
docker pull imagename
```

### Melihat image yang ada
```
docker images
```

### Membuat dan menjalankan sebuah container
```
docker run imagename
```

### Membuat dan menjalankan sebuah container detach dengan tag image
```
docker run -d imagename:tag
```

### Membuat dan menjalankan sebuah container dengan forwarding port
```
docker run -p portout:portin -d imagename
```

### Membuat dan menjalankan sebuah container dengan forwarding port serta memberi nama
```
docker run -p portout:portin -d --name containername imagename
```

### Melihat container yang aktif
```
docker ps
```

### Melihat semua container
```
docker ps -a
```

### Stop container
```
docker stop containerid
```

### Start container
```
docker start containerid
```

### Melihat log container
```
docker logs containerid
docker logs containername
```

### Melihat log container realtime
```
docker logs -f containername
```

### Masuk ke container
```
docker exec -it containername bash
```








### Syntax di Linux
```
hostname

pwd

ls

env

exit
```


### Dockerfile

```
// Ambil base dari image lain (instalasi nodejs)
FROM node

// set env
ENV API_URL=http://api.docker.com

// menjalankan perintah apapun di image (membuat folder /app)
RUN mkdir /app

// menjalankan perintah di host/local (copy semua file di dalam folder sekarang (host) ke dalam /app (image))
COPY . /app

// (instalasi dependensi)
RUN yarn install

// (jalankan app)
CMD ["yarn", "serve"]
```

```
FROM golang

// buat folder /app jika belum ada, dan set working direktori ke /app (defaultnya ke /)
WORKDIR /app

COPY . .

RUN go build -o todo-api

// dokumentasi app port
EXPOSE 8080

CMD ./todo-api
```

```
docker build -t todo-frontend:v1 .
```



### Registry
```
docker tag containername:tag dipsinisasi/containername:tag

docker login --username dipsinisasi

docker push dipsinisasi/containername:tag
```




### Example
```
docker run -d \
 -p 5433:5432 \
 --name todo-postgres \
 -e POSTGRES_USER=postgres \
 -e POSTGRES_PASSWORD=secret \
-e POSTGRES_DB=belajar \
 -v $(pwd)/postgres/init.sql:/docker-entrypoint-initdb.d/init.sql \
 --network todo \
 postgres
```

```
docker exec -it todo-postgres psql -U postgres -W belajar
```

```
docker build -t todo-frontend:v1 .

docker build -t todo-backend:v1 .

docker network create todo

docker run -d -p 8080:8080 -e DB_USER=postgres -e DB_PASSWORD=secret -e DB_HOST=todo-postgres -e DB_PORT=5432 -e DB_DATABASE=belajar --network todo todo-backend:v1 

docker run -d -p 8081:8080 todo-frontend:v1

```

```
docker compose up
docker compose up -d
docker compose up -f todo.yaml up
```

### Docker Compose
```
# versi docker-compose
version: '3'

# konfigurasi docker
services:
    # --name containername
    todo-postgres:
        image: postgres
        ports:
            - 5433:5432
        environment:
            - POSTGRES_USER=postgres
            - POSTGRES_PASSWORD=rahasia
            - POSTGRES_DB=belajar
        volumes:
            - ./postgres/init.sql:/docker-entrypoint-initdb.d/init.sql
    todo-backend:
        # build
        # image: dipsinisasi/containername
        build: ./backend
        ports:
            - 8080:8080
        environment:
            - DB_USER=postgres
            - DB_PASSWORD=rahasia
            - DB_HOST=todo-postgres
            - DB_PORT=5432
            - DB_DATABASE=belajar
        # menjalankan backend setelah postgres
        depends_on:
            - todo-postgres
    todo-frontend:
        # image: dipsinisasi/containername
        build: ./frontend
        ports:
            - 8081:8080

```