# 个人文档

## Mac 建立简单的本地服务器
> 适用于python2.*，如果是python3.*请用http.server 替换 SimpleHTTPServer

PYTHON自带HTTP服务，命令：
```
python -m SimpleHTTPServer
```
使用上述命令将当前目录发布到8000端口，为当前进行，不是后台运行

指定端口：
```
python -m SimpleHTTPServer 8000
```

指定后台运行，加&：
```
python -m SimpleHTTPServer 8000 &
```
生成的新的进程为当前bash的子进程，当关闭当前bash时，相应的子进程也会被kill掉，这也不是我们想要的结果。

```
nohup python -m SimpleHTTPServer 8000 &
```
加nohup，忽略所有的挂断信号，如果当前bash关闭，则当前进程会挂载到init进程下，成为其子进程，这样即使退出当前用户，其8000端口也可以使用。

注意
```
1. SimpleHTTPServer有一个特性，如果待共享的目录下有index.html，那么index.html文件会被视为默认主页；如果不存在index.html文件，那么就会显示整个目录列表。
2. 在哪个目录下启动，就会以当前目录为根目录展示列表
```