---
title: (MongoDB) MongoDB 설치 방법
date: 2023-09-06 13:00:00:00 +0900
categories: [SW Development, Backend]
tags: [swdev, mongodb, install]     # TAG names should always be lowercase
--- 

### MongoDB 설치 방법 
#### 1. Linux HOST 에 설치 (Ubuntu 22.04, jammy) [참고](https://www.leafcats.com/289)
- 새로운 리파지토리 추가하는데 필요한 종속성 설치. 이미 설치되어있을수도 있음.
```shell
$ sudo apt update
$ sudo apt install dirmngr gnupg apt-transport-https ca-certificates software-properties-common
```
- MongoDB Repository 추가(MongoDB 6.0버전)
```shell
$ wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
$ sudo echo 'deb [arch=amd64] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/6.0 multiverse' | sudo tee /etc/apt/source.list.d/mongodb-org-6.0.list
```
- 설치
```shell
$ sudo apt update
$ sudo apt-get install mongodb-org
```
- 확인<br/>
```shell
$ systemctl status mongod # or service mongod status
$ systemctl start mongod # or service mongod start
$ systemctl restart mongod # or service mongod restart
$ systemctl stop mongod # or service stop status
```
- 정상상태
> ? mongod.service - MongoDB Database Server<br/>
     Loaded: loaded (/lib/systemd/system/mongod.service; enabled; vendor preset: enabled)<br/>
     Active: active (running) since Fri 2020-05-15 05:30:39 UTC; 18s ago<br/>
       Docs: https://docs.mongodb.org/manual<br/>
   Main PID: 106996 (mongod)<br/>
     Memory: 76.0M<br/>
     CGroup: /system.slice/mongod.service<br/>
             ??106996 /usr/bin/mongod --config /etc/mongod.conf<br/>
             <br/>
  May 15 05:30:39 ubunt4 systemd[1]: Started MongoDB Database Server.<br/>
  May 15 05:30:48 ubunt4 systemd[1]: /lib/systemd/system/mongod.service:11: PIDFile= references a path below legacy directory /var/run/, upd> lines 1-11/11 (END)

- mongodb client만 설치
```shell
$ mongo --version
  The program 'mongo' is currently not installed. You can install it by typing:
  apt-get install mongodb-clients
$ apt-get install mongodb-clients
$ mongo --version
  MongoDB shell version: 2.4.9
$ mongo 172.17.0.4 #mongodb 접속
``` 
<br/>

#### 2. Docker-Container 내부에 설치 (HOST에 ubuntu docker를 띄우고 그안에 mongodb설치 --> 이렇게 잘 안씀.)
> Host Ubuntu에 설치하는 것과 동일하나, 
- systemctl이 먹지 않는 문제, [MongoDB가 설치된 우분투 이미지 만들기](https://5w33th0me4jisu.tistory.com/entry/Docker-MongoDB%EA%B0%80-%EC%84%A4%EC%B9%98%EB%90%9C-%EC%9A%B0%EB%B6%84%ED%88%AC-%EC%9D%B4%EB%AF%B8%EC%A7%80-%EB%A7%8C%EB%93%A4%EA%B8%B0feat-commit)
- service mongod start로 실행해도 fail 됨. 이 경우 /etc/systemd/system폴더에 /lib/systemd/system/mongod.service를 심볼릭링크로 잡아주거나 하는 trouble shooting 가이드가 구글링을 통해 찾았으나, 잘 되지 않음.[참고](https://gdtbgl93.tistory.com/113) [참고2](http://joonas.tistory.com/38)

<br/>

#### 3. with Mongodb image로 Docker Container로 설치, 실행
> 타 container내부에 mongodb를 설치하는 것이 아니라, mongodb 자체를 컨테이너로 만들어 띄운다.
<br/>

```shell
$ docker pull mongo
$ docker images
$ docker run --name mongodb-container -v /docker/mongodb_data:/data/db -d -p 27017:27017 mongo
```

#### 4. with mongodb image로 Docker-compose로 설치, 실행
아래와 같이 하게되면 root계정이 생겨서, 접근권한 제어가 가능하다.
``` shell
version: "3"
services:
  mongodb:
        image: mongo
        restart: always
        ports:
          - 27017:27017
        environment:
          - MONGO_INITDB_ROOT_USERNAME=mongoadmin
          - MONGO_INITDB_ROOT_PASSWORD=digital21
        volumes:
          - ./data:/data/db
  mongo-express:
        image: mongo-express
        container_name: mongo-express
        restart: always
        ports:
          - 8081:8081
        environment:
          - ME_CONFIG_MONGODB_ADMINUSERNAME=mongoadmin
          - ME_CONFIG_MONGODB_ADMINPASSWORD=digital21
          - ME_CONFIG_MONGODB_SERVER=mongodb
          - ME_CONFIG_MONGODB_PORT=27017
          - ME_CONFIG_BASICAUTH_USERNAME=mongoadmin
          - me_CONFIG_BASICAUTH_PASSWORD=digital21
        depends_on:
          - mongodb
```
``` shell
//실행
> docker-compose up -d
```
#### 5. Windows에 설치


### 6. HOST설치된 MongoDB 삭제 방법 
1. Ubuntu
```shell
$ sudo service mongod stop # 서비스를 먼저 멈춤
$ sudo apt remove mongodb-org* # 패키지삭제
$ sudo apt-get purge mongodb-org* # 패키지 환경파일 삭제
$ sudo rm -r /var/log/mongodb #log삭제
$ sudo rm -r /var/lib/mongodb #data삭제
$ sudo apt list --installed | grep mongo #설치된 패키지 확인
```