# Docker使用技巧

## 搜索

- 命令： `docker search [镜像名字]`

```
docker search nginx
```

## 镜像

### 搜索镜像`docker search [OPTIONS] TERM`

- 搜索名字为hello-world过滤展示stars大于100的列表
```
[root@CentOS7-9 ~]# docker search -f=stars=100 hello-world
NAME                          DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
hello-world                   Hello World! (an example of minimal Dockeriz…   1405      [OK]       
kitematic/hello-world-nginx   A light-weight nginx container that demonstr…   147 
```

- 输出完整的镜像描述`--no-trunc`
```
[root@CentOS7-9 ~]# docker search --no-trunc -f=stars=100 hello-world
NAME                          DESCRIPTION                                                                  STARS     OFFICIAL   AUTOMATED
hello-world                   Hello World! (an example of minimal Dockerization)                           1405      [OK]       
kitematic/hello-world-nginx   A light-weight nginx container that demonstrates the features of Kitematic   147  
```

### 下载镜像`docker pull NAME`

```
[root@CentOS7-9 ~]# docker pull nginx
Using default tag: latest
latest: Pulling from library/nginx
75646c2fb410: Pull complete 
6128033c842f: Pull complete 
71a81b5270eb: Pull complete 
b5fc821c48a1: Pull complete 
da3f514a6428: Pull complete 
3be359fed358: Pull complete 
Digest: sha256:bae781e7f518e0fb02245140c97e6ddc9f5fcf6aecc043dd9d17e33aec81c832
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest
```

###  查询本地镜像`docker images`

```
[root@CentOS7-9 ~]# docker images
REPOSITORY   TAG       IMAGE ID       CREATED      SIZE
nginx        latest    7ce4f91ef623   3 days ago   133MB
```

### 运行镜像
```
docker run --name nginx-stp \
-p 80:80 -p 443:443 \
-v /home/nginx/nginx.conf:/etc/nginx/nginx.conf \
-v /home/nginx/conf.d:/etc/nginx/conf.d \
-v /home/nginx/logs:/var/log/nginx \
-v /data/wwwroot:/usr/share/nginx/html \
-d nginx
```

### 删除镜像 `docker rmi IMAGE`

```
[root@CentOS7-9 ~]# docker rmi hello-world
Untagged: hello-world:latest
Untagged: hello-world@sha256:308866a43596e83578c7dfa15e27a73011bdd402185a84c5cd7f32a88b501a24
Deleted: sha256:d1165f2212346b2bab48cb01c1e39ee8ad1be46b87873d9ca7a4e434980a7726
Deleted: sha256:f22b99068db93900abe17f7f5e09ec775c2826ecfe9db961fea68293744144bd
```

### 创建镜像


