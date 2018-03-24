# Introduction

### 安装:(推荐使用docker的镜像,这样也不会“污染”本地环境)

**基于Ubuntu**

- 下载docker:
> sudo apt-get install docker.io
- 给予你自己使用docker的权限:
> sudo chmod o+wr /var/run/docker.sock
- 查找rabbmit镜像:
> docker search rabbitmq

你会看到：
```
docker search rabbitmq
NAME                                           DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
rabbitmq                                       RabbitMQ is an open source multi-protocol ...   1801      [OK]       
tutum/rabbitmq                                 Base docker image to run a RabbitMQ server      15                   
frodenas/rabbitmq                              A Docker Image for RabbitMQ                     12                   [OK]
bitnami/rabbitmq                               Bitnami Docker Image for RabbitMQ               9                    [OK]
...
```
- 下载rabbitmq镜像:
> docker pull rabbitmq
- 查看自己本地已经下载好的镜像:
> docker images
```
REPOSITORY            TAG                 IMAGE ID            CREATED             SIZE
rabbitmq              latest              b17bd9d70e8b        9 days ago          127 MB
```
- 运行rabbitmq镜像:
> docker run -d --name my-rabbitmq -p 4369:4369 -p 5671:5671 -p 5672:5672 -p 25672:25672 rabbitmq
- 查看自己已经运行的镜像:
> docker ps

## 说明:

- 你可能会遇到如下的warning:
```
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.27/containers/json: dial unix /var/run/docker.sock: connect: permission denied
```
因为本机与docker通信是socket通信，也就是通过 '/var/run/docker.sock' socket文件通信的,而这个文件的owner是root

> srw-rw---- 1 root docker 0 Mar 24 21:31 /var/run/docker.sock

对于你自己是没有权限使用这个文件的,所以你要为你添加权限才可以使用,所以才要运行:
> sudo chmod o+wr /var/run/docker.sock

或者其他方式什么都行,只要你能拿到读写权限就可以.

- 你会遇到当你再次开启电脑之后,运行 'docker ps' 的时候,看不到运行的容器, 请运行 'docker ps -a'，这是你会看到你的容器,你会看到你之前运行的那个容器的status是Exit状态.
  
  你可以:

  > docker restart CONTAINER-ID

  你也可以:

  > docker run -d --restart=always --name my-rabbitmq -p 4369:4369 -p 5671:5671 -p 5672:5672 -p 25672:25672 rabbitmq

- 其次在使用rabbitmq的时候,填写的host不在是localhost,而是通过 docker inspect CONTAINER-ID 中的 IP Address.

**额外说一句: 当你渐渐熟悉了docker,你会慢慢爱上它,会觉得它非常方便.**