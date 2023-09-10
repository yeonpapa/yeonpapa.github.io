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
$ docker run -d -it --name containerName imageName bash 
```
#### Options
<figure style="margin-left: auto; margin-right: auto; display: block;">
    <img src="/assets/img/dockerrunoption1.png"> <figcaption>docker 옵션1</figcaption>
    <img src="/assets/img/dockerrunoption2.png"><figcaption>docker 옵션2</figcaption>
</figure>
<br>
