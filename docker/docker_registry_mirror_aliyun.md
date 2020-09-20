# Docker更换阿里云镜像加速


## 环境

- 一台安装了Docker的CentOS6.9版本Linux服务器

- 一个阿里云账号

## 操作

1. 登录阿里云地址 `https://www.aliyun.com/`

2. 打开控制台-容器镜像服务-镜像中心-镜像加速器，可以看到加速器地址 `https://xxx.mirror.aliyuncs.com` 添加到配置文件中

```bash
[guo@iZwz9hw8pun8vmbs0u0ckeZ ~]$ cat /etc/sysconfig/docker 
# /etc/sysconfig/docker
#
# Other arguments to pass to the docker daemon process
# These will be parsed by the sysv initscript and appended
# to the arguments list passed to docker -d

other_args="--registry-mirror=https://xxx.mirror.aliyuncs.com"
```

3. 重启Docker后台服务`service docker restart`

```bash
[guo@iZwz9hw8pun8vmbs0u0ckeZ ~]$ sudo service docker restart
Stopping docker:                                           [  OK  ]
Starting docker:                                           [  OK  ]
```

4. 更换网易的操作类似于阿里云