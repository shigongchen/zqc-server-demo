# Zaiqiuchang server demo

Zaiqiuchang is a mobile app developed using React Native, both iOS and Android are supported. This project is the lite version of the api service code, which developed in Go, and deploy using Docker. The lite version is only including user related api, but it should be a good start point for developing any api service. 

### How to deploy

You need install [docker engine](https://docs.docker.com/engine/installation/) first.

**run in dev mode with auto detecting code changing**

```
> git clone git@github.com:jaggerwang/zqc-server-demo.git && cd zqc-server-demo
> mkdir -p ~/data/projects/zqc-server-demo # create directory for data volumes
> ./deploy.sh # pull images and run containers
> ./fswatch.sh # watching code change, fswatch needed
```
The data and log of server, mongodb and redis will be saved at host's path "~/data/projects/zqc-server-demo", which mounted at container's path "/data".

**run in prod mode**

Of course you should install docker engine first.
```
> git clone git@github.com:jaggerwang/zqc-server-demo.git && cd zqc-server-demo
> mkdir -p /data/zqc-server-demo # create directory for data volumes
> ./deploy-prod.sh
```
The data and log of server, mongodb and redis will be saved at host's path "/data/zqc-server-demo", which mounted at container's path "/data".

**build image of your own**

```
> cd zqc-server-demo
> ./docker-build.sh
```

**create mongodb index**

```
> cd zqc-server-demo
> docker-compose -p zqc-server-demo exec server zqc db createIndexes
```
When deploy, it will auto run this command to create mongodb index. So normally you do not need to do this by your own.

### API

The server container exposed port 1323, and it mapped to port 10400 of the host. So you can use domain "http://localhost:10400" to access the following api.

Path|Method|Description
----|------|-----------
/register|POST|Register account.
/login|GET|Login.
/isLogined|GET|Check whether logined.
/logout|GET|Logout.
/account/edit|POST|Edit account profile.
/account/info|GET|Get current account info.
/user/info|GET|Get user info by id.
/user/infos|GET|Get user info by ids.

### FAQ

**How to change image repository?**

> Search and replace all "daocloud.io/jaggerwang/zqc-server-demo" to your own.

**How can I build the base images of this project, including go, mongodb and redis?**

> The dockerfiles of the base images can be found at "https://github.com/jaggerwang/jw-dockerfiles".

### Other resources

* [技术文章 - Go + Docker API服务开发和部署](https://jaggerwang.net/develop-and-deploy-api-service-with-go-and-docker-intro/)
* [在球场官网](https://www.zaiqiuchang.com)
