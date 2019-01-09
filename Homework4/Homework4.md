# Requirment1
## 1.安装Docker
```
apt-get update
apt-get install docker.io
```
## 2.安装docker-compose
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
给予运行权限：

```
sudo chmod +x /usr/local/bin/docker-compose
```
## 3.得到Drone的Docker image
```
docker pull drone/drone:0.8
```
## 4.设置OAuth application，以此联系Drone与github
![](https://github.com/CJTSAJ/homework-of-pro-ren/blob/master/Homework4/png/1.png)
## 5.使用docker-compose下载Drone，并启动Drone Server
新建docker-compose.yaml文件

用对应的信息为environment中的变量赋值，包括DRONE\_HOST、DRONE\_ADMIN、DRONE\_GITHUB\_CLIENT、DRONE\_GITHUB\_SECRET、DRONE\_SECRET	。

其中DRONE\_HOST为OAuth application中所设置的地址。DRONE_ADMIN为github用户名。DRONE\_GITHUB\_CLIENT、DRONE\_GITHUB\_SECRET可以在创建好的OAuth app中查看。DRONE\_SECRET为自定义的server与agent连接的密钥。

```
version: '2'

services:
  drone-server:
    image: drone/drone:0.8

    ports:
      - 80:8000
      - 9000
    volumes:
      - drone-server-data:/var/lib/drone/
    restart: always
    environment:
      - DRONE_OPEN=true
      - DRONE_HOST=${DRONE_HOST}
      - DRONE_GITHUB=true
      - DRONE_ADMIN=${GITHUB_USERNAME}
      - DRONE_GITHUB_CLIENT=${DRONE_GITHUB_CLIENT}
      - DRONE_GITHUB_SECRET=${DRONE_GITHUB_SECRET}
      - DRONE_SECRET=${DRONE_SECRET}
      
  drone-agent:
    image: drone/agent:0.8

    command: agent
    restart: always
    depends_on:
      - drone-server
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    environment:
      - DRONE_SERVER=drone-server:9000
      - DRONE_SECRET=${DRONE_SECRET}

volumes:
  drone-server-data:
```
运行docker-compose

```
docker-compose up
```

## 配置集成项目
- 登录drone服务，设置hook，监听仓库动态
- 编写前后端.drone.yml和dockerfile文件
- 前后端打包入docker hub，在服务器上运行这两个docker镜像，设置对应端口后，可用浏览器进行访问
- [前端](https://github.com/CJTSAJ/drone) [后端](https://github.com/CJTSAJ/drone-backend)

![](https://github.com/CJTSAJ/homework-of-pro-ren/blob/master/Homework4/png/2.png)

# Requierment2
## 在单机上部署kubernate
#### 安装docker
```
sudo apt-get update
sudo apt-get install docker.io
```

#### 安装虚拟机
```
sudo apt-get install virtualbox
```

#### 安装kubectl
由于防火墙原因，国内不可以直接下载安装包，我将下载好的安装包上传到自己的github，然后从服务器拉取，解压

#### 安装minikube
```
curl -Lo minikube http://kubernetes.oss-cn-hangzhou.aliyuncs.com/minikube/releases/v0.28.0/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
```

#### 启动minikube
```
sudo minikube start --vm-driver=none
```

#### 启动容器服务
```
sudo kubectl run kube-nginx999 --image=nginx:latest --port=80 --image-pull-policy=IfNotPresent
```
#### 查看状态
```
root@data2:/# sudo kubectl get pods
NAME                            READY   STATUS    RESTARTS   AGE
kube-nginx999-ff58f75b7-fxndz   1/1     Running   0          1m
```

#### 打开dashboard
dashboard暂时无法打开，不知原因
```
root@data2:/# minikube dashboard --url
http://172.17.32.12:30000
```

### 项目未完成，将继续跟进，希望老师通融
