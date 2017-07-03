## 安装docker  
Docker 软件包已经包括在默认的 CentOS-Extras 软件源里。因此想要安装 docker，只需要运行下面的 yum 命令：  
`yum install docker-io -y`  
直接yum安装，安装成功后查看版本  
`docker -v`  
启动docker  
`service docker start`  
设置开机启动  
`chkconfig docker on`  


## 配置 Docker  
因为国内访问 Docker Hub 较慢, 可以使用腾讯云提供的国内镜像源, 加速访问 Docker Hub  
依次执行以下命令  
`echo "OPTIONS='--registry-mirror=https://mirror.ccs.tencentyun.com'" >> /etc/sysconfig/docker`  
`systemctl daemon-reload`  
`service docker restart`  

## 下载镜像  
下载一个官方的 CentOS 镜像到本地  
`docker pull centos`  
下载好的镜像就会出现在镜像列表里  
`docker images`  

## 运行容器  
这时我们可以在刚才下载的 CentOS 镜像生成的容器内操作了。  
生成一个 centos 镜像为模板的容器并使用 bash shell  
`docker run -it centos /bin/bash`  
这个时候可以看到命令行的前端已经变成了 [root@(一串 hash Id)] 的形式, 这说明我们已经成功进入了 CentOS 容器。  
在容器内执行任意命令, 不会影响到宿主机, 如下  
`mkdir -p /data/simple_docker`  
可以看到 /data 目录下已经创建成功了 simple_docker 文件夹  
`ls /data`  
退出容器  
`exit`  
查看宿主机的 /data 目录, 并没有 simple_docker 文件夹, 说明容器内的操作不会影响到宿主机  
`ls /data`   

## 保存容器
查看所有的容器信息， 能获取容器的id  
`docker ps -a`  
然后执行如下命令，保存镜像：  
`docker commit -m="备注" 你的CONTAINER_ID 你的IMAGE`  
ex: `docker commit -m="my centos_image" 477562cd2878 mycentos`  
再次执行docker images查看自己的镜像列表，发现已经多了一个你自己保存的镜像。
运行保存的镜像，再次查看/data目录是否有simple_docker文件夹。
`docker run mycentos ls /data`
