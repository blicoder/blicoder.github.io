---
layout: post
title: Docker Dasar
---


## Pengenalan Docker

Docker adalah salah satu implementasi container manager

```
docker version
```

## Docker Registry

Docker Registry adalah tempat menyimpan docker image

## Docker Image

Docker Image mirip seperti installer aplikasi dimana di dalamnya terdapat aplikasi dan dependency

#### List image
```
docker image ls
docker images
```

#### Pull image dari registry
```
docker image pull imagename:tag
docker pull imagename
```

#### Hapus image
```
docker image rm imagename:tag
docker rmi imagename
```

## Docker Container

Docker container mirip seperti aplikasi hasil installer

#### Melihat container semua
```
docker container ls -a
docker ps -a
```

#### Melihat container berjalan
```
docker container ls
docker ps
```

#### Membuat Container
```
docker container create --name contoh image:tag
```

#### Menjalankan container
```
docker container start containername
docker start containername
```

#### Menghentikan container
```
docker container stop containername
docker stop containername
```

#### Menghapus container
```
docker container rm containername
docker rm containername
```

## Container Log

#### Melihat container log
```
docker container logs containername
docker logs containername
```

#### Melihat container log realtime
```
docker logs -f containername
```

## Container Exec

Container exec digunakan untuk mengeksekusi kode program yang terdapat di dalam container

#### Masuk ke container
```
docker container exec -it containername /bin/bash
docker exec -it containername bash
```
-i = menjaga input tetap aktif
-t = terminal akses


## Container Port

#### Port Forwading
```
docker container create --name containername --publish porthost:portcontainer image:tag
docker container create --name containername -p porthost:portcontainer -p porthost2:portcontainer2 image:tag
```

## Container Environment Variable

#### Menambah Environment Variable
```
docker container create --name containername --env KEY1="value" -e KEY2=value image:tag
```

## Container Stats

```
docker container stats
docker stats
```

## Container Resource Limit

```
docker container create --name containername --env KEY1="value" -e KEY2=value --memory 100m --cpus 0.5 image:tag
```

#### Memory
Misal 100m = 100 MB

b = bytes
k = kilo bytes
m = mega bytes
g = giga bytes

#### CPU
Misal 1.5 = satu dan setengah CPU core


## Bind Mounts

Bind Mounts merupakan kemampuan melakukan mounting (sharing) file atau folder yang terdapat di sistem host ke container yang terdapat di docker

#### Parameter Mount

| Parameter | Keterangan |
| - | - |
| type | Tipe mount, bind, dan volume |
| source | Lokasi file atau folder di sistem host |
| destination | Lokasi file atau folder di container |
| readonly | Jika ada, maka file atau folder hanya bisa dibaca di container, tidak bisa ditulis |

#### Melakukan Mounting
```
docker container create --name contaiername --mount "type=bind,source=folder,destination=folder,readonly" image:tag
```

## Docker volume (Recommendation)

Docker volume mirip bind mounts, bedanya adalah terdapat management volume, diman kita bisa membuat volume, melihat daftar volume, dan menghapus volume

Volume sendiri bisa dianggap storage yang digunakan menyimpan data, bedanya dengan bind mounts, pada bind mounts, data disimpan pada sistem host, sedangkan pada volume, data di manage oleh docker

#### Melihat docker volume
```
docker volume ls
```

#### Membuat doker volume
```
docker volume create volumename
```

#### Menghapus Volume
```
docker volume rm volumename
```

## Container Volume

```
docker container create --name containername --mount "type=volume,source=folder,destination=folder,readonly" image:tag
```

## Backup Volume

```
docker container stop mongovolume

docker container run --rm --name ubuntubackup --mount "type=bind,source=/Users/khannedy/Developments/YOUTUBE/belajar-docker-dasar/backup,destination=/backup" --mount "type=volume,source=mongodata,destination=/data" ubuntu:latest tar cvf /backup/backup-lagi.tar.gz /data

docker container start mongovolume
```

## Restore Volume

```
docker volume create mongorestore

docker container run --rm --name ubunturestore --mount "type=bind,source=/Users/khannedy/Developments/YOUTUBE/belajar-docker-dasar/backup,destination=/backup" --mount "type=volume,source=mongorestore,destination=/data" ubuntu:latest bash -c "cd /data && tar xvf /backup/backup.tar.gz --strip 1"

docker container create --name mongorestore --publish 27020:27017 --mount "type=volume,source=mongorestore,destination=/data/db" --env MONGO_INITDB_ROOT_USERNAME=eko --env MONGO_INITDB_ROOT_PASSWORD=eko mongo:latest

docker container start mongorestore
```

## Docker Network

Dengan menggunakan network, kita bisa mengkoneksikan container dengan container lain dalam satu network yg sama sehingga bisa saling berkomunikasi

#### Network Driver
- bridge
- host (hanya di docker linux)
- none

#### Melihat Network
```
docker network ls
```

#### Membuat Network
```
docker network create --driver drivername networkname
```

#### Menghapus Network
```
docker network rm networkname
```

## Container Network

#### Membuat container dengan network
```
docker container create --name containername --network networkname image:tag
```

#### Menghapus container dari network
```
docker network disconnect networkname containername
```

#### Menambahkan container ke network
```
docker network connect networkname containername
```

## Inspect

```
docker image inspect imagename
docker container inspect containername
docker volume inspect volumename
docker network inspect networkname
```

## Prune

```
docker image prune
docker container prune
docker volume prune
docker network prune
docker system prune
```