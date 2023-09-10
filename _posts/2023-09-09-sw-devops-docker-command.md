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
- commit <br>
원본이미지 -> run -> 필요한 라이브러리 설치 -> commit -> 새로운 이미지<br/>

- build ( with Dockerfile )

```shell
$ docker build -t imageName:0.1 . # docker build -t 이미지이름 Dockerfile위치
```

## 이미지를 실행하는 방법 Container
- docker run [옵션] [이미지] [명령] [매개변수] <br/>

```shell
$ docker run -d -it --name containerName imageName bash 
```
#### Options
1. **-i, --interactive** <br/>
표준 입력stdin을 활성화하며, 컨테이너와 연결attach되어 있지 않더라도 표준 입력을 유지합니다.
보통 이 옵션을 사용하여 Bash 에 명령을 입력합니다.<br/>
2. **-t, --tty** <br/>
TTY 모드pseudo-TTY를 사용합니다. Bash를 사용하려면 이 옵션을 설정해야 합니다.
이 옵션을 설정하지 않으면 명령을 입력할 수는 있지만, 셸이 표시되지 않습니다.<br/>
3. **--name** <br/>
컨테이너 이름을 설정합니다.<br/>
4. **-d, --detach** <br/>
Detached 모드입니다. 보통 데몬 모드라고 부르며, 컨테이너가 백그라운드로 실행됩니다.<br/>
5. **-p, --publish** <br/>
호스트와 컨테이너의 포트를 연결합니다. (포트포워딩) [호스트 포트]:[컨테이너 포트] -p 80:80<br/><br/>
6. **--privileged** <br/>
컨테이너 안에서 호스트의 리눅스 커널기능(Capability)을 모두 사용.
호스트의 주요 자원에 접근할 수 있습니다.<br/>
7. **--rm** <br/>
프로세스 종료시 컨테이너 자동 제거 <br/>
8. **--restart** <br/>
컨테이너 종료 시, 재시작 정책을 설정합니다. --restart="always"<br/>
9. **-v, --volume**<br/>
데이터 볼륨을 설정입니다. 호스트와 컨테이너의 디렉토리를 연결하여, <br/>
파일을 컨테이너에 저장하지 않고 호스트에 바로 저장합니다.(마운트)<br/>
10. **-u, --user** <br/>
컨테이너가 실행될 리눅스 사용자 계정 이름 또는 UID를 설정합니다. --user root <br/>
11. **-e, --env** <br/>
컨테이너 내에서 사용할 환경 변수를 설정합니다.<br/>
보통 설정 값이나 비밀번호를 전달할 때 사용합니다. -e GRANT_SUDO=yes<br/>
12. **--link** <br/>
컨테이너끼리 연결합니다. [컨테이너명 : 별칭] --link="db:db"
13. **-h, --hostname**<br/>
컨테이너의 호스트 이름을 설정합니다.<br/>
14. **-w, --workdir** <br/>
컨테이너 안의 프로세스가 실행될 디렉터리를 설정합니다.<br/>
15. **-a, --attach** <br/>
컨테이너에 표준 입력(stdin), 표준 출력(stdout), 표준 에러(stderr) 를 연결합니다.<br/>
16. **-c, --cpu-shares** <br/>
CPU 자원 분배 설정입니다. 기본 값은 1024이며, 각 값은 상대적으로 적용됩니다.<br/>
17. **-m, --memory** <br/>
메모리 한계를 설정합니다.<숫자><단위> 형식이며 단위는 b, k, m, g 를 사용할 수 있습니다 --memory=”100000b” <br/>
18. **--gpus** <br/>
컨테이너에서 호스트의 NVIDIA GPU 를 사용할 수 있도록 설정합니다.호스트는 NVIDIA GPU 가 장착 된 Linux 서버여야하며,
NVIDIA driver 가 설치되어 있어야하고, docker 19.03.5 버전 이상이어야합니다.<br/>
19. **--gpus all** <br/> GPU 모두 사용하기<br/>
20. **--gpus ‘”device=0,1”’** <br/> GPU 지정해서 사용하기<br/>
21. **--security-opt** <br/>
SELinux, AppArmor 옵션을 설정합니다. <br/>
22. **--security-opt=”label:level:TopSecret”**