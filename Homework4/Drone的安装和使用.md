# Drone的安装和使用
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
## 访问OAuth app的地址查看结果
![](https://github.com/CJTSAJ/homework-of-pro-ren/blob/master/Homework4/png/2.png)
