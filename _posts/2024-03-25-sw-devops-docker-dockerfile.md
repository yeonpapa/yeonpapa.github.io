---
title: (DOCKER) Dockerfile, docker-compose
date: 2024-03-25 09:00:00:00 +0900
categories: [SW DevOps, Container]
tags: [swdevops, docker, dockerfile, docker-compose]     # TAG names should always be lowercase
--- 

## Dockerfile
Docker image를 만들기 위한 파일. 문서로서 이미지를 생성하고 실행(컨테이너)함.

``` Dockerfile
FROM python:3.9
COPY requirements.txt app/requirements.txt
WORKDIR /app
RUN pip install -r requirements.txt
COPY . /app
EXPOSE 8501
CMD ["streamlit", "run", "echart_demo.py","--server.port 8502"] # 명령어에 맞는 옵션을 줄수 있다.
```

## docker-compose
- 하나의 문서에 여러 개의 컨테이너를 정의<br>
- Docker Compose는 다중 컨테이너 애플리케이션을 정의 공유할 수 있도록 개발된 도구로 단일 명령을 사용하여 모두 실행 또는 종료할 수 있도록 개발된 도구

```yaml
version: '3'  # docker-compose file format의 버전
services:
  streamlit_app:
    build: .     #현재 디렉토리에서 Dockerfile을 찾아서 빌드
    image: test/test:1.1 # 빌드이미지 이름을 지정함. docker build -t imageName:0.1 . 이렇게 command라인에서 이름을 지정하거나 docker-compose.yml 에서 지정함. Dockerfile에서는 이름을 지정할 수 없음.
    container_name : test # container의 이름을 지정함.
    volumes:
      - .:/app
    ports:
      - 8501:8501
```
## docker-compose 실행명령어
``` shell
> docker-compose build --no-cache # 이미지를 완전히 새로 빌드
> docker-compose up -d --build  #docker를 새로빌드하면서 컨테이너를 서비스(-d)로 실행.
> docker-compose -f yaml파일path -p container_name up 
```

## docker compose 예시
``` yml
version: "3.8"
services:
    //1. 빌더 컨테이너
    builder:
        //build를 통해 도커파일 경로(context),지정(dockerfile). 도커파일에서 사용하는 환경변수(.env파일)를 파라미터(args)로 지정
        build:
            context: .
            dockerfile: builder.Dockerfile
            args:
                USER_UID: ${USER_UID}
                USER_GID: ${USER_GID}
                DOCKER_UID: ${DOCKER_UID}
        user: "root"
        //컨테이너 안에서 작동하는 명령 지정. 어떤 프로그램을 이용하여 실행해야 하는지를 지정하는것으로 필수이며, 컨테이너가 꺼지는 현상을 방지한다.
        command: /bin/sh -c "sleep infinity"
        container_name: choi-dev
        working_dir: /workspace
        //2가지 방법(volume vs bind mount)
        volumes:
            - type: volume
              source: choi
              target: /home/vscode/.vscode-server
            - type: volume
              source: vscode-server-insiders-choi
              target: /home/vscode/.vscode-server-insiders
            - type: bind
              source: /var/run/docker.sock
              target: /var/run/docker.sock
            - type: bind
              source: ../
              target: /workspace
            - type: bind
              source: ~/.m2
              target: /home/vscode/.m2
            - type: bind
              source: ~/ent
              target: /ent
        //커스텀 네트워크 설정
        networks:
            - choi-net
    //2. vespa 컨테이너
    //image를 통해 이미지를 직접 빌드
    vespa-choi:
        image: engine:7.594.36
        container_name: choi
        hostname: choi-net
        //포트 포워딩 : 호스트와 컨테이너 포트를 바인딩. 컨테이너의 target포트와 호스트의 published 포트와 연결해준다.
        ports:
            - target: 19071
              published: 19072
              protocol: tcp
              mode: host
            - target: 8080
              published: 9091
              protocol: tcp
              mode: host
        //마운트할 볼륨 명 : 컨테이너 내부 경로
        volumes:
           - choi-data:/opt/engine/var
           - choi-logs:/opt/engine/logs
           - ~/ent:/ent
           - ~/payco/default-env.txt:/opt/engine/conf/engine/default-env.txt
        networks:
           - choi-net

//데이터 볼륨 정의
volumes:
    server-choi:
    vscode-server-insiders-choi:
    choi-data:
    choi-logs:

//bridge(많이 사용) : 하나의 호스트 컴퓨터 내에서 여러 컨테이너들이 서로 소통할 수 있도록 해줌
networks:
    choi-net:
        driver: bridge
```

