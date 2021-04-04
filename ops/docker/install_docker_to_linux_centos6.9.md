# Linux系统CentOS6.8/9安装Docker

## 环境

- 一台阿里云CentOS6.9服务器

## 操作

### 查看系统版本

!> 命令：`lsb_release -a`

```bash
[guo@iZwz9hw8pun8vmbs0u0ckeZ ~]$ yum -y install lsb
...
[guo@iZwz9hw8pun8vmbs0u0ckeZ ~]$ lsb_release -a
LSB Version:    :base-4.0-amd64:base-4.0-noarch:core-4.0-amd64:core-4.0-noarch:graphics-4.0-amd64:graphics-4.0-noarch:printing-4.0-amd64:printing-4.0-noarch
Distributor ID: CentOS
Description:    CentOS release 6.9 (Final)
Release:        6.9
Codename:       Final
```

### 确保已经持有EPEL仓库

!> 命令： `yum install -y epel-release`

```bash
[guo@iZwz9hw8pun8vmbs0u0ckeZ ~]$ sudo yum install -y epel-release
Loaded plugins: fastestmirror
Setting up Install Process
Determining fastest mirrors
 * base: mirrors.aliyun.com
 * extras: mirrors.aliyun.com
 * nux-dextop: mirror.li.nux.ro
 * rpmfusion-free-updates: mirrors.ustc.edu.cn
 * rpmfusion-nonfree-updates: mirror.lzu.edu.cn
 * updates: mirrors.aliyun.com
base                                                                                                                  | 3.7 kB     00:00     
base/primary_db                                                                                                       | 4.7 MB     00:00     
centos-sclo-rh                                                                                                        | 2.9 kB     00:00     
centos-sclo-rh/primary_db                                                                                             | 1.5 MB     01:37     
epel                                                                                                                  | 4.7 kB     00:00     
epel/primary_db                                                                                                       | 6.1 MB     00:00     
extras                                                                                                                | 3.4 kB     00:00     
extras/primary_db                                                                                                     |  29 kB     00:00     
nux-dextop                                                                                                            | 2.9 kB     00:00     
nux-dextop/primary_db                                                                                                 | 1.0 MB     00:07     
rpmfusion-free-updates                                                                                                | 3.7 kB     00:00     
rpmfusion-free-updates/primary_db                                                                                     | 177 kB     00:00     
rpmfusion-nonfree-updates                                                                                             | 3.7 kB     00:00     
rpmfusion-nonfree-updates/primary_db                                                                                  |  33 kB     00:00     
updates                                                                                                               | 3.4 kB     00:00     
updates/primary_db                                                                                                    | 8.9 MB     00:00     
Package epel-release-6-8.noarch already installed and latest version
Nothing to do
```

### 安装Docker

!> 命令： `yum install -y docker-io`

```bash
[guo@iZwz9hw8pun8vmbs0u0ckeZ ~]$ sudo yum install -y docker-io
Loaded plugins: fastestmirror
Setting up Install Process
Loading mirror speeds from cached hostfile
 * base: mirrors.aliyun.com
 * extras: mirrors.aliyun.com
 * nux-dextop: mirror.li.nux.ro
 * rpmfusion-free-updates: mirrors.ustc.edu.cn
 * rpmfusion-nonfree-updates: mirror.lzu.edu.cn
 * updates: mirrors.aliyun.com
No package docker-io available.
Error: Nothing to do
```

### 此时如果出现报错了应该是被Q了 

!> 命令：`yum install https://get.docker.com/rpm/1.7.1/centos-6/RPMS/x86_64/docker-engine-1.7.1-1.el6.x86_64.rpm`

```bash
[guo@iZwz9hw8pun8vmbs0u0ckeZ ~]$ sudo yum install https://get.docker.com/rpm/1.7.1/centos-6/RPMS/x86_64/docker-engine-1.7.1-1.el6.x86_64.rpm
Loaded plugins: fastestmirror
Setting up Install Process
docker-engine-1.7.1-1.el6.x86_64.rpm                                                                                  | 4.5 MB     01:48     
Examining /var/tmp/yum-root-SV4K89/docker-engine-1.7.1-1.el6.x86_64.rpm: docker-engine-1.7.1-1.el6.x86_64
Marking /var/tmp/yum-root-SV4K89/docker-engine-1.7.1-1.el6.x86_64.rpm to be installed
Loading mirror speeds from cached hostfile
 * base: mirrors.aliyun.com
 * extras: mirrors.aliyun.com
 * nux-dextop: mirror.li.nux.ro
 * rpmfusion-free-updates: mirrors.ustc.edu.cn
 * rpmfusion-nonfree-updates: mirror.lzu.edu.cn
 * updates: mirrors.aliyun.com
Resolving Dependencies
--> Running transaction check
---> Package docker-engine.x86_64 0:1.7.1-1.el6 will be installed
--> Processing Dependency: libcgroup for package: docker-engine-1.7.1-1.el6.x86_64
--> Running transaction check
---> Package libcgroup.x86_64 0:0.40.rc1-27.el6_10 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

=============================================================================================================================================
 Package                      Arch                  Version                           Repository                                        Size
=============================================================================================================================================
Installing:
 docker-engine                x86_64                1.7.1-1.el6                       /docker-engine-1.7.1-1.el6.x86_64                 19 M
Installing for dependencies:
 libcgroup                    x86_64                0.40.rc1-27.el6_10                updates                                          131 k

Transaction Summary
=============================================================================================================================================
Install       2 Package(s)

Total size: 19 M
Total download size: 131 k
Installed size: 20 M
Is this ok [y/N]: y
Downloading Packages:
libcgroup-0.40.rc1-27.el6_10.x86_64.rpm                                                                               | 131 kB     00:00     
Running rpm_check_debug
Running Transaction Test
Transaction Test Succeeded
Running Transaction
  Installing : libcgroup-0.40.rc1-27.el6_10.x86_64                                                                                       1/2 
  Installing : docker-engine-1.7.1-1.el6.x86_64                                                                                          2/2 
  Verifying  : docker-engine-1.7.1-1.el6.x86_64                                                                                          1/2 
  Verifying  : libcgroup-0.40.rc1-27.el6_10.x86_64                                                                                       2/2 

Installed:
  docker-engine.x86_64 0:1.7.1-1.el6                                                                                                         

Dependency Installed:
  libcgroup.x86_64 0:0.40.rc1-27.el6_10                                                                                                      

Complete!
```

### Docker的配置文件

!> 路径：`/etc/sysconfig/docker`

```bash
[guo@iZwz9hw8pun8vmbs0u0ckeZ ~]$ cat /etc/sysconfig/docker
# /etc/sysconfig/docker
#
# Other arguments to pass to the docker daemon process
# These will be parsed by the sysv initscript and appended
# to the arguments list passed to docker -d

other_args=""
```

### 启动Docker后台服务 

!> 命令：`service docker start`

```bash
[guo@iZwz9hw8pun8vmbs0u0ckeZ ~]$ sudo service docker start
Starting cgconfig service:                                 [  OK  ]
Starting docker:                                           [  OK  ]
[guo@iZwz9hw8pun8vmbs0u0ckeZ ~]$ service docker status
docker (pid  26928) is running...
```

### 查看Docker版本

!> 命令：`docker --version` & `docker version`

```bash
[guo@iZwz9hw8pun8vmbs0u0ckeZ ~]$ docker --version
Docker version 1.7.1, build 786b29d
[guo@iZwz9hw8pun8vmbs0u0ckeZ ~]$ sudo docker version
Client version: 1.7.1
Client API version: 1.19
Go version (client): go1.4.2
Git commit (client): 786b29d
OS/Arch (client): linux/amd64
Server version: 1.7.1
Server API version: 1.19
Go version (server): go1.4.2
Git commit (server): 786b29d
OS/Arch (server): linux/amd64
```