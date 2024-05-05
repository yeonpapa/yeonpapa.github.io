---
title: (DOCKER) 명령어
date: 2023-09-09 09:00:00:00 +0900
categories: [SW DevOps, Container]
tags: [swdevops, docker, host, linux]     # TAG names should always be lowercase
--- 

## Docker Image, Docker Container
IMAGE : 서비스 운영에 필요한 서버 프로그램, 소스코드 및 라이브러리, 컴파일된 실행 파일을 묶어놓은 것을 Image 라고한다.<br/>
LAYER : 기존 이미지에 추가적인 파일이 필요할 때 다시 처음부터 다운받는게 아니라 해당파일만 추가하는 개념. 파일이 추가 되면 새로운 Layer가 생성됨. 그래서 이미지와 레이어는 같은의미로도 사용됨. DockerHub 및 개인 저장소에서 이미지를 공유할 떄는 바뀐부분 Layer만 주고받기 가능하다.<br/>
CONTAINER : 이미지를 실행한 상태.

## 이미지를 만드는 방법 Commit과 Build
- commit <br/>
원본이미지 -> run -> 필요한 라이브러리 설치 -> commit -> 새로운 이미지<br/>

- build ( with Dockerfile )

```shell
$ docker build -t imageName:0.1 . # docker build -t 이미지이름 Dockerfile위치
```

## 이미지를 실행하는 방법 Container
- docker run [-옵션] [이미지식별자] [명령어] [매개변수] <br/>

```shell
$ docker run -d -it --name containerName imageName /bin/bash 
$ docker search centos # docker hub에서 공식이미지 찾기, 공식이미지는 xxx/centos처럼 /앞에 붙는 이름이 없음
$ docker pull centos:latest # 이미지 가져오기
$ docker images # host에서 도커이미지 목록 출력
$ docker ps -a #host내의 컨테이너 목록 출력
$ docker start <containerID> #컨테이너 시작
$ docker attach <containerID> #컨테이너 접속 or docker exec -it <컨테이너 ID 또는 이름> /bin/bash
$ docker commit [옵션] <컨테이너ID 또는 이름> <새로운_이미지_이름> 
# -a, --author: 커밋한 사용자 또는 작성자 정보를 지정합니다.
# -c, --change: 컨테이너에서 실행된 변경 사항을 추가합니다.
# -m, --message: 커밋에 대한 메시지를 지정합니다.
# -p, --pause: 컨테이너를 일시 중지하고 커밋을 수행합니다. (일반적으로 사용되는 옵션입니다)
$ # 이미지를 원격 레지스트리에 푸시
docker push {namespace}/{repositoryname}:tag # docker hub에 image push, 도커허브에 repository가 있어야 함.
```
#### Options
<figure style="margin-left: auto; margin-right: auto; display: block;">
    <img src="/assets/img/dockerrunoption1.png" alt="dockerrunoption1"> <figcaption>docker 옵션1</figcaption>
    <img src="/assets/img/dockerrunoption2.png" alt="dockerrunoption2"><figcaption>docker 옵션2</figcaption>
</figure>
<br>
