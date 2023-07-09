---
title: Ubuntu에 VS Code로 Remote 연결
date: 2023-07-09 14:00:00:00 +0900
categories: [SW DevOps, Container]
tags: [swdevops, vs code, remote, ubuntu]     # TAG names should always be lowercase
--- 

## VS Code로 Ubuntu Server 원격 연결
> Client : Windows 10, Server : Ubuntu <br> Client에 VScode 설치하고 VScode로 Ubuntu server에 원격으로 로그인하여 개발함.<br>
Putty를 사용하지 않고 보다 나은 IDE환경을 갖추어 일할 수 있음.

1. VS Code Extension - Remote Development 설치
   - Windows에 VS Code를 설치한 후, Remote Development extension설치
   - **F1** 키(Ctrl+Shift+P or F1 : Show Command Palette)를 눌러 **Remote-SSH: Connect to Host** 실행
2. ssh 접속
   - ```$ ssh -p portnumber username@ip_address``` 
   - portnumber 생략하면 default = 22 
3. ssh-key 로 접근
   - ```> ssh-keygen -t rsa -b 4096```
   - **C:\user\username\.ssh\id_rsa.pub** 의 내용을 서버의 **vi /home/yeonpapa/.ssh/authorized_keys** 에 복사해서 붙여넣음
   - 여기서 주의할 것은 ubuntu 서버에 접속하는 계정(yeonpapa) home 디렉토리 밑에 .ssh 안에 authorized_keys에 붙여넣어야 함.<br> root계정이나 다른 계정 하위에 키를 넣으면 안됨.
4. C:\Users\Administrator\.ssh\config 파일 수정
   ```config
      Host My_Ubuntu_Home
         HostName 192.168.0.9
         User yeonpapa
         IdentityFile ~/.ssh/id_rsa
   ```
   
