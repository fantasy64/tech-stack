

1 进入docker的几种方法 

```
#参数<CONTAINER ID>对应docker ps展示的值：
#1） 使用docker exec
docker exec -it <CONTAINER ID> /bin/bash
#2） 使用nsenter
PID=$(docker inspect --format {{.State.Pid}} <CONTAINER ID>)
nsenter --target $PID --mount --uts --ipc --net --pid```
```



2 docker的常用命令

参考链接https://www.jianshu.com/p/adaa34795e64

# 容器类

## 查看容器信息

```shell
# 查看当前运行的容器
docker ps
# 查看全部容器
docker ps -a
# 查看全部容器的id和信息
docker ps -a -q
# 查看全部容器占用的空间
docker ps -as
# 查看一个正在运行容器进程，支持 ps 命令参数
docker top
# 查看容器的示例id
sudo docker inspect -f  '{{.Id}}' [id]
# 检查镜像或者容器的参数，默认返回 JSON 格式
docker inspect
# 返回 ubuntu:14.04  镜像的 docker 版本
docker inspect --format '{{.DockerVersion}}' ubuntu:14.04
docker inspect --format='{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ubuntu:14.04
```

## 容器同步命令

```shell
# 保存对容器的修改
docker commit
# 保存某个容器成为一个镜像
docker commit -a "user" -m "commit info" [CONTAINER] [imageName]:[imageTag]
# 推送一个容器到中心仓库
docker login --username=[userName] --password=[pwd] [registryURL]
## 建议登录后查看 docker info
docker tag [imageID] [remoteURL]:[imageTag]
docker push [remoteURL]:[imageTag]
# 拉取提交的容器
docker pull [remoteURL]:[imageTag]
# 对比容器的改动
docker diff
# 附加到一个运行的容器上
docker attach
```

## 创建和删除容器

```shell
# 创建一个容器命名为 test 使用镜像daocloud.io/library/ubuntu
docker create -it --name test daocloud.io/library/ubuntu
# 创建并启动一个容器 名为 test 使用镜像daocloud.io/library/ubuntu
docker run --name test daocloud.io/library/ubuntu
# 删除一个容器
docker rm [容器id]
# 删除所有容器
docker rm `docker ps -a -q`
# 根据Dockerfile 构建
docker build -t [image_name] [Dockerfile_path]
```



## 容器的启动和停止

```shell
#启动|停止|重启
docker start|stop|restart [id]
# 暂停|恢复 某一容器的所有进程
docker pause|unpause [id]
# 杀死一个或多个指定容器进程
docker kill -s KILL [id]
# 停止全部运行的容器
docker stop `docker ps -q`
# 杀掉全部运行的容器
docker kill -s KILL `docker ps -q`
```



# 镜像操作

## 远程镜像

```shell
docker search
# 搜索处收藏数不小于 3 ，并且能够自动化构建的  django 镜像，并且完整显示镜像描述
docker search -s 3 --automated --no-trunc django
docker pull
# 拉取ubuntu最新的镜像
docker pull ubuntu:latest
# 服务器拉取个人动态，可选择时间区间
docker events
# 拉取个人从 2015/07/20 到 2015/08/08 的个人动态
docker events --since="20150720" --until="20150808"

```



## 镜像同步操作

```shell
# 标记本地镜像，将其归入某一仓库
docker tag
# 将 ID 为 5db5f84x1261 的容器标记为 mine/lnmp:0.2 镜像
docker tag 5db5f84x1261 mine/lnmp:0.2
# 将镜像推送至远程仓库，默认为 Docker Hub
docker push

```



## 本地镜像

```she
# 列出本地所有镜像
docker images
# 本地镜像名为 ubuntu 的所有镜像
docker images ubuntu
# 查看指定镜像的创建历史
docker history [id]
# 本地移除一个或多个指定的镜像
docker rmi
# 移除本地全部镜像
docker rmi `docker images -a -q`
# 指定镜像保存成 tar 归档文件， docker load 的逆操作
docker save
# 将镜像 ubuntu:14.04 保存为 ubuntu14.04.tar 文件
docker save -o ubuntu14.04.tar ubuntu:14.04
# 从 tar 镜像归档中载入镜像， docker save 的逆操作
docker load
# 上面命令的意思是将 ubuntu14.04.tar 文件载入镜像中
docker load -i ubuntu14.04.tar
docker load < /home/save.tar
# 构建自己的镜像
docker build -t <镜像名> <Dockerfile路径>
docker build -t xx/gitlab .

```

