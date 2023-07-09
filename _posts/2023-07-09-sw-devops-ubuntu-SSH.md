---
title: (Ubuntu) SSH Server
date: 2023-07-09 11:00:00:00 +0900
categories: [SW DevOps, OS]
tags: [swdevops, linux, ubuntu, ssh]     # TAG names should always be lowercase
--- 

## SSH 설치와 접속방법 
0. Open SSH Server 설치
   - ```$ sudo apt update```
   - ```$ sudo apt install openssh-server```
1. SSH Server
   - ssh 서비스가 실행 중 인지 확인 ```$ sudo systemctl status ssh```
   - active (running) 이면 실행 중
2. SSH enable / start (서비스가 inactive이면 아래 명령어로 enable,start시킴)
   - ```$ sudo systemctl enable ssh```
   - ```$ sudo systemctl start ssh```
3. SSH Client
   - ```$ sudo apt-get install openssh-client```
   - ```$ ssh username@ip_address```
   - (포트지정할 경우) ```$ ssh -p 10001 username@ip_address```
4. Firewall
   - 방화벽 상태 확인 ```$ sudo ufw status```
   - 방화벽에서 ssh 허용 ```$ sudo ufw allow ssh```
5. SSH port변경
   - SSH를 외부에 노출할떄는 22번 포트가 아닌 다른 포트로 변경하는 것이 좋음
   - **/etc/ssh/sshd_config** 파일 수정, Port는 여러개 지정가능
   ```bash
   ## ssh 포트
   ## Port 22
   Port 10022
   Port 20022 
   ```
   ```$ sudo systemctl restart sshd``` or ```$ sudo service sshd restart```
