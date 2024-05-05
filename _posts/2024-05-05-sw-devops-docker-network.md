---
title: (DOCKER) Docker network
date: 2024-05-05 14:00:00:00 +0900
categories: [SW DevOps, Container]
tags: [swdevops, docker, network]     # TAG names should always be lowercase
--- 

## docker network
도커 네트워크(Docker Network) 란 Docker 컨테이너 간의 통신을 관리하고 격리하기 위한 기능을 제공하는 것.
컨테이너화된 애플리케이션은 여러개의 컨테이너로 구성될 수 있는데, 이들 컨테이너가 서로 통신하고 데이터를 주고 받아야 할 경우다.
도커 네트워크를 통해 이러한 컨테이너간 통신을 쉽게 설정하고 관리할 수 있도록 도와 준다.
정리하자면, 같은 호스트 내에서 실행중인 컨테이너 간 연결할 수 있도록 돕는 논리적 네트워크 개념.
docker compose 버전 2에서는 --link 옵션으로 사용하였으나, 지금은 -- networks로 바뀜

<figure style="margin-left: auto; margin-right: auto; display: block;">
    <img src="/assets/img/dockernetwork2.png" alt="overlay"><figcaption>docker_network</figcaption>
    <img src="/assets/img/dockernetwork1.PNG" alt="docker_Network"><figcaption>단일 - 도커네트워크</figcaption>
    <img src="/assets/img/dockernetwork_overlay.PNG" alt="overlay"><figcaption>다중 - Overlay네트워크</figcaption>
</figure>

## 단일 호스트 네트워크(bridge(default),bridge(custom) host, none)
- default bridge 네트워크(docker0) : 기본적으로 컨테이너를 생성하면 docker0 네트워크에 물린다. 그래서 기본적으로 통신이 ip형태로 가능
- custom bridge 네트워크 : 사용자가 네트워크를 생성함. 같은 이름의 네트워크에 컨테이너가 생성되면 컨테이너 이름으로 통신이 가능 ping <container_name>하면 ping이 먹는다. ```docker network create --driver=bridge my-bridge```

- host : host 네트워크는 도커가 제공해주는 가상 네트워크 인터페이스(veth) 을 상요하는 것이 아니라 이름 그대로 host 의 네트워크에 붙어서 사용하는 개념. ```docker run -d --network=host httpd```

- none: none 네트워크 는 해당 컨테이너가 네트워크 기능이 필요 없을 때, 혹은 커스텀 네트워크를 사용해야 되는 경우가 있을 때 네트워크 드라이버를 none 으로 설정하고 사용할 수 있습니다 , 즉 외부 네트워크와의 연결이 단절.```docker run -d --network=none nginx:latest```

## 다중 호스트 네트워크(overlay)
dockerswarm이나 kubernetis환경, 즉 multi hosting환경에서의 네트워크 설정에 사용됨.

<br>

``` yml
# docker compose network 예제
services:
  db: 
    image: postgres:latest
    restart: always
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
    ports:
      - 5432:5432
    volumes:
      - db:/var/lib/postgresql/data
    networks:
      - mynet
  
  web-app:
    image: web-app:latest
    depends_on: 
      - db
    networks:
      - mynet
    ports:
      - 8080:8080
    environment:
      - DB_HOST=db
      - DB_PORT=5432
      - DB_USER=postgres
      - DB_PASSWORD=postgres
      - DB_NAME=postgres

networks:
  mynet:
    driver: bridge

volumes: 
  db:
    driver: local
```

## docker network 실행명령어
``` shell
> docker network ls # host에 존재하는 docker network목록 조회
> docker network inspect bridge  # bridge네트워크 상세조회
> docker network inspect test-network # test-network 상세조회
> docker network create --driver=bridge test-network # user defined 네트워크 생성
> docker run -dit --network=test-network <container-name> # 컨테이너 실행시 network연결
> docker network connect test-network <container-name> #이미 실행중인 container-name을 test-network에 연결
```