---
title: DevOps Ubuntu에 docker설치하기
date: 2023-07-08 14:00:00:00 +0900
categories: [SW DevOps, Docker 설치]
tags: [swdevops, docker install, ubuntu]     # TAG names should always be lowercase
--- 

## ubuntu 
0. ```ubuntu version확인: $ lsb_release -a```
1. ```$ sudo apt-get update```
2. ```필요package설치: $ sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common```
3. ```docker 공식 GPG키 설치: $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -```
4. ```docker 공식 apt저장소 추가: $ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"```
5. ```$ sudo apt-get update```
6. ```도커설치: $ sudo apt-get install docker-ce docker-ce-cli containerd.io```
7. ```도커버전확인: $ sudo docker -v```
8. ```설치확인: $ sudo systemctl status docker``` or ```$ service docker status```
9. ```도커 서비스등록 및 서비스실행: $ sudo systemctl enable docker && service docker start```<br>
10. Install Portainer with Docker
- create volume ```$ sudo docker volume create portainer_data``` and then ```$ sudo docker volume ls```<br>
  - volume은 docker area에 생긴 directory임. 그냥 mkdir로 내가 특정 위치에 폴더를 만들고 그것을 컨테이너와 연결해도 됨.
  - ```볼륨정보확인: $ docker volume inspect portainer_data```
- install portainer<br>
```$ docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:2.11.0```




## Windows
> Windows 10/11 Home --> WSL2 기반 Docker Engine 사용<br> Windows 10/11 Pro --> Hyper-V기반(Old), WSL2 기반 모두 Docker Engine 사용

1. Windows Terminal로 설치, windows terminal은 wsl2 쉘을 바로 실행할수있는 장점이 있음.<br> Powershell에서 ```winget install --id=Microsoft.WindowsTerminal -e``` <br> 또는 chocolately로 설치 ```choco install microsoft-windows-terminal```
2. ```$ dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart```<br>
```$ dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart```
<br>두 명령어 모두 ‘작업을 완료했습니다’ 메시지가 나와야 정상. --> 윈도우를 재부팅합니다.

3. [x64 머신용 WSL2 커널](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)업데이트 패키지 설치.
4. ```$ wsl --set-default-version 2```
5. [Docker Desktop](https://www.docker.com/products/docker-desktop/) 설치
6. Docker Desktop 설정 <br> Settings-General-Use the WSL 2 based engine 항목 check~!!! <br> Settings-Resources-WSL Integration - Enable integration with my default WSL distro 항목 check~!!!
