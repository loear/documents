# CentOS7.9安装Docker

> Docker 要求 CentOS 系统的内核版本不低于3.10 。

- 查询内核版本命令：`uname -r`

演示
```
[root@CentOS7-9 ~]# uname -r
3.10.0-1160.21.1.el7.x86_64
```

## 若已安装，先卸载

- 卸载命令
```
$ sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

## 安装Docker Engine-Community

> 在新主机上首次安装 Docker Engine-Community 之前，需要设置 Docker 仓库，随后可以从仓库安装和更新 Docker。

### 设置仓库

- 安装所需的软件包。yum-utils 提供了 yum-config-manager ，并且 device mapper 存储驱动程序需要 device-mapper-persistent-data 和 lvm2。

```
$ sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
```

- 使用以下命令来设置稳定的仓库

国内阿里源
```
$ sudo yum-config-manager \
    --add-repo \
    http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

官方源
```
$ sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

### 安装 Docker Engine-Community

安装最新版本的 Docker Engine-Community 和 containerd

```
$ sudo yum install docker-ce docker-ce-cli containerd.io
```

安装过程中如果提示接受 GPG 密钥，选是。Docker 安装完默认未启动。并且已经创建好 docker 用户组，但该用户组下没有用户。

### 启动Docker

```
$ sudo systemctl start docker
```

- 查询版本
```
[root@CentOS7-9 ~]# docker --version
Docker version 20.10.5, build 55c4c88
```

- 通过运行 hello-world 映像来验证是否正确安装了 Docker Engine-Community

```
$ sudo docker run hello-world
```